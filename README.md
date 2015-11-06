# 安装

## node

-   使用 Homebrew 安装 node （OS X）
    
    ```
    ruby -e "$(curl -fsSkL raw.github.com/mxcl/homebrew/go)"
    brew install node
    ```

-   使用 nvm 安装 node  

    ```
    wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.27.0/install.sh | bash
    nvm install 0.10.38
    nvm use 0.10.38 --default
    ```

-   源码编译

    ```
    sudo apt-get install build-essential libssl-dev

    curl -O http://nodejs.org/dist/node-latest.tar.gz
    tar zxvf node-latest.tar.gz
    cd node-v*
    ./configure
    make
    sudo make install
    node -v
    ```

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

-   添加用户信息

    `npm adduser`

-   链接包

    `npm link`

-   取消链接包

    `npm unlink`

-   发布包

    `npm publish`

-   取消发布包

    `npm unpublish`

# 调试

## 代码检查

-   `JSLint`
    
    JSLint是一个JavaScript验证工具（非开源），可以扫描JavaScript源代码来查找问题。

-   `JSHint`

    JSHint是基于JSLint的项目,JSLint是一个存在了十多年的JavaScript源码分析工具。然而
    JSLint的可配置性不太强,因此促生了JSHint。

    <https://github.com/jshint/jshint>

    <https://github.com/jshint/node-jshint>

    ```    
    npm install -g jshint
    jshint my_app.js
    ```

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

    ```
    Trace:
        at lastFunction (/Users/mike/tmp/app.js:12:11)
        at secondFunction (/Users/mike/tmp/app.js:8:3)
        at firstFunction (/Users/mike/tmp/app.js:4:3)
        at Object.<anonymous> (/Users/mike/tmp/app.js:15:3)
    ```

    注意,堆栈跟踪中的执行顺序是按时间倒序显示的。

-   使用 debug 管理调试输出

    <https://github.com/visionmedia/debug>

## chrome-inspect

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
    
    | 可选项                                     | 用途                      | 
    |-------------------------------------------|--------------------------| 
    | run                                       | 执行脚本,在第一行暂停        | 
    | restart                                   | 重新执行脚本               | 
    | cont, c                                   | 继续执行,直到遇到下一个断点   | 
    | next, n                                   | 单步执行                   | 
    | step, s                                   | 单步执行并进入函数          | 
    | out, o                                    | 从函数中步出               | 
    | setBreakpoint(), sb()                     | 当前行设置断点              | 
    | setBreakpoint(‘f()’), sb(...)             | 在函数f的第一行设置断点       | 
    | setBreakpoint(‘script.js’, 20), sb(...)   | 在 script.js 的第20行设置断点| 
    | clearBreakpoint, cb(...)                  | 清除所有断点                | 
    | backtrace, bt                             | 显示当前的调用栈             | 
    | list(5)                                   | 显示当前执行到的前后5行代码    | 
    | watch(expr)                               | 把表达式 expr 加入监视列表    | 
    | unwatch(expr)                             |  把表达式 expr 从监视列表移除 | 
    | watchers                                  | 显示监视列表中所有的表达式和值 | 
    | repl                                      | 在当前上下文打开即时求值环境   | 
    | kill                                      | 终止当前执行的脚本           | 
    | scripts                                   | 显示当前已加载的所有脚本      | 
    | version                                   | 显示v8版本                 |

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

-   测试驱动开发(TDD)

    assert

    nodeunit

    Mocha

-   行为驱动开发(BDD)

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

-   目录遍历攻击

    <http://en.wikipedia.org/wiki/Directory_traversal_attack>

# 专业术语

## common.js

## DIRT

-   简介

    (data-intensive real-time)

    数据密集型实时程序

-   示例： Browserling(<browserling.com>)

    一个用Node开发的DIRT程序。在这个网站上,可以在浏览器中使用各种浏览器。
    Browserling用了一个叫做StackVM的由Node驱动的项目,
    而StackVM管理了用QEMU(快速模拟器)模拟器创建的虚拟机,
    QEMU会模拟运行浏览器所需的CPU和外设。

-   示例： Testling(<testling.com>)

    可以通过命令行在多个浏览器上并行运行测试包。

## REPL

-   简介

    （Read-Eval-Print-Loop）

    一种交互式计算机编程环境

## Promise

-   参考资料：

    <http://nodeonly.com/nodesang/#/5>

    <https://github.com/promises-aplus/promises-spec>

    <https://github.com/petkaantonov/bluebird>

    <http://www.cnblogs.com/1000/p/getting-started-with-promises.html>

    <http://www.cnblogs.com/1000/p/3847745.html>


