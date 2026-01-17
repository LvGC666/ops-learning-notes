# 我的运维学习笔记


## 📝day1(2026/1/2)
学会了VMware Workstaion、Centos Stream9以及Ubuntu Server的配置

通过MobaXterm远程连接到了Linux系统

### linux基础命令
-'ip a':查看网络接口信息

-'shutdown -h -r -s:控制linux系统立即、定时关机、重启以及取消

明天继续学习Linux核心命令，加油！！！

## 📝day2(2026/1/3)
### Linux目录

/bin:二进制命令所在目录

/dev:/device(设备文件目录)

/etc:系统配置文件目录

/home:普通用户的家目录(桌面)

/root:Linux超级管理员家目录

/opt:额外的软件安装所在目录

/sbin:超级管理员命令所在目录
### Linux定位与查看

pwd:查看当前所在位置

ls：

ls -a:显示指定目录下的所有子目录与文件

ls -l(ll):以列表的形式显示文件详情信息

ls -h(可搭配ll命令):显示文件大小和单位

### 切换与目录结构

cd:

cd :切换进入用户家目录

cd 路径:进入指定目录

cd ..:切换到上级目录(实现于两个最近操作的目录)

tree:将目录以树形结构的形式呈现

### 目录管理命令

mkdir -p:创建多级目录(文件夹)

rmdir :删除空目录

### 文件操作命令

touch *.*:创建一个文件

cp -r 源文件位置 目标路径:实现文件或目录的复制

mv 源文件路径 目标路径:实现文件的移动以及重命名

rm -r(-f) 文件/目录路径:实现对文件或目录的删除

find:

find 路径 -name *.txt (按照文档名称查找) -type f(文件) d(文件夹) (按照文档的类型查找) -size (按照文件大小查找) -mtime (按照修改日期查找) 

-exec 操作命令 {} \;(对于查找到的结果进行指令操作)

拓展:如果将find执行后的结果输出到文件中则使用重定向符号

命令1 > 目标文件 (>:覆盖 >>:追加)如果重定向的目标文件不存在则会自动创建

如果修改文件的最后使用时间则使用 touch -d "xxxx-xx-xx xx:xx:xx:"目标文件

## 📝day3(2026/1/4)

编辑文件：vi、vim(需通过命令安装:dnf -y install vim)

vim a.txt(直接打开文件)  vim +10 a.txt(打开文件并定位到第10行)

vim命令模式:

dd(剪切或删除光标所在行)  ndd(从光标位置向下连续剪切或删除n行)

yy(复制光标所在行)       nyy(从光标位置向下连续复制n行)

p(粘贴)

gg(回到顶部)  GG(回到底部)

vim编辑模式:

i(前) a(后) o(后一行) O(前一行)

esc(退出编辑模式)

vim底行模式:

:w(保存)  :q(退出需先保存)  !(强制)  :x(保存并退出)  ：set nu(设置行号)  /关键词(搜索关键词)

文本查看命令:

cat 文件 (从上往下查看所有数据，适合小文件)

more 文件 (分页查看文件)

less 文件 

使用q退出查看，/关键词 可进行搜索，使用n可跳到下一结果

tail 参数 文件 （从后往前并监控文件变化）

tail -N 文件 （从后往前看N行）   tail -f 文件（是否持续显示末尾内容） 

echo xxx :打印输出到控制台

wc 参数 文件（统计文件中的行数、单词数、字节数）

-l（行数）  -w（单词数） -c（字节数） -m（字符数） -L（最长行的长度）

grep 内容 文件 （直接找到包含内容的行并显示出来）

| 表⽰管道符号
格式：命令1 | 命令2 | 命令3 ....    作⽤：将上⼀个命令的执⾏结果，作为下⼀个命令的输⼊

文件解压缩命令 
-c（打包一个新文件） -x（解压缩文件） -z（使用gzip压缩或解压，产生.tar.gz格式文件） -f（指定压缩或解压后的文件名称） -v（显示过程）
一般组合：压缩（-czvf） 解压（-xzvf）

zip -r 文件名.zip 需要压缩的文件名

unzip 文件名.zip -d 解压路径

### 用户和组管理

group add（添加） mod（修改） del（删除） -g（指定用户组编号） -name（用户组名称）

## 📝day4(2026/1/5)

useradd(添加)  -g（设置主组） -G（设置附加组） -u(设置用户id) -d（设置用户家目录） -s（设置用户的类型，默认为普通用户/bin/bash, 系统用户/sbin/nologin）

usermod(修改)  与添加用户指令相同

userdel（删除） -r（连同家目录的相关信息删除） -f（强制删除）

passwd  用户名（修改用户密码）

su - 用户名（切换至用户）

### Linux的权限管理

三种权限：可读（r） 可写（w） 可执行（x）

权限三部分：所属用户权限（u） 所属用户组权限（g） 其他用户权限（o）

