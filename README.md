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

-   查看包

    `npm view`

-   安装包

    `npm install [-g]`

-   包文档

    `npm docs`

-   包源码

    `npm explore [-g]`

-   链接包

    `npm link`

-   取消链接包

    `npm unlink`

-   添加用户信息

    `npm adduser`

-   发布包

    `npm publish`

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

## 单元测试

1.  测试驱动开发(TDD)

    assert

    nodeunit

    Mocha

2.  行为驱动开发(BDD)

    Mocha

    Vows

    should.js

## 验收测试

   Tobi

   Soda


# 知识点

## 模块机制
-   module.exports

    ``` JAVASCRIPT
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
    ```

## 关于 require 和同步I/O
require 是Node中少数几个同步I/O操作之一。因为经常用到模块,并且一般都是在文件
顶端引入,所以把 require 做成同步的有助于保持代码的整洁、有序,还能增强可读性。

但在程序中I/O密集的地方尽量不要用 require 。所有同步调用都会阻塞Node,直到调用完成才能
做其他事情。比如你正在运行一个HTTP服务器,如果在每个进入的请求上都用了 require ,
就会遇到性能问题。所以通常都只在程序最初加载时才使用 require 和其他同步操作。

## 异步编程
-   简介

    在Node的世界里流行两种响应逻辑管理方式:`回调`和`事件监听`。

-   回调

    回调通常用来定义一次性响应的逻辑。

-   事件监听

    事件监听器,本质上也是一个回调,不同的是,它跟一个概念实体(事件)相关联。用事件监听器响应重复性事件。

## 数据流和管道
-   详细

    <https://github.com/substack/stream-handbook>

-   语法

    `ReadableStream.pipe(WritableStream);`

-   示例

    ``` JAVASCRIPT
    var readStream = fs.createReadStream('./original.txt')
    var writeStream = fs.createWriteStream('./copy.txt')
    readStream.pipe(writeStream);
    ```

## 流程控制
-   工具
    
    Nimble、Step、Seq

