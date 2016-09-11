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

## Usage

To spawn a new instance of wordpress on port 80.  The -p 80:80 maps the internal docker port 80 to the outside port 80 of the host machine.

```bash
$ sudo docker run -p 80:80 --name lampv1 -d myzero1/lampv1
```

Start your newly created docker.

```
$ sudo docker start lampv1
```

After starting the docker-wordpress-nginx check to see if it started and the port mapping is correct.  This will also report the port mapping between the docker container and the host machine.

```
$ sudo docker ps

0.0.0.0:80 -> 80/tcp lampv1
```

You can the visit the following URL in a browser on your host machine to get started:

```
http://127.0.0.1:80
http://127.0.0.1/phpmyadmin/
```
## notice
  * The defualt user of mysql is root;
  
  * The defualt password of mysql is root;
  
  * You can change it in Dockerfile
    ```
    # add and config mysql 
    RUN echo 'mysql-server-5.6 mysql-server/root_password password root' | sudo debconf-set-selections
    RUN echo 'mysql-server-5.6 mysql-server/root_password_again password root' | sudo debconf-set-selections
    ```