-   初识Promises

    Promises是什么:

    Promises象征着一个异步操作的最终结果。Promises交互主要通过它的then方法，
    then方法接受一个回调函数，这个回调函数接受执行成功的返回值或执行失败的错误原因，
    错误原因一般是Error对象。需要注意的是，then方法执行的返回值是一个Promise对象，
    而then方法接受的回调函数的返回值则可以是任意的JavaScript对象，包括Promises。
    基于这种机制，Promise对象的链式调用就起作用了。

    Promises的状态:

    Promise对象有三种状态：pending（初始状态）、fulfilled（成功执行）、rejected（执行出错）。
    pending状态的Promise对象可以转换到其它两种状态。

-   使用Promise进行错误处理

    异步模式中的错误处理:

    ```javascript
    fs.readFile('file.json', 'utf8', function(err, data){
        if(err){
            console.error("无法读取文件")
        }else{
            try{
                var json = JSON.parese(data)
            }catch(e){
                console.error("不符合json格式");
            }
        }
    })
    ```

    假设fs.readFileAsync是fs.readFile的Promise版本，这意味着：

    fs.readFileAsync方法的返回结果是一个Promise对象
    fs.readFileAsync方法的返回结果拥有一个then方法
    fs.readFileAsync方法接受参数与fs.readFile一致，除了最后一个回调函数

    返回Promise对象意味着，执行fs.readFileAsync并不会立即执行异步操作，
    而是通过调用其then方法来执行，then方法接受的回调函数用于处理正确返回结果。
    所以使用fs.readFileAsync的使用方式如下：

    ```
    //Promise版本
    fs.readFileAsync('file.json', 'utf8')
    .then(function(data){
      console.log(data)
    })
    ```

    由于Promises/A+标准对Promise对象只规定了唯一的then方法，没有专门
    针对catch或者error的方法，我们将继续使用bluebird。

    ```javascript
    // 带错误处理的Promise版本
    fs.readFileAsync('file.json', 'utf8')
    .then(function(data){
      console.log(data)
    })
    .catch(SyntaxError, function(e){
      //code here
    })
    .catch(function(e){
      //code here
    })
    ```

-   Promisify

    使用bluebird如何对fs.readFileAsync方法进行promisify：

    ```javascript
    var Promise = require('bluebird')
    fs.readFileAsync = Promise.promisify(fs.readFie, fs)
    ```

    对于bluebird它还有一个更强大的方法，那就是promisify的高级版本 promisifyAll，比如：

    ```javascript
    var Promise = require('bluebird')
    Promise.promisifyAll(fs)
    ```

    行完上面的代码之后，fs对象下所有的异步方法都会对应的生成一个Promise版本方法，
    比如fs.readFile对应fs.readFileAsync，fs.mkdir对应fs.mkdirAsync，以此类推。

    另外要注意的就是，Promise版本的函数除了最后一个参数（回调函数），
    其它参数与原函数均一一对应，调用的时候别忘了传递原有的参数。

    注：如果你正在使用mongoose，除了bluebird你可能还需要mongoomise，它的优点在于：

    *   能够接受任意的Promise Library (Q/when.js/RSVP/bluebird/es6-promise等等)
    *   能够对Model自定义静态私有方法进行promisify，而bluebird.promisifyAll不支持
    *   mongoomise + bluebird与仅使用bluebird性能相差无几，可能更好。

-   resolve 和 reject

    ```
    return Promise.resolve(result);
    ```

    ```
    return Promise.reject(err);
    ```

-   Promise.all()
    
    ```
    ...
    .then(function(sendReq){
        ...
        var queue = [];
        ...
        for(var i = 0; i < items.length; i++){
          ...
          var p = StockInfo.update({product:product_id}, {$set:{
            ...
          }})

          queue.push(p);
        }
        return Promise.all(queue);
    })
    ...
    ```

-   node 中的 promise 实现

    - bluebird （<https://github.com/petkaantonov/bluebird>）
    - q （<https://github.com/kriskowal/q>）Angularjs的$q对象是q的精简版
    - then （<https://github.com/teambition/then.js>）
    - when  （<https://github.com/cujojs/when>）
    - async  （<https://github.com/caolan/async>）
    - eventproxy（<https://github.com/JacksonTian/eventproxy>）朴灵作品 使用event来处理流程

