#各个发行系列的不同
各个系列的linux的不同主要是表现在对软件的管理上。下面就说说ubuntu这里系列的软件管理

#ubuntu

## 一、Ubuntu中软件安装方法

1. APT方式

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



