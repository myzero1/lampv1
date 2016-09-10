#各个发行系列的不同
各个系列的linux的不同主要是表现在对软件的管理上。下面就说说ubuntu这里系列的软件管理

#ubuntu

## 一、Ubuntu中软件安装方法

1. APT方式

    1. apt-cache search ------(package 搜索包)

    1. 普通安装：apt-get install softname1 softname2 …;

    2. 修复安装：apt-get -f install softname1 softname2... ;(-f Atemp to correct broken dependencies)

    3. 重新安装：apt-get --reinstall install softname1 softname2...;

2. Dpkg方式

    1. 普通安装：dpkg -i package_name.deb

3. 源码安装（.tar、tar.gz、tar.bz2、tar.Z）

    * 首先解压缩源码压缩包然后通过tar命令来完成

        1. 解xx.tar.gz：tar zxf xx.tar.gz 
        
        2. 解xx.tar.Z：tar zxf xx.tar.Z 
        
        3. 解xx.tgz：tar zxf xx.tgz 
        
        4. 解xx.bz2：bunzip2 xx.bz2 
        
        6. 解xx.tar：tar xf xx.tar

    * 然后进入到解压出的目录中，建议先读一下README之类的说明文件，因为此时不同源代码包或者预编译包可能存在差异，然后建议使用ls -F --color或者ls -F命令（实际上我的只需要 l 命令即可）查看一下可执行文件，可执行文件会以*号的尾部标志。

    * 一般依次执行
        1. ./configure

        2. make

        3. sudo make install

    * 即可完成安装。

## 二、Ubuntu中软件包的卸载方法

1. APT方式

    1. 移除式卸载：apt-get remove softname1 softname2 …;（移除软件包，当包尾部有+时，意为安装）

    3. 清除式卸载 ：apt-get --purge remove softname1 softname2...;(同时清除配置)

    4. 清除式卸载：apt-get purge sofname1 softname2...;(同上，也清除配置文件)

2. Dpkg方式

    1. 移除式卸载：dpkg -r pkg1 pkg2 ...;

    3. 清除式卸载：dpkg -P pkg1 pkg2...;
    
## 三、查看已经安装的包

1. dpkg -l --列出当前系统中所有的包.可以和参数less一起使用在分屏查看. (类似于rpm -qa)

3. dpkg -l |grep -i "软件包名" --查看系统中与"软件包名"相关联的包.

## 四、其他应用
1. apt
    1. apt-cache search # ------(package 搜索包)
    1. apt-cache show #------(package 获取包的相关信息，如说明、大小、版本等)
    1. apt-get install # ------(package 安装包)
    1. apt-get install # -----(package --reinstall 重新安装包)
    1. apt-get -f install # -----(强制安装, "-f = --fix-missing"当是修复安装吧...)
    1. apt-get remove #-----(package 删除包)
    1. apt-get remove --purge # ------(package 删除包，包括删除配置文件等)
    1. apt-get autoremove --purge # ----(package 删除包及其依赖的软件包+配置文件等（只对6.10有效，强烈推荐）)
    1. apt-get update #------更新源
    1. apt-get upgrade #------更新已安装的包
    1. apt-get dist-upgrade # ---------升级系统
    1. apt-get dselect-upgrade #------使用 dselect 升级
    1. apt-cache depends #-------(package 了解使用依赖)
    1. apt-cache rdepends # ------(package 了解某个具体的依赖,当是查看该包被哪些包依赖吧...)
    1. apt-get build-dep # ------(package 安装相关的编译环境)
    1. apt-get source #------(package 下载该包的源代码)
    1. apt-get clean && apt-get autoclean # --------清理下载文件的存档 && 只清理过时的包
    1. apt-get check #-------检查是否有损坏的依赖
    1. dpkg -S filename -----查找filename属于哪个软件包
    1. apt-file search filename -----查找filename属于哪个软件包
    1. apt-file list packagename -----列出软件包的内容
    1. apt-file update --更新apt-file的数据库

2. dpkg
    1. dpkg --info "软件包名" --列出软件包解包后的包名称.
    1. dpkg -l --列出当前系统中所有的包.可以和参数less一起使用在分屏查看. (类似于rpm -qa)
    1. dpkg -l |grep -i "软件包名" --查看系统中与"软件包名"相关联的包.
    1. dpkg -s 查询已安装的包的详细信息.
    1. dpkg -L 查询系统中已安装的软件包所安装的位置. (类似于rpm -ql)
    1. dpkg -S 查询系统中某个文件属于哪个软件包. (类似于rpm -qf)
    1. dpkg -I 查询deb包的详细信息,在一个软件包下载到本地之后看看用不用安装(看一下呗).
    1. dpkg -i 手动安装软件包(这个命令并不能解决软件包之前的依赖性问题),如果在安装某一个软件包的时候遇到了软件依赖的问题,可以用apt-get -f install在解决信赖性这个问题.
    1. dpkg -r 卸载软件包.不是完全的卸载,它的配置文件还存在.
    1. dpkg -P 全部卸载(但是还是不能解决软件包的依赖性的问题)
    1. dpkg -reconfigure 重新配置
3. 更多请参考http://www.cnblogs.com/forward/archive/2012/01/10/2318483.html