-   总结

    node.js风格函数指的是这样的一种异步函数，它接受的最后一个参数是异步操作完成之后的回调函数，
    这个回调函数的第一个参数接受执行错误的Error对象，第二个参数接受成功返回值）。

    promisify大概的意思就是根据一个node.js风格的异步方法生成另一个等价的Promise风格的
    方法（这个方法返回值是一个Promise，其它形参与原方法相同除了没有最后一个回调函数），
    这个名词我最早是看到bluebird使用。

## RESTful

-   参考资料

    <http://www.ruanyifeng.com/blog/2011/09/restful>

    <http://www.csdn.net/article/2013-06-13/2815744-RESTful-API>

-   REST

    REST（Representational State Transfer）：表现层状态转化

    REST 是一种软件架构风格，设计风格而不是标准，只是提供了一组设计原则和约束条件。
    它主要用于客户端和服务器交互类的软件。基于这个风格设计的软件可以更简洁，
    更有层次，更易于实现缓存等机制。

    RESTful架构：

    1.  每一个URI代表一种资源；
    2.  客户端和服务器之间，传递这种资源的某种表现层；
    3.  客户端通过四个HTTP动词，对服务器端资源进行操作，实现"表现层状态转化"。

-   资源（Resources）

    REST的名称"表现层状态转化"中，省略了主语。"表现层"其实指的是"资源"的"表现层"。

    "资源"，就是网络上的一个实体，它可以是一段文本、一张图片、一首歌曲、一种服务，
    可以用一个URI（统一资源定位符）指向它，每种资源对应一个特定的URI。

-   表现层（Representation）

    "资源"是一种信息实体，它可以有多种外在表现形式。

    我们把"资源"具体呈现出来的形式，叫做它的"表现层"

    比如，文本可以用txt格式表现，也可以用HTML格式、XML格式、JSON格式表现，甚至可以采用二进制格式；
    图片可以用JPG格式表现，也可以用PNG格式表现。。

    URI只代表资源的实体，不代表它的形式。严格地说，有些网址最后的".html"后缀名是不必要的，
    因为这个后缀名表示格式，属于"表现层"范畴，而URI应该只代表"资源"的位置。

-   状态转化（State Transfer）

    如果客户端想要操作服务器，必须通过某种手段，让服务器端发生"状态转化"（State Transfer）。
    而这种转化是建立在表现层之上的，所以就是"表现层状态转化"。

    四种基本操作：GET用来获取资源，POST用来新建资源（也可以用于更新资源），
    PUT用来更新资源，DELETE用来删除资源

-   实现

    1.  因为"资源"表示一种实体，所以应该是名词，URI不应该有动词
        
        如何拆分出这些资源：

            GET     /tickets        # 获取ticket列表
            GET     /tickets/12     # 查看某个具体的ticket
            POST    /tickets        # 新建一个ticket
            PUT     /tickets/12     # 更新ticket 12.
            DELETE  /tickets/12     # 删除ticekt 12
        
        如何处理关联？
        
            GET     /tickets/12/messages    - Retrieves list of messages for ticket #12
            GET     /tickets/12/messages/5  - Retrieves message #5 for ticket #12
            POST    /tickets/12/messages    - Creates a new message in ticket #12
            PUT     /tickets/12/messages/5  - Updates message #5 for ticket #12
            PATCH   /tickets/12/messages/5  - Partially updates message #5 for ticket #12
            DELETE  /tickets/12/messages/5  - Deletes message #5 for ticket #12
    2.  更新和创建操作应该返回资源

        PUT、POST、PATCH 操作在对资源进行操作的时候常常有一些副作用：例如created_at,updated_at 时间戳。
        为了防止用户多次的API调用（为了进行此次的更新操作），我们应该会返回更新的资源（updated representation.）
        例如：在POST操作以后，返回201 created 状态码，并且包含一个指向新资源的url作为返回头.

    2.  版本信息放入url还是放入请求头

        strip使用的方法就很好：它的url里面有主版本信息，同时请求头俩面有子版本信息。
        这样在子版本变化过程中url的稳定的。变化有时是不可避免的，关键是如何管理变化。
        完整的文档和合理的时间表都会使得API使用者使用的更加轻松。

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

# 开源项目

## javascript

-   详细
  
    <https://github.com/jashkenas/coffee-script/wiki/List-of-languages-that-compile-to-JS>

## jslinux
-   官网 

    http://bellard.org/jslinux/

-   简介

    一个运行在 Javascript 中的 PC 模拟器