-   文章

    [虚拟座谈: 如何从JavaScript异步编程中活下来](http://mng.bz/wKnV)

## 利用多核的优势
-   简介

    现代的计算机CPU大多数都是多核的,但单个Node进程在运行时只能使用其中的一个内核。
    为了让单个程序使用多核实现起来更容易,Node增加了集群(cluster)API。

-   示例

    ``` JAVASCRIPT
    var cluster = require('cluster');
    var http = require('http');
    var numCPUs = require('os').cpus().length;
    var workers = {};
    var requests = 0;
    if (cluster.isMaster) {
      for (var i = 0; i < numCPUs; i++) {
        workers[i] = cluster.fork();
        (function (i) {
          workers[i].on('message', function(message) {
            if (message.cmd == 'incrementRequestTotal') {
              requests++;
              for (var j = 0; j < numCPUs; j++) {
                workers[j].send({
                  cmd:
                  'updateOfRequestTotal',
                  requests: requests
                });
              }
            }
          });
        })(i);
      }
      cluster.on('death', function(worker) {
        console.log('Worker ' + worker.pid + ' died.');
      });
    } else {
      process.on('message', function(message) {
        if (message.cmd == 'updateOfRequestTotal') {
          requests = message.requests;
        }
      });
      http.Server(function(req, res) {
        res.writeHead(200);
        res.end('Worker ID ' + process.env.NODE_WORKER_ID
        + ' says cluster has responded to ' + requests
        + ' requests.');
        process.send({cmd: 'incrementRequestTotal'});
      }).listen(8000);
    }
    ```

## HTTPS

-   简介
    
    安全的超文本传输协议，提供了一种保证 Web 会话私密性的方法。将 HTTP 和 TLS/SSL 传输层
    结合到一起

-   私钥和公钥（证书）

    私钥用来解密客户端发往服务器的数据

    公钥（证书）用来加密从客户端发往服务器的数据

-   生成

    生成私钥使用 OpenSSL： 

    `openssl genrsa 1024 > key.pem`

    生成公钥（证书）需要私钥：

    `openssl req -x509 -new -key key.pem > key-cert.pem`

-   应用

    ``` JAVASCRIPT
    var https = require('https');
    var fs = require('fs');
    var options = {
      key: fs.readFileSync('./key.pem'),
      cert: fs.readFileSync('./key-cert.pem')
    };
    https.createServer(options, function (req, res) {
      res.writeHead(200);
      res.end("hello world\n");
    }).listen(3000);
    ```

## 目录遍历攻击
<http://en.wikipedia.org/wiki/Directory_traversal_attack>

# 全局对象

## process
-   Exit Codes

    Node.js will normally exit with a 0 status code when no more async operations 
    are pending. 

-   Event

    `exit`: Emitted when the process is about to exit.

    `message`: Messages sent by `ChildProcess.send()`

    `beforeExit`

    `uncaughtException`

    `unhandledRejection`

    `rejectionHandled`

-   Signal Events

    Emitted when the processes receives a signal. 

    [a list of standard POSIX signal](http://wikipedia.org/wiki/Unix_signal#POSIX_sign)

    for example：

    An easy way to send the SIGINT signal is with Control-C in most terminal programs.

    ``` JAVASCRIPT
    // Start reading from stdin so we don't exit.
    process.stdin.resume();

    process.on('SIGINT', function() {
      console.log('Got SIGINT.  Press Control-D to exit.');
    });
    ```

## module

-   module.exports & exports

-   require

    when require() is called:

    ```
    require(X) from module at path Y
    1. If X is a core module,
       a. return the core module
       b. STOP
    2. If X begins with './' or '/' or '../'
       a. LOAD_AS_FILE(Y + X)
       b. LOAD_AS_DIRECTORY(Y + X)
    3. LOAD_NODE_MODULES(X, dirname(Y))
    4. THROW "not found"

    LOAD_AS_FILE(X)
    1. If X is a file, load X as JavaScript text.  STOP
    2. If X.js is a file, load X.js as JavaScript text.  STOP
    3. If X.json is a file, parse X.json to a JavaScript Object.  STOP
    4. If X.node is a file, load X.node as binary addon.  STOP

    LOAD_AS_DIRECTORY(X)
    1. If X/package.json is a file,
       a. Parse X/package.json, and look for "main" field.
       b. let M = X + (json main field)
       c. LOAD_AS_FILE(M)
    2. If X/index.js is a file, load X/index.js as JavaScript text.  STOP
    3. If X/index.json is a file, parse X/index.json to a JavaScript object. STOP
    4. If X/index.node is a file, load X/index.node as binary addon.  STOP

    LOAD_NODE_MODULES(X, START)
    1. let DIRS=NODE_MODULES_PATHS(START)
    2. for each DIR in DIRS:
       a. LOAD_AS_FILE(DIR/X)
       b. LOAD_AS_DIRECTORY(DIR/X)

    NODE_MODULES_PATHS(START)
    1. let PARTS = path split(START)
    2. let I = count of PARTS - 1
    3. let DIRS = []
    4. while I >= 0,
       a. if PARTS[I] = "node_modules" CONTINUE
       c. DIR = path join(PARTS[0 .. I] + "node_modules")
       b. DIRS = DIRS + DIR
       c. let I = I - 1
    5. return DIRS
    ```

# 核心模块
## child_process

Asynchronous Process Creation:

-   `child_process.exec(command[, options], callback)`

    用 cp.exec() 缓冲命令结果

    ``` JAVASCRIPT
    var exec = require('child_process').exec,
        child;

    child = exec('cat *.js bad_file | wc -l',
      function (error, stdout, stderr) {
        console.log('stdout: ' + stdout);
        console.log('stderr: ' + stderr);
        if (error !== null) {
          console.log('exec error: ' + error);
        }
    });
    ```

-   `child_process.spawn(command[, args][, options])`

    用 cp.spawn() 繁衍带有流接口的命令 

    这个函数跟 cp.exec() 不同，允许你跟每个子进程的 stdio 流交互

    ``` JAVASCRIPT
    var cp = require('child_process');
    var child = cp.spawn('ls', [ '-l' ]);

    // stdout is a regular Stream instance, which emits 'data','end', etc.
    child.stdout.pipe(fs.createWriteStream('ls-result.txt'));

    child.on('exit', function (code, signal) {
      // emitted when the child process exits
    });
    ```

-   `child_process.fork(modulePath[, args][, options])`

    用 cp.fork() 分散工作负载

    cp.fork() 提供了 child.send() 和 child.on('message') 来向子进程发送和接受消息。
    在子进程中,你可以用 process.send() 和 process.on('message') 向父进程发送和接受消息。

Synchronous Process Creation：

-   `child_process.spawnSync(command[, args][, options])`

-   `child_process.execSync(command[, options])`

# 第三方模块

## nimble
-   简介

    一个精简的流程控制工具

## formidable
-   简介

    用于媒体上传和转换

-   计算上传进度

    formidable 的 process 事件能给出收到的字节数，以及期望收到的字节数。

    可以这样计算百分比，做出一个进度条

    ``` JAVASCRIPT
    form.on('progress', function(bytesReceived, bytesExpected){
      var percent = Math.floor(bytesReceived / bytesExpected * 100);
      console.log(percent);
    });
    ```

## node-mysql
-   主页

    <https://github.com/felixge/node-mysql>

-   简介

    让 Node 能跟 Mysql 交互

## node-postgres
-   主页

    <https://github.com/brianc/node-Postgres>

-   简介

    最成熟也是最活跃的 PostgreSQL 数据库 API 模块

## node_redis
-   主页

    <https://github.com/mranney/node_redis>

-   redis 教程

    [redis快速教程](http://redis.io/topics/quickstart)
 
    [尝试Redis](http://try.redis.io/)

    [Redis in Action](#)

## hiredis
-   主页

    <https://github.com/pietern/hiredis-node>

-   简介

    这个模块会显著提升 Redis 的性能

    如果你装了 hiredis ，node-redis API 会自动使用 hiredis 替代它的 JavaScript 实现

## node-mongodb-native
-   主页

    <https://github.com/mongodb/node-mongodb-native>

-   简介

    最成熟、维护最活跃的 MongooseDB API 模块

## mongoose

-   主页

    <http://mongoosejs.com>

-   简介

    Mongoose 的模型提供了一个到 MongoDB 集合接口。

## forever

-   主页

    <https://github.com/nodejitsu/forever>

-   简介

    能在程序崩溃退出后还能重启它。

## debug

-   主页

    <https://github.com/visionmedia/debug>

-   简介

    调试模式

## fstream

-   主页

    <https://github.com/isaacs/fstream>

-   简介

    fs 模块扩展

## filed

-   主页

    <https://github.com/mikeeal/filed>

-   简介

    fs 模块扩展

## node-tar

-   主页

    <https://github.com/isaacs/node-tar>

-   简介

    node 版本的 tar

## gm

-   主页

    <http://aheckmann.github.com/gm/>

-   简介

    用强大的 GraphicsMagick 和 ImageMagick 库在 Node 程序中执行各种图片的处理和转换操作

## node-cgi

-   主页

    <https://github.com/ToolTallNate/node-cgi>

-   简介

    将 cp.spawn() 的使用抽象成实用功能的优秀范例模块

## commander.js
    
-   简介

    命令行工具封装模块

-   相关模块

    nopt, optimist, nomnom

## ansi.js

-   简介

    命令行彩色输出

-   相关模块 

    colors.js, clicolor, ansi.js

# 专业术语
## DIRT(data-intensive real-time)
-   简介

    数据密集型实时程序

-   示例： Browserling(<browserling.com>)

    一个用Node开发的DIRT程序。在这个网站上,可以在浏览器中使用各种浏览器。
    Browserling用了一个叫做StackVM的由Node驱动的项目,
    而StackVM管理了用QEMU(快速模拟器)模拟器创建的虚拟机,
    QEMU会模拟运行浏览器所需的CPU和外设。

-   示例： Testling(<testling.com>)

    可以通过命令行在多个浏览器上并行运行测试包。

## REPL（Read-Eval-Print-Loop）

    一种交互式计算机编程环境

## MIME
-   维基百科

    <http://en.wikipedia.org/wiki/MIME> 

-   简介

    通过HTTP提供文件时，要用正确的MIME类型设置HTTP头的 Content-Type 。

-   Node模块： mime

## WebSocket
-   维基百科 

    <http://en.wikipedia.org/wiki/WebSocket>

-   简介

    一个为支持实时通讯而设计的轻量的双向通信协议。

-   Node模块： socket.io

# 开源项目

## javascript

-   详细
  
    <https://github.com/jashkenas/coffee-script/wiki/List-of-languages-that-compile-to-JS>

## jslinux
-   官网 

    http://bellard.org/jslinux/

-   简介

    一个运行在 Javascript 中的 PC 模拟器
