# 基础

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

-   简介
    
    NPM的全称是Node Package Manager，是一个NodeJS包管理和分发工具，已经成为了非官方的发
    布Node模块（包）的标准。

-   配置文件

    `package.json`

-   常用命令
    
    ```
    npm search                      寻找包
    npm view                        查看包
    npm install [-g]                安装包
    npm docs                        包文档
    npm explore [-g]                包源码
    npm adduser                     添加用户信息
    npm link                        链接包
    npm unlink                      取消链接包
    npm publish                     发布包
    npm unpublish                   取消发布包
    ```

## Bower

-   简介

    Bower是一个客户端技术的软件包管理器，它可用于搜索、安装和卸载如JavaScript、HTML、CSS之类
    的网络资源。其他一些建立在Bower基础之上的开发工具，如YeoMan和Grunt。

-   安装

    `npm install -g bower`

-   配置文件

    `bower.json`

-   常用命令

    ```
    bower init                      创建bower.json文件
    bower install [--save]          包的安装
    bower list                      所有包的列表
    bower search                    包的搜索
    bower info                      特定的包的信息
    bower uninstall                 包的卸载
    ```

## grunt

-   简介

    Grunt是基于Node.js的项目构建工具。它可以自动运行你所设定的任务。

-   安装

    `npm install -g grunt-cli`

-   配置文件

    `Gruntfile.js` `package.json`

## gulp

-   简介

    Gulp.js 是一个自动化构建工具,开发者可以使用它在项目开发过程中自动执行常见任务。

-   安装

    `npm install -g gulp`

-   配置文件

    `gulpfile.js`

## yeoman

-   简介

    Yeoman是Google的团队和外部贡献者团队合作开发的，他的目标是通过Grunt（一个用于开发任务自动
    化的命令行工具）和Bower（一个HTML、CSS、Javascript和图片等前端资源的包管理器）的包装为
    开发者创建一个易用的工作流。

    Yeoman的目的不仅是要为新项目建立工作流，同时还是为了解决前端开发所面临的诸多严重问题，例如
    零散的依赖关系。

    Yeoman主要有三部分组成：yo（脚手架工具）、grunt（构建工具）、bower（包管理器）。这三个工
    具是分别独立开发的，但是需要配合使用，来实现我们高效的工作流模式。

-   官网

    <https://github.com/yeoman/yo>

## pm2
-   简介

    pm2 是一个带有负载均衡功能的Node应用的进程管理器.

-   详细

    <http://www.oschina.net/translate/goodbye-node-forever-hello-pm2?cmp>

-   安装

    `npm install -g pm2`

-   常用命令

    ```
    pm2 start <app_name|id|all>     启动程序
    pm2 list                        列举进程
    pm2 stop <app_name|id|all>      退出程序
    pm2 restart                     重启应用
    pm2 describe id|all             程序信息
    pm2 monit                       监控
    pm2 logs                        实时集中log处理
    pm2 web                         API(端口：9615 ) 
    ```

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

## node-debugger

-   官方

    <https://nodejs.org/api/debugger.html>

-   启动

    `node debug server.js`

-   断点

    `debugger;` 在程序中设置断点

    `setBreakpoint() (sb())` 在调试器中设置断点

    `clearBreakpoint() (cb())` 在调试器中取消断点

-   更多

    <http://i5ting.github.io/node-debug-tutorial/>

## node-inspector

-   官方

    <https://github.com/node-inspector/node-inspector>

-   安装

    `npm install -g node-inspector`

-   启动

    `node-debug app.js`

## chrome-inspect

# 测试

## 概述

-   分类

    软件开发测试分类：

    <http://www.douban.com/note/89359502/>

    Node.js 测试相关：

    <https://github.com/nodejs/node-v0.x-archive/wiki/modules#testing>

    单元测试：

    ```
    测试驱动开发(TDD)： assert, nodeunit, Mocha, chai
    行为驱动开发(BDD)： Mocha, chai, Vows, should.js
    ```

    测试覆盖率:
    ```
    istanbul
    ```

## mocha

# 全局对象和核心模块

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

## child_process

