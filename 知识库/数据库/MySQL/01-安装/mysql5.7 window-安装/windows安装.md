### windows 安装mysql5.7

#####  安装步骤：

1、下载mysql5.7安装包 （https://downloads.mysql.com/archives/community/

2、配置MySQL环境变量

3、配置my.ini文件

4、使用命令进行安装

5、修改MySQL的密码

##### 一、下载

![img.png](..%2F..%2F..%2F..%2F..%2Fimages%2Fimg.png)

##### 二、配置MySQL环境变量

在系统环境变量中配置如下：
名称：MYSQL_HOME
值：MySQL的安装路径（例如：D:\MySQL\mysql-5.7.24-winx64）
追加系统path路径：;%MYSQL_HOME%\bin 到原有值的后面

##### 三、配置my.ini文件

在D:\MySQL\mysql-5.7.24-winx64 下创建my.ini文件，注意 使用D://

```MYSQL
[mysqld]
# 端口号
port = 3306
# mysql-5.7.27-winx64的路径
basedir=D://MySQL/mysql-5.7.24-winx64
# mysql-5.7.27-winx64的路径+/data
datadir=D://MySQL/mysql-5.7.24-winx64/data 
# 最大连接数
max_connections=200
# 编码
character-set-server=utf8
default-storage-engine=INNODB
sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES
[mysql]
# 编码
default-character-set=utf8 
 

```

##### 四、使用命令进行安装

使用管理员身份打开cmd窗口，进入MySQL的bin目录下
执行安装命令：

```
mysqld -install
```

若出现Service successfully installed，证明安装成功
如出现Install of the Service Denied，则说明没有以管理员权限来运行cmd
执行初始化命令：

```
mysqld --initialize
```

最后执行启动命令：

```
net start mysql
```

##### 五、修改MySQL的密码

**第一步、先停掉MySQL服务**

执行命令： 

```shell
net stop mysql
```

**第二步、修改my.ini文件**
[mysqld] 下添加

```shell
 skip-grant-tables
```

**第三步、重启MySQL**
执行命令：

```SHELL
net start mysql
```

**第四步、进入MySQL**
执行命令：

```shell
mysql -u root -p
```

不需要输入密码，直接回车
使用MySQL，修改密码

(也可以不执行)执行命令：

```
use mysql;
```

修改密码
执行命令： 

```
update mysql.user set authentication_string=password(‘密码’) where user=‘root’;
```

接下来刷新一下MySQL
执行命令： 

```
flush privileges;
```

将 my.ini配置文件中的skip-grant-tables删除
重启一下MySQL服务
之后，若在执行

```
 mysql -uroot -p 
```

后输入你新更改的密码，即可登录，安装完成。