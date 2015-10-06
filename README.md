# 安装
## node

-   使用 Homebrew 安装 node （OS X）
    
        ruby -e "$(curl -fsSkL raw.github.com/mxcl/homebrew/go)"
        brew install node

-   使用 nvm 安装 node  

        wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.27.0/install.sh | bash
        nvm install 0.10.38
        nvm use 0.10.38 --default


-   源码编译

        sudo apt-get install build-essential libssl-dev
 
        curl -O http://nodejs.org/dist/node-latest.tar.gz
        tar zxvf node-latest.tar.gz
        cd node-v*
        ./configure
        make
        sudo make install
        node -v

## npm

-   寻找包
    
    `npm search`

-   安装包

    `npm install [-g]`

-   包文档

    `npm docs`

-   包源码

    `npm explore [-g]`

# 调试
## 代码检查

-   `JSLint`
    
    JSLint是一个JavaScript验证工具（非开源），可以扫描JavaScript源代码来查找问题。

-   `JSHint`

    JSHint是基于JSLint的项目,JSLint是一个存在了十多年的JavaScript源码分析工具。然而
    JSLint的可配置性不太强,因此促生了JSHint。

    <https://github.com/jshint/jshint>

    <https://github.com/jshint/node-jshint>
    
        npm install -g jshint
        jshint my_app.js

-   `JSCritic`    

    JSCritic 是一个 JavaScript 代码质量检测工具。该工具使用 JSHint 进行检查代码质量，同时提供一个在线的版本。

    <https://github.com/kangax/jscritic>

-   `node-jscs`

    node-jscs 是一个 JavaScript 的代码风格检查工具。可在 Node.js 和浏览器中使用

    <https://github.com/jscs-dev/node-jscs>

## 调试输出

-   `console.log`

    用来向标准输出中输出程序的状态信息

    console.info 是同一函数的另一个名称。

    可以给出 printf() 风格的参数，如： `console.log('Counter: %d', counter);`

-   `console.warn`, `console.error`

    而输出警告和错误信息的 console.warn 和 console.error 函数也差不多。唯一的区别是
    它们不是显示到标准输出中,而是显示到标准错误中。

-   `console.dir`

    输出对象的内容

-   `console.time`, `console.timeEnd`

    返回自开始计时后过去的时间

-   `console.trace`

    堆栈跟踪提供了程序逻辑中某点之前执行了哪些函数的信息。

    输出的堆栈跟踪如下例所示：

        Trace:
            at lastFunction (/Users/mike/tmp/app.js:12:11)
            at secondFunction (/Users/mike/tmp/app.js:8:3)
            at firstFunction (/Users/mike/tmp/app.js:4:3)
            at Object.<anonymous> (/Users/mike/tmp/app.js:15:3)

    注意,堆栈跟踪中的执行顺序是按时间倒序显示的。

-   使用 debug 管理调试输出

    <https://github.com/visionmedia/debug>

## node-debugger

-   官方

    <https://nodejs.org/api/debugger.html>

-   启动

    `node debug server.js`

-   断点

    `debugger;` 在程序中设置断点

    `setBreakpoint() (sb())` 在调试器中设置断点

    `clearBreakpoint() (cb())` 在调试器中取消断点

-   命令
    
    | 可选项 | 用途    | 
    |-------|------------| 
    | run   | 执行脚本,在第一行暂停| 
    | restart   | 重新执行脚本| 
    | cont, c   | 继续执行,直到遇到下一个断点| 
    | next, n   | 单步执行| 
    | step, s   | 单步执行并进入函数| 
    | out, o    | 从函数中步出| 
    | setBreakpoint(), sb() | 当前行设置断点| 
    | setBreakpoint(‘f()’), sb(...)| 在函数f的第一行设置断点| 
    | setBreakpoint(‘script.js’, 20), sb(...)| 在 script.js 的第20行设置断点| 
    | clearBreakpoint, cb(...)| 清除所有断点| 
    | backtrace, bt| 显示当前的调用栈| 
    | list(5)| 显示当前执行到的前后5行代码| 
    | watch(expr)| 把表达式 expr 加入监视列表| 
    | unwatch(expr)|  把表达式 expr 从监视列表移除 | 
    | watchers| 显示监视列表中所有的表达式和值| 
    | repl| 在当前上下文打开即时求值环境| 
    | kill| 终止当前执行的脚本| 
    | scripts| 显示当前已加载的所有脚本| 
    | version| 显示v8版本|

-   更多

    <http://i5ting.github.io/node-debug-tutorial/>

## node-inspector

-   官方

    <https://github.com/node-inspector/node-inspector>

-   安装

    `npm install -g node-inspector`

-   启动

    `node-debug app.js`

# 测试

# 知识点
## 关于 require 和同步I/O
require 是Node中少数几个同步I/O操作之一。因为经常用到模块,并且一般都是在文件
顶端引入,所以把 require 做成同步的有助于保持代码的整洁、有序,还能增强可读性。但在
程序中I/O密集的地方尽量不要用 require 。所有同步调用都会阻塞Node,直到调用完成才能
做其他事情。比如你正在运行一个HTTP服务器,如果在每个进入的请求上都用了 require ,
就会遇到性能问题。所以通常都只在程序最初加载时才使用 require 和其他同步操作。

## module.exports

    var Currency = function(canadianDollar) {
      this.canadianDollar = canadianDollar;
    }
    Currency.prototype.roundTwoDecimals = function(amount) {
      return Math.round(amount * 100) / 100;
    }
    Currency.prototype.canadianToUS = function(canadian) {
      return this.roundTwoDecimals(canadian * this.canadianDollar);
    }
    Currency.prototype.USToCanadian = function(us) {
      return this.roundTwoDecimals(us / this.canadianDollar);
    }
    module.exports = Currency;

## 异步编程技术
在Node的世界里流行两种响应逻辑管理方式:`回调`和`事件监听`。
- 回调

回调通常用来定义一次性响应的逻辑。

- 事件监听

事件监听器,本质上也是一个回调,不同的是,它跟一个概念实体(事件)相关联。用事件监听器响应重复性事件。
