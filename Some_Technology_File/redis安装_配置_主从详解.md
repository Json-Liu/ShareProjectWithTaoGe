##Redis 安装 配置 部署 详解
###1、安装 Redis
****
>切换： cd /usr/local/    （建议放这个目录下，也可以自定义其他目录）
>下载： wget http://download.redis.io/releases/redis-3.2.0.tar.gz
>解压： tar xzf redis-3.2.0.tar.gz
>切换： cd redis-3.2.0
>编译： make （必须先安装GCC 如果没有安装  则安装GCC ：yum install gcc-c++）
****
###2、 配置Redis
>Redis的配置比较简单  只有一个配置文件 redis.conf  存在redis的安装目录下（解压的目录）

>建立目录：
>>mkdir /etc/redis            创建存放 redis.conf 配置文件目录
>>mkdir /var/redis/log    创建存放 redis 的日志文件目录
>>mkdir /var/redis/run    创建存放 redis 的PID文件目录
>>mkdir /var/redis/dir    创建存放 redis 的数据文件目录

>修改配置：
>>vim /etc/redis/redis.conf 
>>daemonize yes                                设置 redis 服务可后台运行
>>pidfile /var/redis/run/redis_6379.pid        设置 PID 存放路径
>>logfilr /var/redis/log/redis_6379.log        设置 redis 日志存放路径
>>dbfilename dump_6379.rdb
>>dir /var/redis/dir                            设置 redis 数据文件存放路径
###3、启动与关闭
>cp redis-benchmark redis-cli redis-server /usr/bin/         把常用的redis命令拷贝到 /usr/bin/ >目录中 这样就可以在任意路径下使用 redis 命令，因为 LINUX 会自动到 /usr/bin/ 目录下搜索命令

>启动 redis 服务:
>>redis-server /etc/redis/redis.conf            开启 redis 服务 商品为配置文件中默认的 6379
>>进入 redis 命令行：
>>>redis-cli （默认使用端口为 6379 的 redis 服务 ） 或 redis-cli -p 6379
>>>127.0,0,1:6379> set name helloworld
>>>"OK"
>>>127.0,0,1:6379> get name 
>>>"helloworld"

>关闭 redis 服务:
>>redis-cli shutdown  或 redis-cli -p 6379 shutdown 关闭端口为 6379 的 redis 服务
>>开启多个实例：
>>>安装、配置好单实例的 redis 服务（前面三步）
>>>在 /etc/redis 目录下拷贝 redis.conf 配置文件为 redis_6380.conf （建议这种用 redis_端口号 >>>这种形式 方便识别）
>>>修改 redis_6380.conf 配置文件中的 端口号 PID文件 日志存放路径 数据文件存放路径 
>>>启动新实例: redis-server /etc/redis/redis_6380.conf

###4、配置主从服务器
>第一种方法:在配置文件中加上 slave of IP 端口 EXP：slaveof 192.168.1.1 6379
>第二种方法：利用 redis-cli 进行到 redis 命令行 输入  slaveof 192.168.1.1 6379 利用 SLAVEOF 命令 然后同步就会开始