-   Asynchronous Process Creation:

    用 cp.exec() 缓冲命令结果: `child_process.exec(command[, options], callback)`

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

    用 cp.spawn() 繁衍带有流接口的命令: `child_process.spawn(command[, args][, options])`

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

    用 cp.fork() 分散工作负载: `child_process.fork(modulePath[, args][, options])`

    cp.fork() 提供了 child.send() 和 child.on('message') 来向子进程发送和接受消息。
    在子进程中,你可以用 process.send() 和 process.on('message') 向父进程发送和接受消息。

-   Synchronous Process Creation：

    `child_process.spawnSync(command[, args][, options])`

    `child_process.execSync(command[, options])`

-   child-process-promise

    <https://github.com/patrick-steele-idem/child-process-promise>

# 知识点

## 异步编程

-   简介

    在Node的世界里流行两种响应逻辑管理方式:`回调`和`事件监听`。

-   回调

    回调通常用来定义一次性响应的逻辑。

-   事件监听

    事件监听器,本质上也是一个回调,不同的是,它跟一个概念实体(事件)相关联。用事件监听器响应重复性事件。

-   关于 require 和同步I/O

    require 是Node中少数几个同步I/O操作之一。因为经常用到模块,并且一般都是在文件
    顶端引入,所以把 require 做成同步的有助于保持代码的整洁、有序,还能增强可读性。

    但在程序中I/O密集的地方尽量不要用 require 。所有同步调用都会阻塞Node,直到调用完成才能
    做其他事情。比如你正在运行一个HTTP服务器,如果在每个进入的请求上都用了 require ,
    就会遇到性能问题。所以通常都只在程序最初加载时才使用 require 和其他同步操作。


-   when require() is called

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


## COOKIE

-   基础

    在HTML文档被发送之前，Web服务器通过传送HTTP 包头中的Set-Cookie 消息把一个cookie 发送到用户的浏览器中，如下示例：

    ```
    Set-Cookie: name=value; Path=/; expires=Wednesday, 09-Nov-99 23:12:40 GMT;
    ```

    其中比较重要的属性：

    ```
    name=value：键值对，可以设置要保存的 Key/Value，注意这里的 name 不能和其他属性项的名字一样
    Expires： 过期时间（秒），在设置的某个时间点后该 Cookie 就会失效，如 expires=Wednesday, 09-Nov-99 23:12:40 GMT
    maxAge： 最大失效时间（毫秒），设置在多少后失效
    secure： 当 secure 值为 true 时，cookie 在 HTTP 中是无效，在 HTTPS 中才有效
    Path： 表示 cookie 影响到的路径，如 path=/。如果路径不能匹配时，浏览器则不发送这个Cookie
    httpOnly: 是微软对COOKIE做的扩展。如果在COOKIE中设置了“httpOnly”属性，则通过程序（JS脚本、applet等）将无法读取到COOKIE信息，防止XSS攻击产生
    ```

-   node.js 中的 cookie

    两个方案：

    1.使用 `response.writeHead`

    缺点：使用response.writeHead只能发送一次头部，即只能调用一次，且不能与response.render共存，否则会报错。

    ```javascript
    //设置过期时间为一分钟
    var today = new Date();
    var time = today.getTime() + 60*1000;
    var time2 = new Date(time);
    var timeObj = time2.toGMTString();
    response.writeHead({
       'Set-Cookie':'myCookie="type=ninja", "language=javascript";path="/";Expires='+timeObj+';httpOnly=true'
    });
    ```

    2.使用 `response.cookie`

    语法: `response.cookie('cookieName', 'name=value[name=value...]',[options]);`

    ```javascript
    response.cookie('haha', 'name1=value1&name2=value2', {maxAge:10*1000, path:'/', httpOnly:true});
    ```

-   cookieParser

    express 在 4.x 版本之后，管理session和cookies等许多模块都不再直接包含在express中， 而是需要单独下载安装相应模块。

    `$ npm install cookie-parser`

    使用示例：

    ```javascript
    var express      = require('express');
    var cookieParser = require('cookie-parser');
     
    var app = express();
    app.use(cookieParser());
     
    app.get('/', function (req, res) {
        // 如果请求中的 cookie 存在 isVisit, 则输出 cookie
        // 否则，设置 cookie 字段 isVisit, 并设置过期时间为1分钟
        if (req.cookies.isVisit) {
            console.log(req.cookies);
            res.send("再次欢迎访问");
        } else {
            res.cookie('isVisit', 1, {maxAge: 60 * 1000});
            res.send("欢迎第一次访问");
        }
    });
    app.listen(80);
    ```

