# PHP目前比较常见的四种大运行模式

1. CGI（通用网关接口 / Common Gateway Interface）
2. FastCGI（常驻型CGI / Long-Live CGI）
3. CLI（命令行运行 / Command Line Interface）
4. Web模块模式（Apache等Web服务器运行的模式）

## CGI

CGI即通用网关接口（Common Gateway Interface），它是一段程序，通俗的讲CGI就象是一座桥，把网页和Web服务器中的执行程序连接起来，它把HTML接收的指令传递给服务器的执行程序，再把服务器执行程序的结果返还给HTML页。CGI 的跨平台性能极佳，几乎可以在任何操作系统上实现。`CGI已经是比较老的模式了，这几年都很少用了。`

###优点

 1. CGI 的跨平台性能极佳，几乎可以在任何操作系统上实现。
 2. Web Server和具体的程序处理独立开来，结构清晰，可控性强。

###缺点

 1. 在高访问需求的情况下，CGI的进程Fork就会成为很大的服务器负担，想 象一下数百个并发请求导致服务器Fork出数百个进程就明白了。这也是为什么CGI一直背负性能低下，高资源消耗的恶名的原因。
 2. php-cgi变更php.ini配置后需重启php-cgi才能让新的php-ini生效，不可以平滑重启。
 3. 直接杀死php-cgi进程,php就不能运行了。(PHP-FPM守护进程会平滑从新生成新的子进程。）

## FastCGI

FastCGI是CGI的升级版本，FastCGI像是一个常驻 (long-live)型的 CGI，它可以一直执行着，只要激活后，不会每次都要花费时间去 Fork 一次 （这是 CGI 最为人诟病的 fork-and-execute 模式）。

FastCGI是一个可伸缩地、高速地在HTTP server和动态脚本语言间通信的接口。多数流行的HTTP server都支持FastCGI，包括Apache、Nginx和lighttpd等，同时，FastCGI也被许多脚本语言所支持，其中就有PHP。

`php-cgi是被调用的进程，php-fpm是配置和管理进程的。`

`PHP的FastCGI进程管理器是PHP-FPM（PHP-FastCGI Process Manager）`

###优点

 1. 稳定性好，FastCGI是以独立的进程池来运行CGI，单独一个进程死掉，系统可以很轻易的丢弃，然后重新分配新的进程来运行逻辑；
 2. 安全性好，FastCGI支持分布式运算。FastCGI和宿主的Server完全独立，FastCGI怎么down也不会把Server搞垮；
 3. 性能好，FastCGI把动态逻辑的处理从Server中分离出来，大负荷的IO处理还是留给宿主Server，这样宿主Server可以一心一意作IO，对于一个普通的动态网页来说, 逻辑处理可能只有一小部分，大量的是图片等静态。
 4. PHP脚本解析更快。php解析程序被载入内存而不用每次需要时从存储器读取。
 5. 需要使用的系统资源更少，由于服务器不用每次需要时载入php解析程序，你可以将站点的传输速度提升很多，而必增加cpu负担。
 6. 不用对现有的代码做任何修改。运行在apache+php上程序，无须修改即可适用于php的FastCGI。


###缺点

 1. FastCGI模式更适合生产环境的服务器。但对于开发用机器来说就不太合适。目前的FastCGI和Server沟通还不够智能，一个FastCGI进程如果执行时间过长会被当成是死进程杀掉重起，这样在处理长时间任务的时候很麻烦，这样做也使得FastCGI无法允许联机调试。
 2. 因为是多进程，所以比CGI多线程消耗更多的服务器内存，PHP-CGI解释器每进程消耗7至25兆内存，将这个数字乘以50或100就是很大的内存数。
 3. 用的是多进程，确实有时候多线程CGI解释器更快，而且有时候，它也很稳定。
 
## CLI

PHP在命令行运行的接口。也就是说，PHP不单可以写前台网页，它还可以用来写后台的程序。

###优点

 1. 使用多进程，子进程结束以后，内核会负责回收资源；
 2. 使用多进程，子进程异常退出不会导致整个进程Thread退出，父进程还有机会重建流程；
 3. 一个常驻主进程，只负责任务分发，逻辑更清楚。

###缺点

 1. 
 
## Web模块模式

直接使用模块处理PHP,apache php5_mod.so模块就是专门处理PHP的, 当APACHE启动的时候自动加载模块。

###优点

 1. 反应快，更高效，处理也更安全。

###缺点

 1. 访问大的时候可能会拖累WEB服务软件