设置文件或目录权限：

字母方式： chmod -R 权限信息（+ - =）需要的权限 文件目录

数字方式： chmod -R 三位数字 文件目录

可读：4  可写：2  可执行：1  （文件默认权限：644  目录默认权限：744）

冒险位s（一般给所属用户或组设置）

粘滞位t（一般给其他用户设置）

设置所属用户和所属组： chown -R 用户名（用户组） 文件目录

ACL权限：

查看：getfacl

设置：setfacl -R -m u：用户名：权限 文件目录

setfacl -R -m g：用户名：权限 文件目录

删除： setfacl -R -x u：用户名 文件目录

setfacl -R -x g：用户组 文件目录

setfacl -R -b 文件目录

## 📝day5(2026/1/17)

### 部署环境使用命令

修改主机名:hostnamectl set-hostname 主机名

设置host地址： 在/etc/hosts文件中添加  私网IP 主机名 地址

#### JDK部署

1. mkdir -p /export/software/ (创建安装包目录)
2. 联网下载安装包
   cd /export/software/
   wget https://raw.gitcode.com/open-source-toolkit/66825/blobs/7acfac1a75800e01c620ea37a18de1fa62c645e3/jdk-8u241-linux-x64.tar.gz
3.解压到/opt下
  tar -xzf jdk-8u241-linux-x64.tar.gz -C /opt
4.测试
  cd /opt/jdk1.8.0_241/bin
  ./java -version
5.配置全局使用的环境变量
  vi /etc/profile
  进入命令行模式后， 输入G，切换到文件底部,然后输入 o 在下一行插入内容
  添加以下内容:
export JAVA_HOME=/opt/jdk1.8.0_241(设置 JAVA_HOME 环境变量)

export PATH=$JAVA_HOME/bin:$PATH(设置 PATH 环境变量，方便在命令行使用 java 命令)

export CLASSPATH=$JAVA_HOME/lib:$CLASSPATH(设置 CLASSPATH 环境变量（可选）)

修改后,保存退出 
esc -> :x

重新加载配置信息，让其生效：
source /etc/profile

说明：source 命令会读取并执行指定文件中的命令，因此在执行 source 时，文件中的环境变量或命令就会被当前 shell 会话所执行，并立即生效

6.测试
   在任意路径下执行
   java -version或javac

#### MySQL部署

1.安装
dnf install -y https://dev.mysql.com/get/mysql80-community-release-el9-1.noarch.rpm

2.查看是否启动
dnf repolist enabled | grep mysql

3.安装MySQL8
dnf install -y mysql-community-server --nogpgcheck

4.启动MySQL相关服务
systemctl start mysqld
systemctl enable mysqld
systemctl status mysqld

5.获取MySQL初始root密码
日志放置位置： /var/log/mysqld.log
grep password /var/log/mysqld.log

6.登录MySQL设置安全相关配置
mysql_secure_installation

7.测试登录
mysql -uroot -p[密码]   可以省略密码 直接回车，然后输入密码  

8.导入项目
cd ~
mysql -uroot -pAa123456. < 文件.sql

9.校验
mysql -uroot -pAa123456.(登录MySQL)
show databases;(查询是否有数据库， 看到 forum-java)
use forum-java
show tables;(查询是否有相关的表)
select * from forum_user;(查询是否有数据)

#### Tomcat部署

1.下载安装包
cd /export/software
wget https://mirrors.huaweicloud.com/apache/tomcat/tomcat-9/v9.0.97/bin/apache-tomcat-9.0.97.tar.gz

2.解压Tomcat服务器到/opt/目录下
cd /export/software/
tar -xzf apache-tomcat-9.0.97.tar.gz -C /opt/
cd /opt/

3.启动Tomcat服务器
cd /opt/apache-tomcat-9.0.97/bin
./startup.sh
ps -ef | grep tomcat(通过进程查看是否有Tomcat进程信息)
ss -tulnp(通过查看端口)

4.添加防火墙配置

5.监控Tomcat日志服务
tomcat服务日志: catalina.out

forum-java: 此目录为本次博客系统的相关日志
access.log: 访问日志
error.log: 错误日志
forum-java.log: 项目运行日志 [该项目目前主要使用此日志]

#### Nginx服务部署

1.安装
dnf install -y nginx 

2.启动
systemctl start nginx
systemctl enable nginx
systemctl status nginx(查看状态信息)

3.开放防火墙(http(80)https(443))

4.测试
http://nginx服务器的ip地址80

5.修改Nginx配置文件
vim /etc/nginx/nginx.conf

添加以下内容:
location / {
    proxy_pass http://node2.itcast.cn:8080/;
}

使用Nginx自带的重新加载配置的命令
nginx -s reload

6.监控Nginx日志
- Nginx日志记录所在位置: /var/log/nginx
- access.log:  Nginx访问日志
- error.log: 错误日志