## SESSION

-   简介

    session是另一种记录客户状态的机制，不同的是Cookie保存在客户端浏览器中，而session保存在服务器上。

-   区别

    cookie 和 session 的区别：

    cookie数据存放在客户的浏览器上，session数据放在服务器上。

    cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗 考虑到安全应当使用session。

    session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能 考虑到减轻服务器性能方面，应当使用COOKIE。

    单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。

    所以建议：将登陆信息等重要信息存放为session、其他信息如果需要保留，可以放在cookie中

-   express-session

    安装：　`$ npm install express-session`

    方法： `session(options)`，其中 options 中包含可选参数，主要有：

    ```
    name: 设置 cookie 中，保存 session 的字段名称，默认为 connect.sid 。
    store: session 的存储方式，默认存放在内存中，也可以使用 redis，mongodb 等。express 生态中都有相应模块的支持。
    secret: 通过设置的 secret 字符串，来计算 hash 值并放在 cookie 中，使产生的 signedCookie 防篡改。
    cookie: 设置存放 session id 的 cookie 的相关选项，默认为 (default: { path: '/', httpOnly: true, secure: false, maxAge: null })
    genid: 产生一个新的 session_id 时，所使用的函数， 默认使用 uid2 这个 npm 包。
    rolling: 每个请求都重新设置一个 cookie，默认为 false。
    resave: 即使 session 没有被修改，也保存 session 值，默认为 true。
    ```
    ```javascript
    var express = require('express');
    var session = require('express-session');
    var app = express();
     
    app.use(session({
        secret: 'hello', //secret的值建议使用128个随机字符串
        cookie: {maxAge: 60 * 1000 * 30} // 过期时间（毫秒）
    }));
    app.get('/', function (req, res) {
        if (req.session.sign) {//检查用户是否已经登录
            console.log(req.session);//打印session的值
            res.send('welecome <strong>' + req.session.name + '</strong>, 欢迎你再次登录');
        } else {
            req.session.sign = true;
            req.session.name = 'Tom';
            res.send('欢迎登陆！');
        }
    });
    app.listen(80);
    ```

-   基于 Redis 管理 Session

    安装 

    ```
    $ npm install connect-redis
    ```

    参数

    ```
    client 你可以复用现有的redis客户端对象， 由 redis.createClient() 创建
    host Redis服务器名
    port Redis服务器端口
    socket Redis服务器的unix_socket
    ```

    可选参数

    ```
    ttl Redis session TTL 过期时间 （秒）
    disableTTL 禁用设置的 TTL
    db 使用第几个数据库
    pass Redis数据库的密码
    prefix 数据表前辍即schema, 默认为 "sess:"
    ```

    req在经过session中间件的时候就会自动完成session的有效性验证、延期/重新颁发、以及对session中数据的获取了。

    ```javascript
    var express = require('express');
    var session = require('express-session');
    var RedisStore = require('connect-redis')(session);
     
    var app = express();
    var options = {
        "host": "127.0.0.1",
        "port": "6379",
        "ttl": 60 * 60 * 24 * 30,   //session的有效期为30天(秒)
    };
     
    // 此时req对象还没有session这个属性
    app.use(session({
        store: new RedisStore(options),
        secret: 'express is powerful'
    }));
     
    app.listen(80);
    ```

## 加密密码

-   bcrypt

    bcrypt 是一个加盐的哈希函数，是专门用来对密码做哈希处理的第三方模块。

    ```javascript
    User.prototype.hashPassword = function (fn) {
      var user = this;
      bcrypt.genSalt(12, function (err, salt) {
        if (err) return fn(err);
        user.salt = salt;
        bcrypt.hash(user.pass, salt, function (err, hash) {
          if (err) return fn(err);
          user.pass = hash;
          fn();
        })
      })
    }
    ```
    ```javascript
    User.prototype.authenticate = function (name, pass, fn) {
      User.getByName(name, function (err, user) {
        if (err) return fn(err);
        if (!user.id) return fn();
        bcrypt.hash(pass, user.salt, function (err, hash) {
          if (err) return fn(err);
          if (hash === user.pass) return fn(null, user);
          fn();
        })
      })
    }
    ```

## 命令行工具

-   创建 package.json

    `npm init`

    ```
    {
      "name": "node-command-line-tool",
      "version": "1.0.0",
      "description": "To make a node command line tool",
      "main": "index.js",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "preferGlobal": "true",
      "bin": {
        "hit": "bin/hit.js"
      },
      "keywords": [
        "command",
        "line"
      ],
      "author": "modood",
      "license": "ISC"
    }
    ```

-   编写脚本代码

    `npm install commander --save`
    
    创建 bin/hit.js 文件：

    ```javascript
    #!/usr/bin/env node
    
    var program = require('commander');
    
    program
      .version('0.0.1')
      .option('-p, --print', 'print Hello World')
      .option('-s, --show', 'show github page')
      .parse(process.argv);
    
    if (program.print) {
      console.log('Hello World');
    };
    
    if (program.show) {
      console.log('https://github.com/modood');
    };
    
    console.log('wow! you made it!');
    ```

-   完成

    `sudo npm link`

    本地创建链接文件测试效果

    ```
    $ hit -h
    
      Usage: hit [options]
    
      Options:
    
        -h, --help     output usage information
        -V, --version  output the version number
        -p, --print    print Hello World
        -s, --show     show github page
    ```

## 中间件机制

-   简介

    在 Connect 中，中间件组件是一个 JavaScript 函数，它拦截 HTTP 服务器提供的请求和响应对象
    按惯例会接受三个参数：一个请求对象，一个响应对象，还有一个通常命名为 next 的参数，它是一个回
    调函数，表明这个组件已经完成了它的工作，可以执行下一个中间件组件了。

-   注意

    如果 next 不调用，控制权就不会被交回到分派器去调用下一个中间件组件，命令链中的后续中间件都不
    会被调用，因此中间件的顺序也很重要。

-   挂载

    挂载可以给中间件或整个程序定义一个路径前缀。

    ```javascript
    connect()
      .use(logger)
      .use('/admin', restrict)
      .listen(3000);
    ```

-   创建可配置的中间件

    可配置的中间件可以传入额外的参数来改变它的行为

    例如：可配置的 Connect 中间件组件 logger

    ```javascript
    function logger(format) {
      var regexp = /:(\w+)/g;
      return function (req, res, next) {
        var str = format.replace(regexp, function(match, property){
          return req[property];
        });
        console.log(str);
        next();
      }
    }
    module.exports = logger;
    ```
    ```
    connect()
      .use(logger(':method:url'))
    ```

-   错误处理中间件

    错误处理中间件函数必须接受四个参数：err, req, res, next

    ```javascript
    function errorHandler() {
      var env = process.env.NODE_ENV || 'development';
      return function(err, req, res, next) {
        res.statusCode = 500;
        switch (env) {
          case 'development':
            res.setHeader('Content-Type', 'application/json');
            res.end(JSON.stringify(err));
            break;
          default:
            res.end('Server error');
        }
      }
    }
    ```

## nginx

-   简介

    尽管Node在提供动态内容服务时很高效,但在提供图片、 CSS样式表或客户端JavaScript等静
    态文件服务时并不是最有效的办法。

    通过HTTP提供静态文件的服务应该交给专门针对这个特定任务优化过的特定软件项目,
    因为它们多年以来主要专注于这项任务。

    Nginx (http://nginx.org/en/) 是一个专门针对静态文件服务做过优化的开源Web服务器,很容
    易设置成跟Node一起提供那些文件服务。在典型的Nginx/Node配置中,一般由Nginx先处理所有
    Web请求,再将非静态文件的请求转给Node。

-   安装

    `sudo apt-get install nginx`

-   配置文件

    `/etc/nginx/nginx.conf`

-   配置选项

    ```
    http {
      upstream my_node_app {
        server 127.0.0.1:8000;
      }
      server {
        listen 80;
        server_name localhost domain.com;
        access_log /var/log/nginx/my_node_app.log;
        location ~ /static/ {
          root /home/node/my_node_app;
          if (!-f $request_filename) {
            return 404;
          }
        }
        location / {
          proxy_pass http://my_node_app;
          proxy_redirect off;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
          proxy_set_header Host $http_host;
          proxy_set_header X-NginX-Proxy true;
        }
      }
    }
    ```

# 专业术语

## CommonJS

-   简介

    CommonJS是一种规范，NodeJS是这种规范的实现

-   官网

    <http://www.commonjs.org/>

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
