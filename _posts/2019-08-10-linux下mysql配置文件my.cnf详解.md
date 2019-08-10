---
layout:     post
title:      mysql配置文件my.cnf详解[部分]
subtitle:   my.cnf参数详解
date:       2019-05-27
author:     Wu
header-img: img/post/post-bg-20190810.png
catalog: true
tags:
    - Linux
    - MySQL
    - my.cnf
---

>把几个my.cnf讲解的合并一下，有时间整理一下，可以先搜索查询

### mysql配置文件my.cnf详解[部分]

#### 第一部分

[来源网络](https://www.cnblogs.com/toby/articles/2198697.html)

| 参数 | 说明 |
| --- | --- |
| basedir = path | 使用给定目录作为根目录(安装目录)。 |
| character-sets-dir = path | 给出存放着字符集的目录。 |
| datadir = path | 从给定目录读取数据库文件。 |
| pid-file = filename | 为mysqld程序指定一个存放进程ID的文件(仅适用于UNIX/Linux系统); Init-V脚本需要使用这个文件里的进程ID结束mysqld进程。 |
| socket = filename | 为MySQL客户程序与服务器之间的本地通信指定一个套接字文件(仅适用于UNIX/Linux系统; 默认设置一般是/var/lib/mysql/mysql.sock文件)。在Windows环境下，如果MySQL客户与服务器是通过命名管道进行通信 的，–sock选项给出的将是该命名管道的名字(默认设置是MySQL)。 |
| lower_case_table_name = 1/0 | 新目录和数据表的名字是否只允许使用小写字母; 这个选项在Windows环境下的默认设置是1(只允许使用小写字母)。 |

> mysqld程序：语言设置

| 参数 | 说明 |
| --- | --- |
| character-sets-server = name | 新数据库或数据表的默认字符集。为了与MySQL的早期版本保持兼容，这个字符集也可以用–default-character-set选项给出; 但这个选项已经显得有点过时了。 |
| collation-server = name | 新数据库或数据表的默认排序方式。 |
| lanuage = name | 用指定的语言显示出错信息。 |

> mysqld程序：通信、网络、信息安全

| 参数 | 说明 |
| --- | --- |
| enable-named-pipes | 允许Windows 2000/XP环境下的客户和服务器使用命名管道(named pipe)进行通信。这个命名管道的默认名字是MySQL，但可以用–socket选项来改变。 |
| local-infile [=0] | 允许/禁止使用LOAD DATA LOCAL语句来处理本地文件。 |
| myisam-recover [=opt1, opt2, ...] | 在启动时自动修复所有受损的MyISAM数据表。这个选项的可取值有4种:DEFAULT、BACKUP、QUICK和FORCE; 它们与myisamchk程序的同名选项作用相同。 |
| old-passwords | 使用MySQL 3.23和4.0版本中的老算法来加密mysql数据库里的密码(默认使用MySQL 4.1版本开始引入的新加密算法)。 |
| port = n | 为MySQL程序指定一个TCP/IP通信端口(通常是3306端口)。 |
| safe-user-create | 只有在mysql.user数据库表上拥有INSERT权限的用户才能使用GRANT命令; 这是一种双保险机制(此用户还必须具备GRANT权限才能执行GRANT命令)。 |
| shared-memory | 允许使用内存(shared memory)进行通信(仅适用于Windows)。 |
| shared-memory-base-name = name | 给共享内存块起一个名字(默认的名字是MySQL)。 |
| skip-grant-tables | 不使用mysql数据库里的信息来进行访问控制(警告:这将允许用户任何用户去修改任何数据库)。 |
| skip-host-cache | 不使用高速缓存区来存放主机名和IP地址的对应关系。 |
| skip-name-resovle | 不把IP地址解析为主机名; 与访问控制(mysql.user数据表)有关的检查全部通过IP地址行进。 |
| skip-networking | 只允许通过一个套接字文件(Unix/Linux系统)或通过命名管道(Windows系统)进行本地连接，不允许ICP/IP连接; 这提高了安全性，但阻断了来自网络的外部连接和所有的Java客户程序(Java客户即使在本地连接里也使用TCP/IP)。 |
| user = name | mysqld程序在启动后将在给定UNIX/Linux账户下执行; mysqld必须从root账户启动才能在启动后切换到另一个账户下执行; mysqld_safe脚本将默认使用–user=mysql选项来启动mysqld程序。 |

> mysqld程序：内存管理、优化、查询缓存区

| 参数 | 说明 |
| --- | --- |
| bulk_insert_buffer_size = n | 为一次插入多条新记录的INSERT命令分配的缓存区长度(默认设置是8M)。 |
| key_buffer_size = n | 用来存放索引区块的RMA值(默认设置是8M)。 |
| join_buffer_size = n | 在参加JOIN操作的数据列没有索引时为JOIN操作分配的缓存区长度(默认设置是128K)。 |
| max_heap_table_size = n | HEAP数据表的最大长度(默认设置是16M); 超过这个长度的HEAP数据表将被存入一个临时文件而不是驻留在内存里。 |
| max_connections = n | MySQL服务器同时处理的数据库连接的最大数量(默认设置是100)。 |
| query_cache_limit = n | 允许临时存放在查询缓存区里的查询结果的最大长度(默认设置是1M)。 |
| query_cache_size = n | 查询缓存区的最大长度(默认设置是0，不开辟查询缓存区)。 |
| query_cache_type = 0/1/2 | 查询缓存区的工作模式:0, 禁用查询缓存区; 1，启用查询缓存区(默认设置); 2，”按需分配”模式，只响应SELECT SQL_CACHE命令。 |
| read_buffer_size = n | 为从数据表顺序读取数据的读操作保留的缓存区的长度(默认设置是128KB); 这个选项的设置值在必要时可以用SQL命令SET SESSION read_buffer_size = n命令加以改变。 |
| read_rnd_buffer_size = n | 类似于read_buffer_size选项，但针对的是按某种特定顺序(比如使用了ORDER BY子句的查询)输出的查询结果(默认设置是256K)。 |
| sore_buffer = n | 为排序操作分配的缓存区的长度(默认设置是2M); 如果这个缓存区太小，则必须创建一个临时文件来进行排序。 |
| table_cache = n | 同时打开的数据表的数量(默认设置是64)。 |
| tmp_table_size = n | 临时HEAP数据表的最大长度(默认设置是32M); 超过这个长度的临时数据表将被转换为MyISAM数据表并存入一个临时文件。 |

> mysqld程序：日志

| 参数 | 说明 |
| --- | --- |
| log [= file] | 把所有的连接以及所有的SQL命令记入日志(通用查询日志); 如果没有给出file参数，MySQL将在数据库目录里创建一个hostname.log文件作为这种日志文件(hostname是服务器的主机名)。 |
| log-slow-queries [= file] | 把执行用时超过long_query_time变量值的查询命令记入日志(慢查询日志); 如果没有给出file参数，MySQL将在数据库目录里创建一个hostname-slow.log文件作为这种日志文件(hostname是服务器主机 名)。 |
| long_query_time = n | 慢查询的执行用时上限(默认设置是10s)。 |
| long_queries_not_using_indexs | 把慢查询以及执行时没有使用索引的查询命令全都记入日志(其余同–log-slow-queries选项)。 |
| log-bin [= filename] | 把对数据进行修改的所有SQL命令(也就是INSERT、UPDATE和DELETE命令)以二进制格式记入日志(二进制变更日志，binary update log)。这种日志的文件名是filename.n或默认的hostname.n，其中n是一个6位数字的整数(日志文件按顺序编号)。 |
| log-bin-index = filename | 二进制日志功能的索引文件名。在默认情况下，这个索引文件与二进制日志文件的名字相同，但后缀名是.index而不是.nnnnnn。 |
| max_binlog_size = n | 二进制日志文件的最大长度(默认设置是1GB)。在前一个二进制日志文件里的信息量超过这个最大长度之前，MySQL服务器会自动提供一个新的二进制日志文件接续上。 |
| binlog-do-db = dbname | 只把给定数 据库里的变化情况记入二进制日志文件，其他数据库里的变化情况不记载。如果需要记载多个数据库里的变化情况，就必须在配置文件使用多个本选项来设置，每个数据库一行。 |
| binlog-ignore-db = dbname | 不把给定数据库里的变化情况记入二进制日志文件。 |
| sync_binlog = n | 每经过n次日志写操作就把日志文件写入硬盘一次(对日志信息进行一次同步)。n=1是最安全的做法，但效率最低。默认设置是n=0，意思是由操作系统来负责二进制日志文件的同步工作。 |
| log-update [= file] | 记载出错情况的日志文件名(出错日志)。这种日志功能无法禁用。如果没有给出file参数，MySQL会使用hostname.err作为种日志文件的名字。 |

> mysqld程序：镜像(主控镜像服务器)

| 参数 | 说明 |
| --- | --- |
| server-id = n | 给服务器分配一个独一无二的ID编号; n的取值范围是1~2的32次方启用二进制日志功能。 |
| log-bin = name | 启用二进制日志功能。这种日志的文件名是filename.n或默认的hostname.n，其中的n是一个6位数字的整数(日志文件顺序编号)。 |
| binlog-do/ignore-db = dbname | 只把给定数据库里的变化情况记入二进制日志文件/不把给定的数据库里的变化记入二进制日志文件。 |

> mysqld程序：镜像(从属镜像服务器)

| 参数 | 说明 |
| --- | --- |
| server-id = n | 给服务器分配一个唯一的ID编号 |
| log-slave-updates | 启用从属服务器上的日志功能，使这台计算机可以用来构成一个镜像链(A->B->C)。 |
| master-host = hostname | 主控服务器的主机名或IP地址。如果从属服务器上存在mater.info文件(镜像关系定义文件)，它将忽略此选项。 |
| master-user = replicusername | 从属服务器用来连接主控服务器的用户名。如果从属服务器上存在mater.info文件，它将忽略此选项。 |
| master-password = passwd | 从属服务器用来连接主控服务器的密码。如果从属服务器上存在mater.info文件，它将忽略此选项。 |
| master-port = n | 从属服务器用来连接主控服务器的TCP/IP端口(默认设置是3306端口)。 |
| master-connect-retry = n | 如果与主控服务器的连接没有成功，则等待n秒(s)后再进行管理方式(默认设置是60s)。如果从属服务器存在mater.info文件，它将忽略此选项。 |
| master-ssl-xxx = xxx | 对主、从服务器之间的SSL通信进行配置。 |
| read-only = 0/1 | 0: 允许从属服务器独立地执行SQL命令(默认设置); 1: 从属服务器只能执行来自主控服务器的SQL命令。 |
| read-log-purge = 0/1 | 1: 把处理完的SQL命令立刻从中继日志文件里删除(默认设置); 0: 不把处理完的SQL命令立刻从中继日志文件里删除。 |
| replicate-do-table = dbname.tablename | 与–replicate-do-table选项的含义和用法相同，但数据库和数据库表名字里允许出现通配符”%” (例如: test%.%–对名字以”test”开头的所有数据库里的所以数据库表进行镜像处理)。 |
| replicate-do-db = name | 只对这个数据库进行镜像处理。 |
| replicate-ignore-table = dbname.tablename | 不对这个数据表进行镜像处理。 |
| replicate-wild-ignore-table = dbn.tablen | 不对这些数据表进行镜像处理。 |
| replicate-ignore-db = dbname | 不对这个数据库进行镜像处理。 |
| replicate-rewrite-db = db1name > db2name | 把主控数据库上的db1name数据库镜像处理为从属服务器上的db2name数据库。 |
| report-host = hostname | 从属服务器的主机名; 这项信息只与SHOW SLAVE HOSTS命令有关–主控服务器可以用这条命令生成一份从属服务器的名单。 |
| slave-compressed-protocol = 1 | 主、从服务器使用压缩格式进行通信–如果它们都支持这么做的话。 |
| slave-skip-errors = n1, n2, …或all | 即使发生出错代码为n1、n2等的错误，镜像处理工作也继续进行(即不管发生什么错误，镜像处理工作也继续进行)。如果配置得当，从属服务器不应 该在执行 SQL命令时发生错误(在主控服务器上执行出错的SQL命令不会被发送到从属服务器上做镜像处理); 如果不使用slave-skip-errors选项，从属服务器上的镜像工作就可能因为发生错误而中断，中断后需要有人工参与才能继续进行。 |

> mysqld程序–InnoDB：基本设置、表空间文件

| 参数 | 说明 |
| --- | --- |
| skip-innodb | 不加载InnoDB数据表驱动程序–如果用不着InnoDB数据表，可以用这个选项节省一些内存。 |
| innodb-file-per-table | 为每一个新数据表创建一个表空间文件而不是把数据表都集中保存在中央表空间里(后者是默认设置)。该选项始见于MySQL 4.1。 |
| innodb-open-file = n | InnoDB数据表驱动程序最多可以同时打开的文件数(默认设置是300)。如果使用了innodb-file-per-table选项并且需要同时打开很多数据表的话，这个数字很可能需要加大。 |
| innodb_data_home_dir = p | InnoDB主目录，所有与InnoDB数据表有关的目录或文件路径都相对于这个路径。在默认的情况下，这个主目录就是MySQL的数据目录。 |
| innodb_data_file_path = ts | 用来容纳InnoDB为数据表的表空间: 可能涉及一个以上的文件; 每一个表空间文件的最大长度都必须以字节(B)、兆字节(MB)或千兆字节(GB)为单位给出; 表空间文件的名字必须以分号隔开; 最后一个表空间文件还可以带一个autoextend属性和一个最大长度(max:n)。例如，ibdata1:1G; ibdata2:1G:autoextend:max:2G的意思是: 表空间文件ibdata1的最大长度是1GB，ibdata2的最大长度也是1G，但允许它扩充到2GB。除文件名外，还可以用硬盘分区的设置名来定义表 空间，此时必须给表空间的最大初始长度值加上newraw关键字做后缀，给表空间的最大扩充长度值加上raw关键字做后缀(例如/dev/hdb1: 20Gnewraw或/dev/hdb1:20Graw); MySQL 4.0及更高版本的默认设置是ibdata1:10M:autoextend。 |
| innodb_autoextend_increment = n | 带有autoextend属性的表空间文件每次加大多少兆字节(默认设置是8MB)。这个属性不涉及具体的数据表文件，那些文件的增大速度相对是比较小的。 |
| innodb_lock_wait_timeout = n | 如果某个事务在等待n秒(s)后还没有获得所需要的资源，就使用ROLLBACK命令放弃这个事务。这项设置对于发现和处理未能被InnoDB数据表驱动 程序识别出来的死锁条件有着重要的意义。这个选项的默认设置是50s。 |
| innodb_fast_shutdown 0/1 | 是否以最快的速度关闭InnoDB，默认设置是1，意思是不把缓存在INSERT缓存区的数据写入数据表，那些数据将在MySQL服务器下次启动 时再写入 (这么做没有什么风险，因为INSERT缓存区是表空间的一个组成部分，数据不会丢失)。把这个选项设置为0反面危险，因为在计算机关闭时，InnoDB 驱动程序很可能没有足够的时间完成它的数据同步工作，操作系统也许会在它完成数据同步工作之前强行结束InnoDB，而这会导致数据不完整。 |

> mysqld程序-InnoDB：日志

| 参数 | 说明 |
| --- | --- |
| innodb_log_group_home_dir = p | 用来存放InnoDB日志文件的目录路径(如ib_logfile0、ib_logfile1等)。在默认的情况下，InnoDB驱动程序将使用 MySQL数据目录作为自己保存日志文件的位置。 |
| innodb_log_files_in_group = n | 使用多少个日志文件(默认设置是2)。InnoDB数据表驱动程序将以轮转方式依次填写这些文件; 当所有的日志文件都写满以后，之后的日志信息将写入第一个日志文件的最大长度(默认设置是5MB)。这个长度必须以MB(兆字节)或GB(千兆字节)为单 位进行设置。 |
| innodb_flush_log_at_trx_commit = 0/1/2 | 这个选项决定着什么时候把日志信息写入日志文件以及什么时候把这些文件物理地写(术语称为”同步”)到硬盘上。设置值0的意思是每隔一秒写一次日 志并进行 同步，这可以减少硬盘写操作次数，但可能造成数据丢失; 设置值1(设置设置)的意思是在每执行完一条COMMIT命令就写一次日志并进行同步，这可以防止数据丢失，但硬盘写操作可能会很频繁; 设置值2是一般折衷的办法，即每执行完一条COMMIT命令写一次日志，每隔一秒进行一次同步。 |
| innodb_flush_method = x | InnoDB日志文件的同步办法(仅适用于UNIX/Linux系统)。这个选项的可取值有两种: fdatasync，用fsync()函数进行同步; O_DSYNC，用O_SYNC()函数进行同步。 |
| innodb_log_archive = 1 | 启用InnoDB驱动程序的archive(档案)日志功能，把日志信息写入ib_arch_log_n文件。启用这种日志功能在InnoDB与 MySQL一起使用时没有多大意义(启用MySQL服务器的二进制日志功能就足够用了)。 |

> mysqld程序–InnoDB：缓存区的设置和优化

| 参数 | 说明 |
| --- | --- |
| innodb_log_buffer_pool_size = n | 为InnoDB数据表及其索引而保留的RAM内存量(默认设置是8MB)。这个参数对速度有着相当大的影响，如果计算机上只运行有 MySQL/InnoDB数据库服务器，就应该把全部内存的80%用于这个用途。 |
| innodb_log_buffer_size = n | 事务日志文件写操作缓存区的最大长度(默认设置是1MB)。 |
| innodb_additional_men_pool_size = n | 为用于内部管理的各种数据结构分配的缓存区最大长度(默认设置是1MB)。 |
| innodb_file_io_threads = n | I/O操作(硬盘写操作)的最大线程个数(默认设置是4)。 |
| innodb_thread_concurrency = n | InnoDB驱动程序能够同时使用的最大线程个数(默认设置是8)。 |

> mysqld程序：其它选项

| 参数 | 说明 |
| --- | --- |
| bind-address = ipaddr | MySQL服务器的IP地址。如果MySQL服务器所在的计算机有多个IP地址，这个选项将非常重要。 |
| default-storage-engine = type | 新数据表的默认数据表类型(默认设置是MyISAM)。这项设置还可以通过–default-table-type选项来设置。 |
| default-timezone = name | 为MySQL服务器设置一个地理时区(如果它与本地计算机的地理时区不一样)。 |
| ft_min_word_len = n | 全文索引的最小单词长度工。这个选项的默认设置是4，意思是在创建全文索引时不考虑那些由3个或更少的字符构建单词。 |
| Max-allowed-packet = n | 客户与服务器之间交换的数据包的最大长度，这个数字至少应该大于客户程序将要处理的最大BLOB块的长度。这个选项的默认设置是1MB。 |
| Sql-mode = model1, mode2, … | MySQL将运行在哪一种SQL模式下。这个选项的作用是让MySQL与其他的数据库系统保持最大程度的兼容。这个选项的可取值包括ansi、db2、 oracle、no_zero_date、pipes_as_concat。 |

`注意：如果在配置文件里给出的某个选项是mysqld无法识别的，MySQL服务器将不启动。`


#### 第二部分

[来源网络](https://blog.51cto.com/moerjinrong/2092791)

官网说：从5.7.18开始不在二进制包中提供my-default.cnf文件。参考：https://dev.mysql.com/doc/refman/5.7/en/binary-installation.html

经过测试，在5.7.18版本中，使用tar.gz安装时，也就是压缩包解压出来安装这种，已经不再需要my.cnf文件也能正常运行。

my.cnf文件就是把在命令行上启动MySQL时后面的参数用cnf文件配置好，那么下载启动时就不再需要在命令上加如参数。

这个my.cnf文件可以是自定义位置，也可以使用如下默认的位置，只要放在默认位置，MySQL自动识别（通过deb或者APT源安装的，初始位置在下方列表）：
在Unix和类Unix系统上读取选项文件
文件名                    目的
/etc/my.cnf              全局选项    
/etc/mysql/my.cnf        全局选项    
SYSCONFDIR/my.cnf        全局选项    
$MYSQL_HOME/my.cnf       服务器特定选项（仅限服务器）    
defaults-extra-file      指定的文件 --defaults-extra-file（如果有的话）    
~/.my.cnf                用户特定的选项    
~/.mylogin.cnf           用户特定的登录路径选项（仅限客户端）    

在上表中，~表示当前用户的主目录（的值 $HOME）。
首先它会找/etc/my.cnf 这个文件， 如果这个文件不存在，那么它接下来去找/etc/mysql/my.cnf这个文件，依此类推

以上的详细说明可以参考官方解释：
https://dev.mysql.com/doc/refman/5.7/en/option-files.html
https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html?spm=5176.7920929.0.0.42e941d6WvwfAQ#sysvar_block_encryption_mode
https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html#ngram_token_size
https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html#innodb_monitor_enable
https://github.com/xpchild/SQL/wiki/Changes-in-AliSQL-5.6.32-(2016-09-15)#10-sql-filter

总之，无论是使用APT源安装还是deb包安装，或者二进制（压缩包tar.gz）包安装的，都可以通过my.cnf文件进行配置来达到MySQL的启动配置及调优。
由于在5.7.18开始，二进制包不再包含示例文件my-default.cnf，所以我从5.7.17版本中提取了样例，但是发现里面也没有太多项配置，my-default.cnf内容如下：
```
# For advice on how to change settings please see
#  
# *** DO NOT EDIT THIS FILE. It‘s a template which will be copied to the
# *** default location during install, and will be replaced if you
# *** upgrade to a newer version of MySQL.

[mysqld]

# Remove leading # and set to the amount of RAM for the most important data
# cache in MySQL. Start at 70% of total RAM for dedicated server, else 10%.
# innodb_buffer_pool_size = 128M

# Remove leading # to turn on a very important data integrity option: logging
# changes to the binary log between backups.
# log_bin

# These are commonly set, remove the # and set as required.
# basedir = .....
# datadir = .....
# port = .....
# server_id = .....
# socket = .....

# Remove leading # to set options mainly useful for reporting servers.
# The server defaults are faster for transactions and fast SELECTs.
# Adjust sizes as needed, experiment to find the optimal values.
# join_buffer_size = 128M
# sort_buffer_size = 2M
# read_rnd_buffer_size = 2M 

sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES 

其实，这些项都是命令行的参数，在官网上可以从这个页面 

Mysql参数优化对于新手来讲，是比较难懂的东西，其实这个参数优化，是个很复杂的东西，对于不同的网站，及其在线量，访问量，帖子数量，网络情况，以及机器硬件配置都有关系，优化不可能一次性完成，需要不断的观察以及调试，才有可能得到最佳效果。
下面这个是my.cnf示例：
*******************************************************
[client]
default-character-set = utf8mb4

[mysql]
#开启 tab 补全
#auto-rehash
default-character-set = utf8mb4

[mysqld]
port=3306
basedir=/data/server/mysql57/
datadir=/data/server/mysql57/data/
socket=/data/server/mysql57/data/mysql.sock
symbolic-links=0
log-error=/data/logs/mysql57/mysqld.log
pid-file=/data/server/mysql57/data/mysqld57.pid

# 禁用主机名解析
skip-name-resolve
# 默认的数据库引擎
default-storage-engine = InnoDB
innodb-file-per-table=1innodb_force_recovery = 1#一些坑
group_concat_max_len = 10240sql_mode=expire_logs_days = 7memlock

### 字符集配置
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
init_connect='SET NAMES utf8mb4'### GTID
server_id = 330759# 为保证 GTID 复制的稳定, 行级日志
binlog_format = row
# 开启 gtid 功能
gtid_mode = on
# 保障 GTID 事务安全
# 当启用enforce_gtid_consistency功能的时候,
# MySQL只允许能够保障事务安全, 并且能够被日志记录的SQL语句被执行,
# 像create table ... select 和 create temporarytable语句, 
# 以及同时更新事务表和非事务表的SQL语句或事务都不允许执行
enforce-gtid-consistency = true# 以下两条配置为主从切换, 数据库高可用的必须配置
# 开启 binlog 日志功能
log_bin = mysql57-bin 
# 开启从库更新 binlog 日志
log-slave-updates = on
#slave复制进程不随mysql启动而启动
skip_slave_start=1### 慢查询日志
# 打开慢查询日志功能
slow_query_log = 1# 超过2秒的查询记录下来
long_query_time = 2# 记录下没有使用索引的查询
log_queries_not_using_indexes = 0slow_query_log_file =/data/logs/mysql57/slow.log
#log=/data/logs/mysql57/all.log
### 自动修复
# 记录 relay.info 到数据表中
relay_log_info_repository = TABLE
# 记录 master.info 到数据表中 
master_info_repository = TABLE
# 启用 relaylog 的自动修复功能
relay_log_recovery = on
# 在 SQL 线程执行完一个 relaylog 后自动删除
relay_log_purge = 1### 数据安全性配置
# wei关闭 master 创建 function 的功能
log_bin_trust_function_creators = on
# 每执行一个事务都强制写入磁盘
sync_binlog = 1# timestamp 列如果没有显式定义为 not null, 则支持null属性
# 设置 timestamp 的列值为 null, 不会被设置为 current timestamp
explicit_defaults_for_timestamp=true### 优化配置
# 优化中文全文模糊索引
ft_min_word_len = 1# 默认库名表名保存为小写, 不区分大小写
lower_case_table_names = 1# 单条记录写入最大的大小限制
# 过小可能会导致写入(导入)数据失败
max_allowed_packet = 256M
# 半同步复制开启
#rpl_semi_sync_master_enabled = 1#rpl_semi_sync_slave_enabled = 1# 半同步复制超时时间设置
#rpl_semi_sync_master_timeout = 1000# 复制模式(保持系统默认)
#rpl_semi_sync_master_wait_point = AFTER_SYNC
# 后端只要有一台收到日志并写入 relaylog 就算成功
#rpl_semi_sync_master_wait_slave_count = 1# 多线程复制
# 基于组提交的并行复制方式
slave_parallel_type = logical_clock
#并行的SQL线程数量，此参数只有设置   1<N的情况下才会才起N个线程进行SQL重做。
#经过测试对比发现， 如果主库的连接线程为M， 只有M < N的情况下， 备库的延迟才可以完全避免。
slave_parallel_workers = 4### 连接数限制
max_connections = 1500# 验证密码超过20次拒绝连接
max_connect_errors = 200# back_log值指出在mysql暂时停止回答新请求之前的短时间内多少个请求可以被存在堆栈中
# 也就是说，如果MySql的连接数达到max_connections时，新来的请求将会被存在堆栈中
# 以等待某一连接释放资源，该堆栈的数量即back_log，如果等待连接的数量超过back_log
# 将不被授予连接资源
back_log = 500open_files_limit = 65535# 服务器关闭交互式连接前等待活动的秒数
interactive_timeout = 3600# 服务器关闭非交互连接之前等待活动的秒数
wait_timeout = 3600### 内存分配
# 指定表高速缓存的大小。每当MySQL访问一个表时，如果在表缓冲区中还有空间
# 该表就被打开并放入其中，这样可以更快地访问表内容
table_open_cache = 1024# 为每个session 分配的内存, 在事务过程中用来存储二进制日志的缓存
binlog_cache_size = 4M
# 在内存的临时表最大大小
tmp_table_size = 128M
# 创建内存表的最大大小(保持系统默认, 不允许创建过大的内存表)
# 如果有需求当做缓存来用, 可以适当调大此值
max_heap_table_size = 16M
# 顺序读, 读入缓冲区大小设置
# 全表扫描次数多的话, 可以调大此值
read_buffer_size = 1M
# 随机读, 读入缓冲区大小设置
read_rnd_buffer_size = 8M
# 高并发的情况下, 需要减小此值到64K-128K
sort_buffer_size = 1M
# 每个查询最大的缓存大小是1M, 最大缓存64M 数据
query_cache_size = 64M
query_cache_limit = 1M
# 提到 join 的效率
join_buffer_size = 16M
# 线程连接重复利用
thread_cache_size = 64### InnoDB 优化
## 内存利用方面的设置
# 数据缓冲区
innodb_buffer_pool_size=2G
## 日志方面设置
# 事务日志大小
innodb_log_file_size = 256M
# 日志缓冲区大小
innodb_log_buffer_size = 4M
# 事务在内存中的缓冲
innodb_log_buffer_size = 3M
# 主库保持系统默认, 事务立即写入磁盘, 不会丢失任何一个事务
innodb_flush_log_at_trx_commit = 1# mysql 的数据文件设置, 初始100, 以10M 自动扩展
#innodb_data_file_path = ibdata1:100M:autoextend
# 为提高性能, MySQL可以以循环方式将日志文件写到多个文件
innodb_log_files_in_group = 3##其他设置
# 如果库里的表特别多的情况，请增加此值
#innodb_open_files = 800# 为每个 InnoDB 表分配单独的表空间
innodb_file_per_table = 1# InnoDB 使用后台线程处理数据页上写 I/O（输入）请求的数量
innodb_write_io_threads = 8# InnoDB 使用后台线程处理数据页上读 I/O（输出）请求的数量
innodb_read_io_threads = 8# 启用单独的线程来回收无用的数据
innodb_purge_threads = 1# 脏数据刷入磁盘(先保持系统默认, swap 过多使用时, 调小此值, 调小后, 与磁盘交互增多, 性能降低)
innodb_max_dirty_pages_pct = 90# 事务等待获取资源等待的最长时间
innodb_lock_wait_timeout = 120# 开启 InnoDB 严格检查模式, 不警告, 直接报错 1开启 0关闭
innodb_strict_mode=1# 允许列索引最大达到3072
innodb_large_prefix = on

[mysqldump]
# 开启快速导出
quick
default-character-set = utf8mb4
max_allowed_packet = 256M
```

#### 第三部分

[来源网络](https://www.cnblogs.com/smail-bao/p/6030528.html)

提供一个MySQL 5.6版本适合在1GB内存VPS上的my.cnf配置文件。配置文件可以到这里下载：[下载my.cnf](https://download.21yunwei.com/conf/my.cnf)

```
[client] 
port = 3306 
socket = /tmp/mysql.sock

[mysqld] 
port = 3306 
socket = /tmp/mysql.sock

basedir = /usr/local/mysql 
datadir = /data/mysql 
pid-file = /data/mysql/mysql.pid 
user = mysql 
bind-address = 0.0.0.0 
server-id = 1 #表示是本机的序号为1,一般来讲就是master的意思

skip-name-resolve 
# 禁止MySQL对外部连接进行DNS解析，使用这一选项可以消除MySQL进行DNS解析的时间。但需要注意，如果开启该选项， 
# 则所有远程主机连接授权都要使用IP地址方式，否则MySQL将无法正常处理连接请求

#skip-networking

back_log = 600 
# MySQL能有的连接数量。当主要MySQL线程在一个很短时间内得到非常多的连接请求，这就起作用， 
# 然后主线程花些时间(尽管很短)检查连接并且启动一个新线程。back_log值指出在MySQL暂时停止回答新请求之前的短时间内多少个请求可以被存在堆栈中。 
# 如果期望在一个短时间内有很多连接，你需要增加它。也就是说，如果MySQL的连接数据达到max_connections时，新来的请求将会被存在堆栈中， 
# 以等待某一连接释放资源，该堆栈的数量即back_log，如果等待连接的数量超过back_log，将不被授予连接资源。 
# 另外，这值（back_log）限于您的操作系统对到来的TCP/IP连接的侦听队列的大小。 
# 你的操作系统在这个队列大小上有它自己的限制（可以检查你的OS文档找出这个变量的最大值），试图设定back_log高于你的操作系统的限制将是无效的。

max_connections = 1000 
# MySQL的最大连接数，如果服务器的并发连接请求量比较大，建议调高此值，以增加并行连接数量，当然这建立在机器能支撑的情况下，因为如果连接数越多，介于MySQL会为每个连接提供连接缓冲区，就会开销越多的内存，所以要适当调整该值，不能盲目提高设值。可以过’conn%’通配符查看当前状态的连接数量，以定夺该值的大小。

max_connect_errors = 6000 
# 对于同一主机，如果有超出该参数值个数的中断错误连接，则该主机将被禁止连接。如需对该主机进行解禁，执行：FLUSH HOST。

open_files_limit = 65535 
# MySQL打开的文件描述符限制，默认最小1024;当open_files_limit没有被配置的时候，比较max_connections*5和ulimit -n的值，哪个大用哪个， 
# 当open_file_limit被配置的时候，比较open_files_limit和max_connections*5的值，哪个大用哪个。

table_open_cache = 128 
# MySQL每打开一个表，都会读入一些数据到table_open_cache缓存中，当MySQL在这个缓存中找不到相应信息时，才会去磁盘上读取。默认值64 
# 假定系统有200个并发连接，则需将此参数设置为200*N(N为每个连接所需的文件描述符数目)； 
# 当把table_open_cache设置为很大时，如果系统处理不了那么多文件描述符，那么就会出现客户端失效，连接不上

max_allowed_packet = 4M 
# 接受的数据包大小；增加该变量的值十分安全，这是因为仅当需要时才会分配额外内存。例如，仅当你发出长查询或MySQLd必须返回大的结果行时MySQLd才会分配更多内存。 
# 该变量之所以取较小默认值是一种预防措施，以捕获客户端和服务器之间的错误信息包，并确保不会因偶然使用大的信息包而导致内存溢出。

binlog_cache_size = 1M 
# 一个事务，在没有提交的时候，产生的日志，记录到Cache中；等到事务提交需要提交的时候，则把日志持久化到磁盘。默认binlog_cache_size大小32K

max_heap_table_size = 8M 
# 定义了用户可以创建的内存表(memory table)的大小。这个值用来计算内存表的最大行数值。这个变量支持动态改变

tmp_table_size = 16M 
# MySQL的heap（堆积）表缓冲大小。所有联合在一个DML指令内完成，并且大多数联合甚至可以不用临时表即可以完成。 
# 大多数临时表是基于内存的(HEAP)表。具有大的记录长度的临时表 (所有列的长度的和)或包含BLOB列的表存储在硬盘上。 
# 如果某个内部heap（堆积）表大小超过tmp_table_size，MySQL可以根据需要自动将内存中的heap表改为基于硬盘的MyISAM表。还可以通过设置tmp_table_size选项来增加临时表的大小。也就是说，如果调高该值，MySQL同时将增加heap表的大小，可达到提高联接查询速度的效果

read_buffer_size = 2M 
# MySQL读入缓冲区大小。对表进行顺序扫描的请求将分配一个读入缓冲区，MySQL会为它分配一段内存缓冲区。read_buffer_size变量控制这一缓冲区的大小。 
# 如果对表的顺序扫描请求非常频繁，并且你认为频繁扫描进行得太慢，可以通过增加该变量值以及内存缓冲区大小提高其性能

read_rnd_buffer_size = 8M 
# MySQL的随机读缓冲区大小。当按任意顺序读取行时(例如，按照排序顺序)，将分配一个随机读缓存区。进行排序查询时， 
# MySQL会首先扫描一遍该缓冲，以避免磁盘搜索，提高查询速度，如果需要排序大量数据，可适当调高该值。但MySQL会为每个客户连接发放该缓冲空间，所以应尽量适当设置该值，以避免内存开销过大

sort_buffer_size = 8M 
# MySQL执行排序使用的缓冲大小。如果想要增加ORDER BY的速度，首先看是否可以让MySQL使用索引而不是额外的排序阶段。 
# 如果不能，可以尝试增加sort_buffer_size变量的大小

join_buffer_size = 8M 
# 联合查询操作所能使用的缓冲区大小，和sort_buffer_size一样，该参数对应的分配内存也是每连接独享

thread_cache_size = 8 
# 这个值（默认8）表示可以重新利用保存在缓存中线程的数量，当断开连接时如果缓存中还有空间，那么客户端的线程将被放到缓存中， 
# 如果线程重新被请求，那么请求将从缓存中读取,如果缓存中是空的或者是新的请求，那么这个线程将被重新创建,如果有很多新的线程， 
# 增加这个值可以改善系统性能.通过比较Connections和Threads_created状态的变量，可以看到这个变量的作用。(–>表示要调整的值) 
# 根据物理内存设置规则如下： 
# 1G —> 8 
# 2G —> 16 
# 3G —> 32 
# 大于3G —> 64

query_cache_size = 8M 
#MySQL的查询缓冲大小（从4.0.1开始，MySQL提供了查询缓冲机制）使用查询缓冲，MySQL将SELECT语句和查询结果存放在缓冲区中， 
# 今后对于同样的SELECT语句（区分大小写），将直接从缓冲区中读取结果。根据MySQL用户手册，使用查询缓冲最多可以达到238%的效率。 
# 通过检查状态值’Qcache_%’，可以知道query_cache_size设置是否合理：如果Qcache_lowmem_prunes的值非常大，则表明经常出现缓冲不够的情况， 
# 如果Qcache_hits的值也非常大，则表明查询缓冲使用非常频繁，此时需要增加缓冲大小；如果Qcache_hits的值不大，则表明你的查询重复率很低， 
# 这种情况下使用查询缓冲反而会影响效率，那么可以考虑不用查询缓冲。此外，在SELECT语句中加入SQL_NO_CACHE可以明确表示不使用查询缓冲

query_cache_limit = 2M 
#指定单个查询能够使用的缓冲区大小，默认1M

key_buffer_size = 4M 
#指定用于索引的缓冲区大小，增加它可得到更好处理的索引(对所有读和多重写)，到你能负担得起那样多。如果你使它太大， 
# 系统将开始换页并且真的变慢了。对于内存在4GB左右的服务器该参数可设置为384M或512M。通过检查状态值Key_read_requests和Key_reads， 
# 可以知道key_buffer_size设置是否合理。比例key_reads/key_read_requests应该尽可能的低， 
# 至少是1:100，1:1000更好(上述状态值可以使用SHOW STATUS LIKE ‘key_read%’获得)。注意：该参数值设置的过大反而会是服务器整体效率降低

ft_min_word_len = 4 
# 分词词汇最小长度，默认4

transaction_isolation = REPEATABLE-READ 
# MySQL支持4种事务隔离级别，他们分别是： 
# READ-UNCOMMITTED, READ-COMMITTED, REPEATABLE-READ, SERIALIZABLE. 
# 如没有指定，MySQL默认采用的是REPEATABLE-READ，ORACLE默认的是READ-COMMITTED

log_bin = mysql-bin 
binlog_format = mixed 
expire_logs_days = 30 #超过30天的binlog删除

log_error = /data/mysql/mysql-error.log #错误日志路径 
slow_query_log = 1 
long_query_time = 1 #慢查询时间 超过1秒则为慢查询 
slow_query_log_file = /data/mysql/mysql-slow.log

performance_schema = 0 
explicit_defaults_for_timestamp

#lower_case_table_names = 1 #不区分大小写

skip-external-locking #MySQL选项以避免外部锁定。该选项默认开启

default-storage-engine = InnoDB #默认存储引擎

innodb_file_per_table = 1 
# InnoDB为独立表空间模式，每个数据库的每个表都会生成一个数据空间 
# 独立表空间优点： 
# 1．每个表都有自已独立的表空间。 
# 2．每个表的数据和索引都会存在自已的表空间中。 
# 3．可以实现单表在不同的数据库中移动。 
# 4．空间可以回收（除drop table操作处，表空不能自已回收） 
# 缺点： 
# 单表增加过大，如超过100G 
# 结论： 
# 共享表空间在Insert操作上少有优势。其它都没独立表空间表现好。当启用独立表空间时，请合理调整：innodb_open_files

innodb_open_files = 500 
# 限制Innodb能打开的表的数据，如果库里的表特别多的情况，请增加这个。这个值默认是300

innodb_buffer_pool_size = 64M 
# InnoDB使用一个缓冲池来保存索引和原始数据, 不像MyISAM. 
# 这里你设置越大,你在存取表里面数据时所需要的磁盘I/O越少. 
# 在一个独立使用的数据库服务器上,你可以设置这个变量到服务器物理内存大小的80% 
# 不要设置过大,否则,由于物理内存的竞争可能导致操作系统的换页颠簸. 
# 注意在32位系统上你每个进程可能被限制在 2-3.5G 用户层面内存限制, 
# 所以不要设置的太高.

innodb_write_io_threads = 4 
innodb_read_io_threads = 4 
# innodb使用后台线程处理数据页上的读写 I/O(输入输出)请求,根据你的 CPU 核数来更改,默认是4 
# 注:这两个参数不支持动态改变,需要把该参数加入到my.cnf里，修改完后重启MySQL服务,允许值的范围从 1-64

innodb_thread_concurrency = 0 
# 默认设置为 0,表示不限制并发数，这里推荐设置为0，更好去发挥CPU多核处理能力，提高并发量

innodb_purge_threads = 1 
# InnoDB中的清除操作是一类定期回收无用数据的操作。在之前的几个版本中，清除操作是主线程的一部分，这意味着运行时它可能会堵塞其它的数据库操作。 
# 从MySQL5.5.X版本开始，该操作运行于独立的线程中,并支持更多的并发数。用户可通过设置innodb_purge_threads配置参数来选择清除操作是否使用单 
# 独线程,默认情况下参数设置为0(不使用单独线程),设置为 1 时表示使用单独的清除线程。建议为1

innodb_flush_log_at_trx_commit = 2 
# 0：如果innodb_flush_log_at_trx_commit的值为0,log buffer每秒就会被刷写日志文件到磁盘，提交事务的时候不做任何操作（执行是由mysql的master thread线程来执行的。 
# 主线程中每秒会将重做日志缓冲写入磁盘的重做日志文件(REDO LOG)中。不论事务是否已经提交）默认的日志文件是ib_logfile0,ib_logfile1 
# 1：当设为默认值1的时候，每次提交事务的时候，都会将log buffer刷写到日志。 
# 2：如果设为2,每次提交事务都会写日志，但并不会执行刷的操作。每秒定时会刷到日志文件。要注意的是，并不能保证100%每秒一定都会刷到磁盘，这要取决于进程的调度。 
# 每次事务提交的时候将数据写入事务日志，而这里的写入仅是调用了文件系统的写入操作，而文件系统是有 缓存的，所以这个写入并不能保证数据已经写入到物理磁盘 
# 默认值1是为了保证完整的ACID。当然，你可以将这个配置项设为1以外的值来换取更高的性能，但是在系统崩溃的时候，你将会丢失1秒的数据。 
# 设为0的话，mysqld进程崩溃的时候，就会丢失最后1秒的事务。设为2,只有在操作系统崩溃或者断电的时候才会丢失最后1秒的数据。InnoDB在做恢复的时候会忽略这个值。 
# 总结 
# 设为1当然是最安全的，但性能页是最差的（相对其他两个参数而言，但不是不能接受）。如果对数据一致性和完整性要求不高，完全可以设为2，如果只最求性能，例如高并发写的日志服务器，设为0来获得更高性能

innodb_log_buffer_size = 2M
# 此参数确定些日志文件所用的内存大小，以M为单位。缓冲区更大能提高性能，但意外的故障将会丢失数据。MySQL开发人员建议设置为1－8M之间

innodb_log_file_size = 32M 
# 此参数确定数据日志文件的大小，更大的设置可以提高性能，但也会增加恢复故障数据库所需的时间

innodb_log_files_in_group = 3 
# 为提高性能，MySQL可以以循环方式将日志文件写到多个文件。推荐设置为3

innodb_max_dirty_pages_pct = 90 
# innodb主线程刷新缓存池中的数据，使脏数据比例小于90%

innodb_lock_wait_timeout = 120 
# InnoDB事务在被回滚之前可以等待一个锁定的超时秒数。InnoDB在它自己的锁定表中自动检测事务死锁并且回滚事务。InnoDB用LOCK TABLES语句注意到锁定设置。默认值是50秒

bulk_insert_buffer_size = 8M 
# 批量插入缓存大小， 这个参数是针对MyISAM存储引擎来说的。适用于在一次性插入100-1000+条记录时， 提高效率。默认值是8M。可以针对数据量的大小，翻倍增加。

myisam_sort_buffer_size = 8M 
# MyISAM设置恢复表之时使用的缓冲区的尺寸，当在REPAIR TABLE或用CREATE INDEX创建索引或ALTER TABLE过程中排序 MyISAM索引分配的缓冲区

myisam_max_sort_file_size = 10G 
# 如果临时文件会变得超过索引，不要使用快速排序索引方法来创建一个索引。注释：这个参数以字节的形式给出

myisam_repair_threads = 1 
# 如果该值大于1，在Repair by sorting过程中并行创建MyISAM表索引(每个索引在自己的线程内)

interactive_timeout = 28800 
# 服务器关闭交互式连接前等待活动的秒数。交互式客户端定义为在mysql_real_connect()中使用CLIENT_INTERACTIVE选项的客户端。默认值：28800秒（8小时）

wait_timeout = 28800 
# 服务器关闭非交互连接之前等待活动的秒数。在线程启动时，根据全局wait_timeout值或全局interactive_timeout值初始化会话wait_timeout值， 
# 取决于客户端类型(由mysql_real_connect()的连接选项CLIENT_INTERACTIVE定义)。参数默认值：28800秒（8小时） 
# MySQL服务器所支持的最大连接数是有上限的，因为每个连接的建立都会消耗内存，因此我们希望客户端在连接到MySQL Server处理完相应的操作后， 
# 应该断开连接并释放占用的内存。如果你的MySQL Server有大量的闲置连接，他们不仅会白白消耗内存，而且如果连接一直在累加而不断开， 
# 最终肯定会达到MySQL Server的连接上限数，这会报’too many connections’的错误。对于wait_timeout的值设定，应该根据系统的运行情况来判断。 
# 在系统运行一段时间后，可以通过show processlist命令查看当前系统的连接状态，如果发现有大量的sleep状态的连接进程，则说明该参数设置的过大， 
# 可以进行适当的调整小些。要同时设置interactive_timeout和wait_timeout才会生效。

[mysqldump] 
quick 
max_allowed_packet = 16M #服务器发送和接受的最大包长度

[myisamchk] 
key_buffer_size = 8M 
sort_buffer_size = 8M 
read_buffer = 4M 
write_buffer = 4M
```


#### 第四部分

[来源网络](https://blog.csdn.net/bbwangj/article/details/83752142)
    
以下选项会被MySQL客户端应用读取。注意只有MySQL附带的客户端应用程序保证可以读取这段内容。如果你想你自己的MySQL应用程序获取这些值。需要在MySQL客户端库初始化的时候指定这些选项。

```
[client]
port = 3309
socket =  /usr/local/mysql/tmp/mysql.sock
[mysqld] #服务器端配置
!include  /usr/local/mysql/etc/mysqld.cnf  #包含的配置文件，可以把用户名和密码文件单独存放
port = 3306　　#监听端口　　
bind-address = 0.0.0.0　　#监听的ip地址
server-id = 1　　#MySQL服务的ID
socket =  /usr/local/mysql/tmp/mysql.sock　　#socket通信设置
pid-file =  /usr/local/mysql/var/mysql.pid　 #pid文件路径
basedir =  /usr/local/mysql/　　　　　　　　　　#MySQL程序路径
datadir =  /usr/local/mysql/data　　　　　　　 #数据目录
tmpdir =  /usr/local/mysql/tmp/ 
#此目录被 MySQL用来保存临时文件.例如,它被用来处理基于磁盘的大型排序,和内部排序一样，以及简单的临时表.如果你不创建非常大的临时文件,将其放置到 swapfs/tmpfs 文件系统上也许比较好。另一种选择是你也可以将其放置在独立的磁盘上.你可以使用”;”来放置多个路径，他们会按照 roud-robin 方法被轮询使用.

slave-load-tmpdir =  /usr/local/mysql/tmp/  #当slave执行load data infile时使用
#*** skip options 相关选项 ***#
skip-name-resolve 
#禁止 MySQL 对外部连接进行 DNS 解析，使用这一选项可以消除 MySQL 进行 DNS 解析的时间。但需要注意，如果开启该选项，则所有远程主机连接授权都要使用 IP 地址方式，否则 MySQL 将无法正常处理连接请求！
skip-symbolic-links 
#不能使用连接文件，多个客户可能会访问同一个数据库，因此这防止外部客户锁定 MySQL 服务器。 该选项默认开启

skip-external-locking 
#不使用系统锁定，要使用 myisamchk,必须关闭服务器 ,避免 MySQL的外部锁定，减少出错几率增强稳定性。

skip-slave-start 
#启动 mysql,不启动复制

skip-networking 
#开启该选项可以彻底关闭 MySQL 的 TCP/IP 连接方式，如果 WEB 服务器是以远程连接的方式访问 MySQL 数据库服务器则不要开启该选项！否则将无法正常连接！ 如果所有的进程都是在同一台服务器连接到本地的 mysqld, 这样设置将是增强安全的方法

sysdate-is-now = 1 
#把SYSDATE 函数编程为 NOW的别名

#*** 系统资源相关选项 ***#
back_log = 50 
#接受队列，对于没建立 tcp 连接的请求队列放入缓存中，队列大小为 back_log，受限制与 OS 参数，试图设定 back_log 高于你的操作系统的限制将是无效的。默认值为 50。对于 Linux 系统推荐设置为小于512的整数。如果系统在一个短时间内有很多连接，则需要增大该参数的值

max_connections = 1000 
#指定MySQL允许的最大连接进程数。如果在访问数据库时经常出现"Too Many Connections"的错误提 示，则需要增大该参数值。

max_connect_errors = 10000 
#如果某个用户发起的连接 error 超过该数值，则该用户的下次连接将被阻塞，直到管理员执行 flush hosts ; 命令或者服务重启， 防止黑客 ， 非法的密码以及其他在链接时的错误会增加此值

open_files_limit = 10240 
#MySQL打开的文件描述符限制，默认最小1024;当open_files_limit没有被配置的时候，比较max_connections*5和ulimit-n的值，哪个大用哪个，当open_file_limit被配置的时候，比较open_files_limit和max_connections*5的值，哪个大用哪个。

connect-timeout = 10 
#连接超时之前的最大秒数,在 Linux 平台上，该超时也用作等待服务器首次回应的时间

wait-timeout = 28800 
#等待关闭连接的时间

interactive-timeout = 28800 
#关闭连接之前，允许 interactive_timeout（取代了wait_timeout）秒的不活动时间。客户端的会话 wait_timeout 变量被设为会话interactive_timeout 变量的值。如果前端程序采用短连接，建议缩短这2个值, 如果前端程序采用长连接，可直接注释掉这两个选项，默认配置(8小时)  

slave-net-timeout = 600 
#从服务器也能够处理网络连接中断。但是，只有从服务器超过slave_net_timeout 秒没有从主服务器收到数据才通知网络中断

net_read_timeout = 30 
#从服务器读取信息的超时

net_write_timeout = 60 
#从服务器写入信息的超时

net_retry_count = 10 
#如果某个通信端口的读操作中断了，在放弃前重试多次

net_buffer_length = 16384 
#包消息缓冲区初始化为 net_buffer_length 字节，但需要时可以增长到 max_allowed_packet 字节

max_allowed_packet = 64M
# 服务所能处理的请求包的最大大小以及服务所能处理的最大的请求大小(当与大的BLOB 字段一起工作时相当必要)， 每个连接独立的大小.大小动态增加。 设置最大包,限制server接受的数据包大小，避免超长SQL的执行有问题 默认值为16M，当MySQL客户端或mysqld
服务器收到大于 max_allowed_packet 字节的信息包时，将发出“信息包过大”错误，并关闭连接。对于某些客户端，如果通信信息包过大，在执行查询期间，可能会遇到“丢失与 MySQL 服务器的连接”错误。默认值 16M。

table_cache = 512 
# 所有线程所打开表的数量. 增加此值就增加了mysqld所需要的文件描述符的数量这样你需要确认在[mysqld_safe]中 “open-files-limit” 变量设置打开文件数量允许至少4096

thread_stack = 192K 
# 线程使用的堆大小. 此容量的内存在每次连接时被预留.MySQL 本身常不会需要超过 64K 的内存如果你使用你自己的需要大量堆的 UDF 函数或者你的操作系统对于某些操作需要更多的堆,你也许需要将其设置的更高一点.默认设置足以满足大多数应用

thread_cache_size = 20 
# 我们在 cache 中保留多少线程用于重用.当一个客户端断开连接后,如果 cache 中的线程还少于 thread_cache_size,则客户端线程被放入 cache 中.这可以在你需要大量新连接的时候极大的减少线程创建的开销(一般来说如果你有好的线程模型的话,
这不会有明显的性能提升.)服务器线程缓存这个值表示可以重新利用保存在缓存中线程的数量,当断开连接时如果缓存中还有空间,那么客户端的线程将被放到缓存中,如果线程重新被请求，那么请求将从缓存中读取,如果缓存中是空的或者是新的请求，那么这个线程将被重新创建,
如果有很多新的线程，增加这个值可以改善系统性能.通过比较 Connections 和 Threads_created 状态的变量，可以看到这个变量的作用
根据物理内存设置规则如下：
1G  —> 8
2G  —> 16
3G  —> 32
大于3G  —> 64

thread_concurrency = 8 
#此允许应用程序给予线程系统一个提示在同一时间给予渴望被运行的线程的数量.该参数取值为服务器逻辑CPU数量×2，在本例中，服务器有 2 颗物理CPU，而每颗物理CPU又支持H.T超线程，所以实际取值为 4 × 2 ＝ 8.设置 thread_concurrency的值的正确与否, 
对 mysql 的性能影响很大, 在多个 cpu(或多核)的情况下，错误设置了 thread_concurrency 的值, 会导致 mysql 不能充分利用多 cpu(或多核),出现同一时刻只能一个 cpu(或核)在工作的情况。 thread_concurrency 应设为 CPU 核数的 2 倍.比如有一个双核的 CPU, 
那么 thread_concurrency 的应该为 4; 2 个双核的 cpu,thread_concurrency 的值应为 8,属重点优化参数
 
 
#*** qcache settings 相关选项 ***#
query_cache_limit = 2M 
#不缓存查询大于该值的结果.只有小于此设定值的结果才会被缓冲,  此设置用来保护查询缓冲,防止一个极大的结果集将其他所有的查询结果都覆盖.

query_cache_min_res_unit = 2K 
#查询缓存分配的最小块大小.默认是 4KB，设置值大对大数据查询有好处，但如果你的查询都是小数据查询，就容易造成内存碎片和浪费
查询缓存碎片率 = Qcache_free_blocks / Qcache_total_blocks * 100%
如果查询缓存碎片率超过 20%，可以用 FLUSH QUERY CACHE 整理缓存碎片，或者试试减小query_cache_min_res_unit，如果你的查询都是小数据量的话。
查询缓存利用率 = (query_cache_size – Qcache_free_memory) / query_cache_size *100%
查询缓存利用率在 25%以下的话说明 query_cache_size 设置的过大，可适当减小;查询缓存利用率在 80%以上而且 Qcache_lowmem_prunes > 50 的话说明 query_cache_size 可能有点小，要不就是碎片太多。
查询缓存命中率 = (Qcache_hits – Qcache_inserts) / Qcache_hits * 100%

query_cache_size = 64M  
#指定 MySQL 查询缓冲区的大小。可以通过在 MySQL 控制台执行以下命令观察：
代码:
> SHOW VARIABLES LIKE '%query_cache%';
> SHOW STATUS LIKE 'Qcache%';如果 Qcache_lowmem_prunes 的值非常大，则表明经常出现缓冲不够的情况；
如果 Qcache_hits 的值非常大，则表明查询缓冲使用非常频繁，如果该值较小反而会影响效率，那么可以考虑不用查询缓冲； Qcache_free_blocks，如果该值非常大，则表明缓冲区中碎片很多。
memlock # 如果你的系统支持 memlock() 函数,你也许希望打开此选项用以让运行中的 mysql 在在内存高度
紧张的时候,数据在内存中保持锁定并且防止可能被 swapping out,此选项对于性能有益

#*** default settings 相关选项 ***#
default_table_type = InnoDB 
# 当创建新表时作为默认使用的表类型,如果在创建表示没有特别执行表类型,将会使用此值

default-time-zone = system 
#服务器时区

character-set-server = utf8 
#server 级别字符集

default-storage-engine = InnoDB 
#默认存储引擎

#*** tmp && heap settings 相关选项 ***#
tmp_table_size = 512M 
#临时表的最大大小，如果超过该值，则结果放到磁盘中,此限制是针对单个表的,而不是总和.

max_heap_table_size = 512M 
#独立的内存表所允许的最大容量.此选项为了防止意外创建一个超大的内存表导致永尽所有的内存资源.

#*** log settings 相关选项 ***#
log-bin = mysql-bin 
#打开二进制日志功能.在复制(replication)配置中,作为 MASTER 主服务器必须打开此项.如果你需要从你最后的备份中做基于时间点的恢复,你也同样需要二进制日志.这些路径相对于 datadir

log_slave_updates = 1 
#表示slave将复制事件写进自己的二进制日志

log-bin-index = mysql-bin.index 
#二进制的索引文件名

relay-log = relay-log 
#定义relay_log的位置和名称，如果值为空，则默认位置在数据文件的目录，文件名为host_name-relay-bin.nnnnnn（By default, relay log file names have the form host_name-relay-bin.nnnnnn in the data directory）；

relay_log_index = relay-log.index  
#relay-log的索引文件名

log-warnings = 1 
# 将警告打印输出到错误 log 文件.如果你对于MySQL有任何问题，你应该打开警告 log 并且仔细审查错误日志,查出可能的原因.

log-error =  /usr/local/mysql/log/mysql.err 
#错误日志路径

log_output = FILE 
#参数 log_output 指定了慢查询输出的格式，默认为 FILE，你可以将它设为 TABLE，然后就可以查询 mysql 架构下的 slow_log 表了

log_slow_queries 
#指定是否开启慢查询日志(该参数要被slow_query_log取代，做兼容性保留)

slow_query_log = 1 
# 指定是否开启慢查询日志. 慢查询是指消耗了比 “long_query_time” 定义的更多时间的查询.如果 log_long_format 被打开,那些没有使用索引的查询也会被记录.如果你经常增加新查询到已有的系统内的话. 一般来说这是一个好主意,

long-query-time = 1 
#设定慢查询的阀值，超出次设定值的SQL即被记录到慢查询日志，缺省值为10s.所有的使用了比这个时间(以秒为单位)更多的查询会被认为是慢速查询.不要在这里使用”1″, 否则会导致所有的查询,甚至非常快的查询页被记录下来(由于MySQL 目前时间的精确度只能达到秒的级别).

log_long_format 
# 在慢速日志中记录更多的信息.一般此项最好打开，打开此项会记录使得那些没有使用索引的查询也被作为到慢速查询附加到慢速日志里

slow_query_log_file =  /usr/local/mysql/log/slow.log 
# 指定慢日志文件存放位置，可以为空，系统会给一个缺省的文件host_name-slow.log

log-queries-not-using-indexes 
#如果运行的SQL语句没有使用索引，则mysql数据库同样会将这条SQL语句记录到慢查询日志文件中。

min_examined_row_limit=1000　　　　
#记录那些由于查找了多余1000次而引发的慢查询

long-slow-admin-statements　　　　
#记录那些慢的optimize table，analyze table和alter table语句

log-slow-slave-statements 
#记录由Slave所产生的慢查询

general_log = 1 
#将所有到达MySQL Server的SQL语句记录下来,默认关闭 

general_log_file =  /usr/local/mysql/log/mysql.log 
#general_log路径

max_binlog_size = 1G 
#如果二进制日志写入的内容超出给定值，日志就会发生滚动。你不能将该变量设置为大于1GB或小于4096字节。 默认值是1GB。如果你正使用大的事务，二进制日志还会超过max_binlog_size

max_relay_log_size = 1G 
#标记relaylog允许的最大值，如果该值为0，则默认值为max_binlog_size(1G)；如果不为0，则max_relay_log_size则为最大的relay_log文件大小；

relay-log-purge = 1 
#是否自动清空不再需要中继日志时。默认值为1(启用)

expire_logs_days = 30 
#超过 30 天的 binlog 删除

binlog_cache_size = 1M 
# 在一个事务中 binlog 为了记录 SQL 状态所持有的 cache 大小,如果你经常使用大的,多声明的事务,你可以增加此值来获取更大的性能.所有从事务来的状态都将被缓冲在 binlog 缓冲中然后在提交后一次性写入到 binlog 中,如果事务比此值大, 会使用磁盘上的临时文件来替代.此缓冲在每个连接的事务第一次更新状态时被创建.session 级别

replicate-wild-ignore-table = mysql.% 
#复制时忽略数据库及表
slave_skip_errors=all 
#定义复制过程中从服务器可以自动跳过的错误号，当复制过程中遇到定义的错误号，就可以自动跳过，直接执行后面的SQL语句。
slave_skip_errors选项有四个可用值，分别为：off，all，ErorCode，ddl_exist_errors。
  默认情况下该参数值是off，我们可以列出具体的error code，也可以选择all，mysql5.6及MySQL Cluster NDB 7.3以及后续版本增加了参数ddl_exist_errors，该参数包含一系列error code（1007,1008,1050,1051,1054,1060,1061,1068,1094,1146）
    一些error code代表的错误如下：
    1007：数据库已存在，创建数据库失败
    1008：数据库不存在，删除数据库失败
    1050：数据表已存在，创建数据表失败
    1051：数据表不存在，删除数据表失败
    1054：字段不存在，或程序文件跟数据库有冲突
    1060：字段重复，导致无法插入
    1061：重复键名
    1068：定义了多个主键
    1094：位置线程ID
    1146：数据表缺失，请恢复数据库
    1053：复制过程中主服务器宕机
    1062：主键冲突 Duplicate entry '%s' for key %d
    
    
#*** MyISAM 相关选项 ***#
key_buffer_size = 256M 
#指定用于索引的缓冲区大小，增加它可得到更好的索引处理性能。如果是以InnoDB引擎为主的DB，专用于MyISAM引擎的 key_buffer_size 可以设置较小，8MB 已足够  如果是以MyISAM引擎为主，可设置较大，但不能超过4G. 在这里，强烈建议不使用MyISAM引擎，默认都是用InnoDB引擎.注意：该参数值设置的过大反而会是服务器整体效率降低！

sort_buffer_size = 2M 
#查询排序时所能使用的缓冲区大小。排序缓冲被用来处理类似 ORDER BY 以及 GROUP BY 队列所引起的排序.一个用来替代的基于磁盘的合并分类会被使用.查看 “Sort_merge_passes” 状态变量. 在排序发生时由每个线程分配 注意：该参数对应的分配内存是每连接独占！如果有 100 个连接，那么实际分配的总共排序缓冲区大小为 100 × 6 ＝600MB,所以,对于内存在 4GB 左右的服务器推荐设置为 6-8M。 

read_buffer_size = 2M 
#读查询操作所能使用的缓冲区大小。和 sort_buffer_size 一样，该参数对应的分配内存也是每连接独享！用来做 MyISAM 表全表扫描的缓冲大小.当全表扫描需要时,在对应线程中分配.

join_buffer_size = 8M 
#联合查询操作所能使用的缓冲区大小，和 sort_buffer_size 一样，该参数对应的分配内存也是每连接独享!此缓冲被使用来优化全联合(full JOINs 不带索引的联合).类似的联合在极大多数情况下有非常糟糕的性能表现, 但是将此值设大能够减轻性能影响.通过 “Select_full_join”状态变量查看全联合的数量， 当全联合发生时,在每个线程中分配。

read_rnd_buffer_size = 8M 
#MyISAM 以索引扫描(Random Scan)方式扫描数据的 buffer大小 

bulk_insert_buffer_size = 64M 
#MyISAM 使用特殊的类似树的 cache 来使得突发插入(这些插入是,INSERT … SELECT, INSERT … VALUES (…), (…), …, 以及 LOAD DATAINFILE) 更快. 此变量限制每个进程中缓冲树的字节数.设置为 0 会关闭此优化.为了最优化不要将此值设置大于 “key_buffer_size”.当突发插入被检测到时此缓冲将被分配MyISAM 用在块插入优化中的树缓冲区的大小。注释：这是一个 per thread 的限制 （ bulk 大量）.此缓冲当 MySQL 需要在 REPAIR, OPTIMIZE, ALTER 以及 LOAD DATA INFILE到一个空表中引起重建索引时被分配.这在每个线程中被分配.所以在设置大值时需要小心.

myisam_sort_buffer_size = 64M 
#MyISAM 设置恢复表之时使用的缓冲区的尺寸,当在REPAIR TABLE 或用 CREATE INDEX 创建索引或 ALTER TABLE 过程中排序 MyISAM 索引分配的缓冲区

myisam_max_sort_file_size = 10G
#mysql重建索引时允许使用的临时文件最大大小

myisam_repair_threads = 1 
#如果该值大于 1，在 Repair by sorting 过程中并行创建MyISAM 表索引(每个索引在自己的线程内).如果一个表拥有超过一个索引, MyISAM 可以通过并行排序使用超过一个线程去修复他们.这对于拥有多个 CPU 以及大量内存情况的用户,是一个很好的选择.

myisam_recover = 64K
#允许的 GROUP_CONCAT()函数结果的最大长度
transaction_isolation = REPEATABLE-READ # 设定默认的事务隔离级别.可用的级别如下:READ-UNCOMMITTED, READ-COMMITTED, REPEATABLE-READ,SERIALIZABLE
1.READ UNCOMMITTED-读未提交 2.READ COMMITTE-读已提交 3.REPEATABLE READ -可重复读 4.SERIALIZABLE -串行

# *** INNODB 相关选项 ***#
skip-innodb 
# 如果你的 MySQL 服务包含 InnoDB 支持但是并不打算使用的话,使用此选项会节省内存以及磁盘空间,并且加速某些部分

innodb_file_per_table = 1 
# InnoDB为独立表空间模式，每个数据库的每个表都会生成一个数据空间
独立表空间优点：
1．每个表都有自已独立的表空间。
2．每个表的数据和索引都会存在自已的表空间中。
3．可以实现单表在不同的数据库中移动。
4．空间可以回收（除drop table操作处，表空不能自已回收）
缺点：
1.单表增加过大，如超过100G
结论：
共享表空间在Insert操作上少有优势。其它都没独立表空间表现好。当启用独立表空间时，请合理调整：innodb_open_files

innodb_status_file = 1 
#启用InnoDB的status file，便于管理员查看以及监控等

innodb_open_files = 2048 
# 限制Innodb能打开的表的数据，如果库里的表特别多的情况，请增加这个。这个值默认是300

innodb_additional_mem_pool_size = 100M 
#设置InnoDB存储引擎用来存放数据字典信息以及一些内部数据结构的内存空间大小，所以当我们一个MySQL Instance中的数据库对象非常多的时候，是需要适当调整该参数的大小以确保所有数据都能存放在内存中提高访问效率的。 

innodb_buffer_pool_size = 2G 
#包括数据页、索引页、插入缓存、锁信息、自适应哈希所以、数据字典信息.InnoDB 使用一个缓冲池来保存索引和原始数据, 不像 MyISAM.这里你设置越大,你在存取表里面数据时所需要的磁盘 I/O 越少.在一个独立使用的数据库服务器上,你可以设置这个变量到服务器物理内存大小的 80%,不要设置过大,否则,由于物理内存的竞争可能导致操作系统的换页颠簸.注意在 32 位系统上你每个进程可能被限制在 2-3.5G 用户层面内存限制,所以不要设置的太高.

innodb_write_io_threads = 4
innodb_read_io_threads = 4
# innodb使用后台线程处理数据页上的读写 I/O(输入输出)请求,根据你的 CPU 核数来更改,默认是4
# 注:这两个参数不支持动态改变,需要把该参数加入到my.cnf里，修改完后重启MySQL服务,允许值的范围从 1-64

innodb_data_home_dir =  /usr/local/mysql/var/ 
#设置此选项如果你希望 InnoDB 表空间文件被保存在其他分区.默认保存在 MySQL 的 datadir 中.

innodb_data_file_path = ibdata1:500M;ibdata2:2210M:autoextend
#InnoDB将数据保存在一个或者多个数据文件中成为表空间.如果你只有单个逻辑驱动保存你的数据,一个单个的自增文件就足够好了.其他情况下.每个设备一个文件一般都是个好的选择.你也可以配置 InnoDB 来使用裸盘分区 – 请参考手册来获取更多相关内容

innodb_file_io_threads = 4 
#用来同步 IO 操作的 IO 线程的数量. 此值在 Unix 下被硬编码为 4,但是在 Windows 磁盘 I/O 可能在一个大数值下表现的更好.

innodb_thread_concurrency = 16
#在 InnoDb 核心内的允许线程数量,InnoDB 试着在 InnoDB 内保持操作系统线程的数量少于或等于这个参数给出的限制,最优值依赖于应用程序,硬件以及操作系统的调度方式.过高的值可能导致线程的互斥颠簸.默认设置为 0,表示不限制并发数，这里推荐设置为0，更好去发挥CPU多核处理能力，提高并发量

innodb_flush_log_at_trx_commit = 1 
#如果设置为 1 ,InnoDB 会在每次提交后刷新(fsync)事务日志到磁盘上,这提供了完整的 ACID 行为.如果你愿意对事务安全折衷, 并且你正在运行一个小的食物, 你可以设置此值到 0 或者 2 来减少由事务日志引起的磁盘 I/O
0 代表日志只大约每秒写入日志文件并且日志文件刷新到磁盘.
2 代表日志写入日志文件在每次提交后,但是日志文件只有大约每秒才会刷新到磁盘上.

innodb_log_buffer_size = 8M 
#用来缓冲日志数据的缓冲区的大小.当此值快满时, InnoDB 将必须刷新数据到磁盘上.由于基本上每秒都会刷新一次,所以没有必要将此值设置的太大(甚至对于长事务而言)

innodb_log_file_size = 500M 
#事物日志大小.在日志组中每个日志文件的大小，你应该设置日志文件总合大小到你缓冲池大小的5%~100%，来避免在日志文件覆写上不必要的缓冲池刷新行为.不论如何, 请注意一个大的日志文件大小会增加恢复进程所需要的时间.

innodb_log_files_in_group = 2 
#在日志组中的文件总数.通常来说 2~3 是比较好的.

innodb_log_group_home_dir =  /usr/local/mysql/var/
# InnoDB 的日志文件所在位置. 默认是 MySQL 的 datadir.你可以将其指定到一个独立的硬盘上或者一个 RAID1 卷上来提高其性能innodb_max_dirty_pages_pct = 90 #innodb 主线程刷新缓存池中的数据，使脏数据比例小于 90%,这是一个软限制,不被保证绝对执行.

innodb_lock_wait_timeout = 50 
#InnoDB 事务在被回滚之前可以等待一个锁定的超时秒数。InnoDB 在它自己的 锁定表中自动检测事务死锁并且回滚事务。 InnoDB 用 LOCK TABLES 语句注意到锁定设置。默认值是 50 秒

innodb_flush_method = O_DSYNC 
# InnoDB 用来刷新日志的方法.表空间总是使用双重写入刷新方法.默认值是 “fdatasync”, 另一个是 “O_DSYNC”.

innodb_force_recovery=1
# 如果你发现 InnoDB 表空间损坏, 设置此值为一个非零值可能帮助你导出你的表.从1 开始并且增加此值知道你能够成功的导出表.

innodb_fast_shutdown 
# 加速 InnoDB 的关闭. 这会阻止 InnoDB 在关闭时做全清除以及插入缓冲合并.这可能极大增加关机时间, 但是取而代之的是 InnoDB 可能在下次启动时做这些操作.

# *** 其他 相关选项 ***#
[mysqldump]
quick 
#支持较大数据库的转储，在导出非常巨大的表时需要此项。增加该变量的值十分安全，这是因为仅当需要时才会分配额外内存。例如，仅当你发出长查询或mysqld必须返回大的结果行时mysqld才会分配更多内存。该变量之所以取较小默认值是一种预防措施，以捕获客户端和服务器之间的错误信息包，并确保不会因偶然使用大的信息包而导致内存溢出。 如果你正是用大的BLOB值，而且未为mysqld授予为处理查询而访问足够内存的权限，也会遇到与大信息包有关的奇怪问题。如果怀疑出现了该情况，请尝试在mysqld_safe脚本开始增加ulimit -d 256000，并重启mysqld。

[mysql]
auto-rehash 
#允许通过 TAB 键提示

default-character-set = utf8 
#数据库字符集

connect-timeout = 3
[mysqld_safe]

open-files-limit = 8192 
#增加每个进程的可打开文件数量.确认你已经将全系统限制设定的足够高!打开大量表需要将此值设大
```

#### 第五部分

[来源网络](https://wuguiyunwei.com/index.php/2016/09/21/319.html)

```
[client]

port = 3306

socket = /tmp/mysql.sock

default-character-set = utf8mb4
# 支持utf8mb4编码

[mysql]

prompt="MySQL [\d]> "
#登录数据库后显示当前位置

auto-rehash
#开启数据库tab补全


on-auto-rehash
#关闭数据库tab补全

[mysqld]

port = 3306
#监听端口设置

socket = /tmp/mysql.sock
#指定sock存放位置

basedir = /usr/local/mysql
#Mysql的安装路径

datadir = /samba/mysql
#Mysql的数据库存放路径

pid-file = /samba/mysql/mysql.pid
#Mysql的进程文存放位置

user = mysql
#Mysql使用的用户

bind-address = 0.0.0.0
#允许所有人连接根据 可以需求设置

server-id = 1
#Mysql的server id 根据需求修改

init-connect = 'SET NAMES utf8mb4'
character-set-server = utf8mb4
#utf8mb4编码是utf8编码的超集，兼容utf8，并且能存储4字节的表情字符

skip-name-resolve
# 禁止MySQL对外部连接进行DNS解析，使用这一选项可以消除MySQL进行DNS解析的时间。但需要注意，如果开启该选项，
则所有远程主机连接授权都要使用IP地址方式，否则MySQL将无法正常处理连接请求

#skip-networking
#关闭MySQL的TCP/IP连接方式

back_log = 300
# MySQL能有的连接数量。当主要MySQL线程在一个很短时间内得到非常多的连接请求，这就起作用，
然后主线程花些时间(尽管很短)检查连接并且启动一个新线程。back_log值指出在MySQL暂时停止回答新请求之前的短时间内多少个请求可以被存在堆栈中。
如果期望在一个短时间内有很多连接，你需要增加它。也就是说，如果MySQL的连接数据达到max_connections时，新来的请求将会被存在堆栈中，
以等待某一连接释放资源，该堆栈的数量即back_log，如果等待连接的数量超过back_log，将不被授予连接资源。
另外，这值（back_log）限于您的操作系统对到来的TCP/IP连接的侦听队列的大小。
你的操作系统在这个队列大小上有它自己的限制（可以检查你的OS文档找出这个变量的最大值），试图设定back_log高于你的操作系统的限制将是无效的。

max_connections = 2568
#设置Mysql的最大连接数

max_connect_errors = 100
#防止暴力破解超过100次后禁止连接 成功连接一次后会清零

open_files_limit = 65535
#设置Mysql打开文件数

table_open_cache = 1024
#设置缓存表的最大数目

max_allowed_packet = 500M
#限制插入和更新最大值

binlog_cache_size = 1M
#设置binlog使用内存大小（事务）

max_heap_table_size = 8M
#Mysql内存表容量设置

tmp_table_size = 128M
#增加临时表的大小设置

read_buffer_size = 2M
#Mysql读入缓冲区大小设置

read_rnd_buffer_size = 8M
#Mysql随机读缓冲区大小设置

sort_buffer_size = 8M
# MySQ需要排序 会话 的缓存大小

join_buffer_size = 8M
#表间关联缓存的大小

key_buffer_size = 256M
#指定用于索的缓存区大小

thread_cache_size = 64
#用来缓存空闲线程

query_cache_type = 1
#给所有查询做缓存

query_cache_size = 64M
#指定Mysql查询缓冲区的大小

query_cache_limit = 2M
#指定单个查询能够使用的缓冲区大小

ft_min_word_len = 4
# MyISAM 引擎表全文索引包含的最小词长度

log_bin = mysql-bin
#开启binlog

binlog_format = mixed
#使用mixed日志格式

expire_logs_days = 7
#binlog过期清理时间

log_error = /samba/mysql/mysql-error.log
#错误日志指定

slow_query_log = 1
#开启慢查询

long_query_time = 1
#超过1秒的SQL会记录到下面的日志文件
slow_query_log_file = /samba/mysql/mysql-slow.log

performance_schema = 0
#用于收集数据库服务器性能（修改之后需要重新启动mysql）

explicit_defaults_for_timestamp
#lower_case_table_names = 1

skip-external-locking
#用于多进程条件下为MyISAM数据表进行锁定

default_storage_engine = InnoDB
#默认开启innoDB存储引擎

#default-storage-engine = MyISAM

#MyiSAM

innodb_file_per_table = 1
#innoDB为独立表空间模式，每个数据库的每个表都会生成一个数据空间

innodb_open_files = 500
#限制innodb能打开的数据表

innodb_buffer_pool_size = 1024M
#设置越大，在存取表的时候所需要的I/O越少&nbsp; 根据服务器情况设置

innodb_write_io_threads = 4
innodb_read_io_threads = 4
# innodb使用后台线程处理数据页上的读写 I/O请求,根据 CPU 核数设置

innodb_thread_concurrency = 0
#0表示不限制并发链接数

innodb_purge_threads = 1
# InnoDB中的清除操作是一类定期回收无用数据的操作，
#默认情况下参数设置为0(不使用单独线程)，1 时表示使用单独的清除线程

innodb_flush_log_at_trx_commit = 2
# 0：如果innodb_flush_log_at_trx_commit的值为0,log buffer每秒就会被刷写日志文件到磁盘，提交事务的时候不做任何操作（执行是由mysql的master thread线程来执行的。
主线程中每秒会将重做日志缓冲写入磁盘的重做日志文件(REDO LOG)中。不论事务是否已经提交）默认的日志文件是ib_logfile0,ib_logfile1

1：当设为默认值1的时候，每次提交事务的时候，都会将log buffer刷写到日志。
2：如果设为2,每次提交事务都会写日志，但并不会执行刷的操作。每秒定时会刷到日志文件。要注意的是，并不能保证100%每秒一定都会刷到磁盘，这要取决于进程的调度。
每次事务提交的时候将数据写入事务日志，而这里的写入仅是调用了文件系统的写入操作，而文件系统是有 缓存的，所以这个写入并不能保证数据已经写入到物理磁盘
默认值1是为了保证完整的ACID。当然，你可以将这个配置项设为1以外的值来换取更高的性能，但是在系统崩溃的时候，你将会丢失1秒的数据。
设为0的话，mysqld进程崩溃的时候，就会丢失最后1秒的事务。设为2,只有在操作系统崩溃或者断电的时候才会丢失最后1秒的数据。InnoDB在做恢复的时候会忽略这个值。

总结
设为1当然是最安全的，但性能页是最差的（相对其他两个参数而言，但不是不能接受）。如果对数据一致性和完整性要求不高，完全可以设为2，如果只最求性能，例如高并发写的日志服务器，设为0来获得更高性能

innodb_log_buffer_size = 2M
# 此参数确定些日志文件所用的内存大小，以M为单位。缓冲区更大能提高性能，但意外的故障将会丢失数据。

innodb_log_file_size = 32M
# 此参数确定数据日志文件的大小，更大的设置可以提高性能，但也会增加恢复故障数据库所需的时间

innodb_log_files_in_group = 3
# 为提高性能，MySQL可以以循环方式将日志文件写到多个文件。

innodb_max_dirty_pages_pct = 90
# innodb主线程刷新缓存池中的数据，使脏数据比例小于90%

innodb_lock_wait_timeout = 120
# InnoDB事务在被回滚之前可以等待一个锁定的超时秒数。InnoDB在它自己的锁定表中自动检测事务死锁并且回滚事务。InnoDB用LOCK TABLES语句注意到锁定设置。默认值是50秒

bulk_insert_buffer_size = 8M
# 批量插入缓存大小， 这个参数是针对MyISAM存储引擎来说的。适用于在一次性插入100-1000+条记录时， 提高效率。默认值是8M。可以针对数据量的大小，翻倍增加。

myisam_sort_buffer_size = 64M

# MyISAM设置恢复表之时使用的缓冲区的尺寸，当在REPAIR TABLE或用CREATE INDEX创建索引或ALTER TABLE过程中排序 MyISAM索引分配的缓冲区

myisam_max_sort_file_size = 10G
# 如果临时文件会变得超过索引，不要使用快速排序索引方法来创建一个索引。注释：这个参数以字节的形式给出

myisam_repair_threads = 1
# 如果该值大于1，在Repair by sorting过程中并行创建MyISAM表索引(每个索引在自己的线程内)

interactive_timeout = 28800
# 服务器关闭交互式连接前等待活动的秒数。交互式客户端定义为在mysql_real_connect()中使用CLIENT_INTERACTIVE选项的客户端。默认值：28800秒（8小时）

wait_timeout = 28800
# 服务器关闭非交互连接之前等待活动的秒数。在线程启动时，根据全局wait_timeout值或全局interactive_timeout值初始化会话wait_timeout值，
取决于客户端类型(由mysql_real_connect()的连接选项CLIENT_INTERACTIVE定义)。参数默认值：28800秒（8小时）
MySQL服务器所支持的最大连接数是有上限的，因为每个连接的建立都会消耗内存，因此我们希望客户端在连接到MySQL Server处理完相应的操作后，
应该断开连接并释放占用的内存。如果你的MySQL Server有大量的闲置连接，他们不仅会白白消耗内存，而且如果连接一直在累加而不断开，
最终肯定会达到MySQL Server的连接上限数，这会报'too many connections'的错误。对于wait_timeout的值设定，应该根据系统的运行情况来判断。
在系统运行一段时间后，可以通过show processlist命令查看当前系统的连接状态，如果发现有大量的sleep状态的连接进程，则说明该参数设置的过大，
可以进行适当的调整小些。要同时设置interactive_timeout和wait_timeout才会生效。

[mysqldump]

quick

max_allowed_packet = 500M
#服务器发送和接受的最大包长度

[myisamchk]

key_buffer_size = 256M

sort_buffer_size = 8M

read_buffer = 4M

write_buffer = 4M

#skip-grant-tables
#跳过授权表 忘记密码root密码时添加此选项

#innodb_force_recovery 配置项讲解
innodb_force_recovery影响整个InnoDB存储引擎的恢复状况。默认为0，表示当需要恢复时执行所有的恢复操作（即校验数据页/purge undo/insert buffer merge/rolling back&forward），当不能进行有效的恢复操作时，mysql有可能无法启动，并记录错误日志；
innodb_force_recovery可以设置为1-6,大的数字包含前面所有数字的影响。当设置参数值大于0后，可以对表进行select,create,drop操作,但insert,update或者delete这类操作是不允许的。
1(SRV_FORCE_IGNORE_CORRUPT):忽略检查到的corrupt页。
2(SRV_FORCE_NO_BACKGROUND):阻止主线程的运行，如主线程需要执行full purge操作，会导致crash。
3(SRV_FORCE_NO_TRX_UNDO):不执行事务回滚操作。
4(SRV_FORCE_NO_IBUF_MERGE):不执行插入缓冲的合并操作。
5(SRV_FORCE_NO_UNDO_LOG_SCAN):不查看重做日志，InnoDB存储引擎会将未提交的事务视为已提交。
6(SRV_FORCE_NO_LOG_REDO):不执行前滚的操作。
```

#### 第六部分

[来源网络](https://www.jianshu.com/p/5f39c486561b)

```
# 客户端设置
[client]
port = 3306
# 默认情况下，socket文件应为/usr/local/mysql/mysql.socket,所以可以ln -s xx  /tmp/mysql.sock
socket = /tmp/mysql.sock 

# 服务端设置
[mysqld]

##########################################################################################################
# 基础信息
#Mysql服务的唯一编号 每个mysql服务Id需唯一
server-id = 1

#服务端口号 默认3306
port = 3306

# 启动mysql服务进程的用户
user = mysql

##########################################################################################################
# 安装目录相关
# mysql安装根目录
basedir = /usr/local/mysql-5.7.21

# mysql数据文件所在位置
datadir = /usr/local/mysql-5.7.21/data

# 临时目录 比如load data infile会用到,一般都是使用/tmp
tmpdir  = /tmp

# 设置socke文件地址
socket  = /tmp/mysql.sock

##########################################################################################################
# 事务隔离级别，默认为可重复读（REPEATABLE-READ）。（此级别下可能参数很多间隙锁，影响性能，但是修改又影响主从复制及灾难恢复，建议还是修改代码逻辑吧）
# 隔离级别可选项目：READ-UNCOMMITTED  READ-COMMITTED  REPEATABLE-READ  SERIALIZABLE
# transaction_isolation = READ-COMMITTED
transaction_isolation = REPEATABLE-READ

##########################################################################################################
# 数据库引擎与字符集相关设置

# mysql 5.1 之后，默认引擎就是InnoDB了
default_storage_engine = InnoDB
# 内存临时表默认引擎，默认InnoDB
default_tmp_storage_engine = InnoDB
# mysql 5.7新增特性，磁盘临时表默认引擎，默认InnoDB
internal_tmp_disk_storage_engine = InnoDB

#数据库默认字符集,主流字符集支持一些特殊表情符号（特殊表情符占用4个字节）
character-set-server = utf8

#数据库字符集对应一些排序等规则，注意要和character-set-server对应
collation-server = utf8_general_ci

# 设置client连接mysql时的字符集,防止乱码
# init_connect='SET NAMES utf8'

# 是否对sql语句大小写敏感，默认值为0，1表示不敏感
lower_case_table_names = 1

##########################################################################################################
# 数据库连接相关设置
# 最大连接数，可设最大值16384，一般考虑根据同时在线人数设置一个比较综合的数字，鉴于该数值增大并不太消耗系统资源，建议直接设10000
# 如果在访问时经常出现Too Many Connections的错误提示，则需要增大该参数值
max_connections = 10000

# 默认值100，最大错误连接数，如果有超出该参数值个数的中断错误连接，则该主机将被禁止连接。如需对该主机进行解禁，执行：FLUSH HOST
# 考虑高并发场景下的容错，建议加大。
max_connect_errors = 10000

# MySQL打开的文件描述符限制，默认最小1024;
# 当open_files_limit没有被配置的时候，比较max_connections*5和ulimit -n的值，哪个大用哪个，
# 当open_file_limit被配置的时候，比较open_files_limit和max_connections*5的值，哪个大用哪个。
open_files_limit = 65535

# 注意：仍然可能出现报错信息Can't create a new thread；此时观察系统cat /proc/mysql进程号/limits，观察进程ulimit限制情况
# 过小的话，考虑修改系统配置表，/etc/security/limits.conf和/etc/security/limits.d/90-nproc.conf

# MySQL默认的wait_timeout  值为8个小时, interactive_timeout参数需要同时配置才能生效
# MySQL连接闲置超过一定时间后(单位：秒，此处为1800秒)将会被强行关闭
interactive_timeout = 1800 
wait_timeout = 1800 

# 在MySQL暂时停止响应新请求之前的短时间内多少个请求可以被存在堆栈中 
# 官方建议back_log = 50 + (max_connections / 5),封顶数为900
back_log = 900

##########################################################################################################
# 数据库数据交换设置
# 该参数限制服务器端，接受的数据包大小，如果有BLOB子段，建议增大此值，避免写入或者更新出错。有BLOB子段，建议改为1024M
max_allowed_packet = 128M

##########################################################################################################
# 内存，cache与buffer设置


# 内存临时表的最大值,默认16M，此处设置成128M
tmp_table_size = 64M
# 用户创建的内存表的大小，默认16M，往往和tmp_table_size一起设置，限制用户临师表大小。
# 超限的话，MySQL就会自动地把它转化为基于磁盘的MyISAM表，存储在指定的tmpdir目录下，增大IO压力，建议内存大，增大该数值。
max_heap_table_size = 64M

# 表示这个mysql版本是否支持查询缓存。ps：SHOW STATUS LIKE 'qcache%'，与缓存相关的状态变量。
# have_query_cache

# 这个系统变量控制着查询缓存工能的开启的关闭，0时表示关闭，1时表示打开，2表示只要select 中明确指定SQL_CACHE才缓存。
# 看业务场景决定是否使用缓存，不使用，下面就不用配置了。
query_cache_type = 0 

# 默认值1M，优点是查询缓冲可以极大的提高服务器速度, 如果你有大量的相同的查询并且很少修改表。
# 缺点：在你表经常变化的情况下或者如果你的查询原文每次都不同,查询缓冲也许引起性能下降而不是性能提升。
query_cache_size = 64M 

# 只有小于此设定值的结果才会被缓冲，保护查询缓冲,防止一个极大的结果集将其他所有的查询结果都覆盖。
query_cache_limit = 2M

# 每个被缓存的结果集要占用的最小内存,默认值4kb，一般不怎么调整。
# 如果Qcache_free_blocks值过大，可能是query_cache_min_res_unit值过大，应该调小些
# query_cache_min_res_unit的估计值：(query_cache_size - Qcache_free_memory) / Qcache_queries_in_cache
query_cache_min_res_unit = 4kb

# 在一个事务中binlog为了记录SQL状态所持有的cache大小
# 如果你经常使用大的,多声明的事务,你可以增加此值来获取更大的性能.
# 所有从事务来的状态都将被缓冲在binlog缓冲中然后在提交后一次性写入到binlog中
# 如果事务比此值大, 会使用磁盘上的临时文件来替代.
# 此缓冲在每个连接的事务第一次更新状态时被创建
binlog_cache_size = 1M

#*** MyISAM 相关选项
# 指定索引缓冲区的大小, 为MYISAM数据表开启供线程共享的索引缓存,对INNODB引擎无效。相当影响MyISAM的性能。
# 不要将其设置大于你可用内存的30%,因为一部分内存同样被OS用来缓冲行数据
# 甚至在你并不使用MyISAM 表的情况下, 你也需要仍旧设置起 8-64M 内存由于它同样会被内部临时磁盘表使用.
# 默认值 8M，建议值：对于内存在4GB左右的服务器该参数可设置为256M或384M。注意：该参数值设置的过大反而会是服务器整体效率降低！
key_buffer_size = 64M

# 为每个扫描MyISAM的线程分配参数设置的内存大小缓冲区。 
# 默认值128kb，建议值：16G内存建议1M，4G：128kb或者256kb吧
# 注意，该缓冲区是每个连接独占的，所以总缓冲区大小为 128kb*连接数；极端情况128kb*maxconnectiosns，会超级大，所以要考虑日常平均连接数。
# 一般不需要太关心该数值，稍微增大就可以了，
read_buffer_size = 262144 

# 支持任何存储引擎
# MySQL的随机读缓冲区大小，适当增大，可以提高性能。
# 默认值256kb；建议值：得参考连接数，16G内存，有人推荐8M
# 注意，该缓冲区是每个连接独占的，所以总缓冲区大小为128kb*连接数；极端情况128kb*maxconnectiosns，会超级大，所以要考虑日常平均连接数。
read_rnd_buffer_size = 1M

# order by或group by时用到 
# 支持所有引擎，innodb和myisam有自己的innodb_sort_buffer_size和myisam_sort_buffer_size设置
# 默认值256kb；建议值：得参考连接数，16G内存，有人推荐8M.
# 注意，该缓冲区是每个连接独占的，所以总缓冲区大小为 1M*连接数；极端情况1M*maxconnectiosns，会超级大。所以要考虑日常平均连接数。
sort_buffer_size = 1M

# 此缓冲被使用来优化全联合(full JOINs 不带索引的联合)
# 类似的联合在极大多数情况下有非常糟糕的性能表现,但是将此值设大能够减轻性能影响.
# 通过 “Select_full_join” 状态变量查看全联合的数量
# 注意，该缓冲区是每个连接独占的，所以总缓冲区大小为 1M*连接数；极端情况1M*maxconnectiosns，会超级大。所以要考虑日常平均连接数。
# 默认值256kb;建议值：16G内存，设置8M.
join_buffer_size = 1M

# 缓存linux文件描述符信息，加快数据文件打开速度
# 它影响myisam表的打开关闭，但是不影响innodb表的打开关闭。
# 默认值2000，建议值：根据状态变量Opened_tables去设定
table_open_cache = 2000

# 缓存表定义的相关信息，加快读取表信息速度
# 默认值1400，最大值2000，建议值：基本不改。
table_definition_cache = 1400
# 该参数是myssql 5.6后引入的，目的是提高并发。
# 默认值1，建议值：cpu核数，并且<=16
table_open_cache_instances = 2

# 当客户端断开之后，服务器处理此客户的线程将会缓存起来以响应下一个客户而不是销毁。可重用，减小了系统开销。
# 默认值为9，建议值：两种取值方式，方式一，根据物理内存，1G  —> 8；2G  —> 16； 3G  —> 32； >3G  —> 64；
# 方式二，根据show status like  'threads%'，查看Threads_connected值。
thread_cache_size = 16

# 默认值256k,建议值：16/32G内存，512kb，其他一般不改变，如果报错：Thread stack overrun，就增大看看,
# 注意，每个线程分配内存空间，所以总内存空间。。。你懂得。
thread_stack = 512k

##########################################################################################################
# 日志文件相关设置，一般只开启三种日志，错误日志，慢查询日志，二进制日志。普通查询日志不开启。

# 普通查询日志，默认值off，不开启
general_log = 0
# 普通查询日志存放地址
general_log_file = /usr/local/mysql-5.7.21/log/mysql-general.log

# 全局动态变量，默认3，范围：1～3
# 表示错误日志记录的信息，1：只记录error信息；2：记录error和warnings信息；3：记录error、warnings和普通的notes信息。
log_error_verbosity = 2
# 错误日志文件地址
log_error = /usr/local/mysql-5.7.21/log/mysql-error.log

# 开启慢查询
slow_query_log = 1

# 开启慢查询时间，此处为1秒，达到此值才记录数据
long_query_time = 3

# 检索行数达到此数值，才记录慢查询日志中
min_examined_row_limit = 100

# mysql 5.6.5新增，用来表示每分钟允许记录到slow log的且未使用索引的SQL语句次数，默认值为0，不限制。
log_throttle_queries_not_using_indexes = 0

# 慢查询日志文件地址
slow_query_log_file = /usr/local/mysql-5.7.21/log/mysql-slow.log

# 开启记录没有使用索引查询语句
log-queries-not-using-indexes = 1

# 开启二进制日志
log_bin = /usr/local/mysql-5.7.21/log/mysql-bin.log
# mysql清除过期日志的时间，默认值0，不自动清理，而是使用滚动循环的方式。
expire_logs_days = 0
# 如果二进制日志写入的内容超出给定值，日志就会发生滚动。你不能将该变量设置为大于1GB或小于4096字节。 默认值是1GB。
max_binlog_size = 1000M
# binlog的格式也有三种：STATEMENT，ROW，MIXED。mysql 5.7.7后，默认值从 MIXED 改为 ROW
# 关于binlog日志格式问题，请查阅网络资料
binlog_format = row
# 默认值N=1，使binlog在每N次binlog写入后与硬盘同步，ps：1最慢
# sync_binlog = 1 

##########################################################################################################
# innodb选项

# 说明：该参数可以提升扩展性和刷脏页性能。
# 默认值1，建议值：4-8；并且必须小于innodb_buffer_pool_instances
innodb_page_cleaners = 4

# 说明：一般8k和16k中选择，8k的话，cpu消耗小些，selcet效率高一点，一般不用改
# 默认值：16k；建议值：不改，
innodb_page_size = 16384

# 说明：InnoDB使用一个缓冲池来保存索引和原始数据, 不像MyISAM.这里你设置越大,你在存取表里面数据时所需要的磁盘I/O越少.
# 在一个独立使用的数据库服务器上,你可以设置这个变量到服务器物理内存大小的60%-80%
# 注意别设置的过大，会导致system的swap空间被占用，导致操作系统变慢，从而减低sql查询的效率
# 默认值：128M，建议值：物理内存的60%-80%
innodb_buffer_pool_size = 512M

# 说明:只有当设置 innodb_buffer_pool_size 值大于1G时才有意义，小于1G，instances默认为1，大于1G，instances默认为8
# 但是网络上有评价，最佳性能，每个实例至少1G大小。
# 默认值：1或8，建议值：innodb_buffer_pool_size/innodb_buffer_pool_instances >= 1G
innodb_buffer_pool_instances = 1

# 说明：mysql 5.7 新特性，defines the chunk size for online InnoDB buffer pool resizing operations.
# 实际缓冲区大小必须为innodb_buffer_pool_chunk_size*innodb_buffer_pool_instances*倍数，取略大于innodb_buffer_pool_size
# 默认值128M，建议值：默认值就好，乱改反而容易出问题，它会影响实际buffer pool大小。
innodb_buffer_pool_chunk_size = 128M 

# 在启动时把热数据加载到内存。默认值为on，不修改
innodb_buffer_pool_load_at_startup = 1
# 在关闭时把热数据dump到本地磁盘。默认值为on，不修改
innodb_buffer_pool_dump_at_shutdown = 1

# 说明：影响Innodb缓冲区的刷新算法，建议从小到大配置，直到zero free pages；innodb_lru_scan_depth * innodb_buffer_pool_instances defines the amount of work performed by the page cleaner thread each second.
# 默认值1024，建议值: 未知
innodb_lru_scan_depth = 1024

# 说明：事务等待获取资源等待的最长时间，单位为秒，看具体业务情况，一般默认值就好
# 默认值：50，建议值：看业务。
innodb_lock_wait_timeout = 60

# 说明：设置了Mysql后台任务（例如页刷新和merge dadta from buffer pool）每秒io操作的上限。
# 默认值：200，建议值：方法一，单盘sata设100，sas10，raid10设200，ssd设2000，fushion-io设50000；方法二，通过测试工具获得磁盘io性能后，设置IOPS数值/2。
innodb_io_capacity = 2000
# 说明：该参数是所有缓冲区线程io操作的总上限。
# 默认值：innodb_io_capacity的两倍。建议值：例如用iometer测试后的iops数值就好
innodb_io_capacity_max = 4000

# 说明：控制着innodb数据文件及redo log的打开、刷写模式，三种模式：fdatasync(默认)，O_DSYNC，O_DIRECT
# fdatasync：数据文件，buffer pool->os buffer->磁盘；日志文件，buffer pool->os buffer->磁盘；
# O_DSYNC：  数据文件，buffer pool->os buffer->磁盘；日志文件，buffer pool->磁盘；
# O_DIRECT： 数据文件，buffer pool->磁盘；           日志文件，buffer pool->os buffer->磁盘；
# 默认值为空，建议值：使用SAN或者raid，建议用O_DIRECT，不懂测试的话，默认生产上使用O_DIRECT
innodb_flush_method = O_DIRECT

# 说明：mysql5.7之后默认开启，意思是，每张表一个独立表空间。
# 默认值1，开启
innodb_file_per_table = 1

# 说明：The path where InnoDB creates undo tablespaces.通常等于undo log文件的存放目录。
# 默认值./;自行设置
innodb_undo_directory = /usr/local/mysql-5.7.21/log
# 说明：The number of undo tablespaces used by InnoDB.等于undo log文件数量。5.7.21后开始弃用
# 默认值为0，建议默认值就好，不用调整了。
innodb_undo_tablespaces = 0
# 说明：定义undo使用的回滚段数量。5.7.19后弃用
# 默认值128，建议不动，以后弃用了。
innodb_undo_logs = 128
# 说明：5.7.5后开始使用，在线收缩undo log使用的空间。
# 默认值：关闭，建议值：开启
innodb_undo_log_truncate = 1
# 说明：结合innodb_undo_log_truncate，实现undo空间收缩功能
# 默认值：1G，建议值，不改。
innodb_max_undo_log_size = 1G

# 说明：重作日志文件的存放目录
innodb_log_group_home_dir = /usr/local/mysql-5.7.21/log
# 说明：日志文件的大小
# 默认值:48M,建议值：根据你系统的磁盘空间和日志增长情况调整大小
innodb_log_file_size = 128M
# 说明：日志组中的文件数量，mysql以循环方式写入日志
# 默认值2，建议值：根据你系统的磁盘空间和日志增长情况调整大小
innodb_log_files_in_group = 3
# 此参数确定些日志文件所用的内存大小，以M为单位。缓冲区更大能提高性能，但意外的故障将会丢失数据。MySQL开发人员建议设置为1－8M之间
innodb_log_buffer_size = 16M

# 说明：可以控制log从系统buffer刷入磁盘文件的刷新频率，增大可减轻系统负荷
# 默认值是1；建议值不改。系统性能一般够用。
innodb_flush_log_at_timeout = 1
# 说明：参数可设为0，1，2；
# 参数0：表示每秒将log buffer内容刷新到系统buffer中，再调用系统flush操作写入磁盘文件。
# 参数1：表示每次事物提交，将log buffer内容刷新到系统buffer中，再调用系统flush操作写入磁盘文件。
# 参数2：表示每次事物提交，将log buffer内容刷新到系统buffer中，隔1秒后再调用系统flush操作写入磁盘文件。
innodb_flush_log_at_trx_commit = 1

# 说明：限制Innodb能打开的表的数据，如果库里的表特别多的情况，请增加这个。
# 值默认是2000，建议值：参考数据库表总数再进行调整，一般够用不用调整。
innodb_open_files = 8192

# innodb处理io读写的后台并发线程数量，根据cpu核来确认，取值范围：1-64
# 默认值：4，建议值：与逻辑cpu数量的一半保持一致。
innodb_read_io_threads = 4
innodb_write_io_threads = 4
# 默认设置为 0,表示不限制并发数，这里推荐设置为0，更好去发挥CPU多核处理能力，提高并发量
innodb_thread_concurrency = 0
# 默认值为4，建议不变。InnoDB中的清除操作是一类定期回收无用数据的操作。mysql 5.5之后，支持多线程清除操作。
innodb_purge_threads = 4 

# 说明：mysql缓冲区分为new blocks和old blocks；此参数表示old blocks占比；
# 默认值：37，建议值，一般不动
innodb_old_blocks_pct = 37
# 说明：新数据被载入缓冲池，进入old pages链区，当1秒后再次访问，则提升进入new pages链区。
# 默认值：1000
innodb_old_blocks_time=1000
# 说明：开启异步io，可以提高并发性，默认开启。
# 默认值为1，建议不动
innodb_use_native_aio = 1

# 说明：默认为空，使用data目录，一般不改。
innodb_data_home_dir=/usr/local/mysql-5.7.21/data
# 说明：Defines the name, size, and attributes of InnoDB system tablespace data files.
# 默认值，不指定，默认为ibdata1:12M:autoextend
innodb_data_file_path = ibdata1:12M:autoextend

# 说明:设置了InnoDB存储引擎用来存放数据字典信息以及一些内部数据结构的内存空间大小,除非你的数据对象及其多，否则一般默认不改。
# innodb_additional_mem_pool_size = 16M

# 说明：The crash recovery mode。只有紧急情况需要恢复数据的时候，才改为大于1-6之间数值，含义查下官网。
# 默认值为0；
#innodb_force_recovery = 0

##########################################################################################################
# 其他。。。。
# 参考http://www.kuqin.com/database/20120815/328905.html
# skip-external-locking

# 禁止MySQL对外部连接进行DNS解析，使用这一选项可以消除MySQL进行DNS解析的时间。
# 缺点：所有远程主机连接授权都要使用IP地址方式，因为只认得ip地址了。
# skip_name_resolve = 0

# 默认值为off,timestamp列会自动更新为当前时间，设置为on|1，timestamp列的值就要显式更新
explicit_defaults_for_timestamp = 1

[mysqldump]
# quick选项强制 mysqldump 从服务器查询取得记录直接输出而不是取得所有记录后将它们缓存到内存中
quick
max_allowed_packet = 16M

[mysql]
# mysql命令行工具不使用自动补全功能，建议还是改为
# no-auto-rehash
auto-rehash
socket = /tmp/mysql.sock
```

#### 第七部分

[来源网络](https://github.com/jaywcjlove/mysql-tutorial/blob/master/chapter2/2.5.md)

MySQL配置修改
---

安装完了之后更改配置的需求比较少，所以你需要根据实际使用过程中来修改 MySQL 配置参数，MySQL提供了两个更改配置的方式。

- 通过配置想来修改，听说在windows上面有个配置工具(MySQL server instance config) 提供了自动配置服务，真嗨皮。
- 另一种是手工修改配置文件来修改。

对于初学者刚接触MySQL来说，使用工具来修改配置是非常好的，但是在 Mac 系统下面没有找到这样的工具，如果你部署到Linux下面好像没有这种工具，所以在真正的生产环境还是得修改配置来更改 MySQL 配置。接下来只讲解配置文件来修改，为你将来在 Mac 或者 Linux ，包括windows平台系统下容易配置做点准备吧，通过配置文件来配置，让你做跨平台玩儿 MySQL ，让你逼格更高一点，哈哈。


## MySQL安装目录说明

MySQL 不同的版本安装目录会有一点不一致，但是大致会差不多，会有一点差异，我这个是 Mac OS X 系统中的安装目录，在这里`/usr/local/mysql`

|目录 | 目录内容 |
| ---- | ---- |
|bin/ | 客户端程序和mysqld服务器，相关命令 |
|data/ | |
|docs/ |    |
|include/ | 包含头文件|
|lib/ | 库 |
|man/ |    |
|share/ |    |
|support-files/ | 存在一些默认配置文件，如`my-default.cnf` |


## 配置文件的位置

从命令行终端运行此命令，将在寻找Linux/BSD / OS X系统中的MySQL配置文件 my.cnf 文件：

```bash
mysql --help | grep 'Default options' -A 1
```

上面命令执行后，会有这样的输出：

```bash
Default options are read from the following files in the given order:
/etc/my.cnf /etc/mysql/my.cnf /usr/local/etc/my.cnf ~/.my.cnf
```

现在，可以检查你正在使用的 my.cnf 文件是否存在。在 Mac OS X 中默认式没有 my.cnf 文件的。你可以从这个地方复制一份过去 `/usr/local/mysql/support-files/my-default.cnf` 每个版本都不一样，你只需要找到一个 `.cnf` 后缀结尾的文件即可。复制到`/etc/`目录下并重新命名为 `my.cnf`

## Windows系统配置文件读取

在Windows上，MySQL的程序读取从下表中显示的文件，按照指定的顺序启动配置选项（顶部文件首先被读取，文件读取后优先）。

| 文件名字  | 作用 |
| ---- | ---- |
| **%PROGRAMDATA%**\MySQL\MySQL Server 5.6\my.ini, **%PROGRAMDATA%**\MySQL\MySQL Server 5.6\my.cnf | 全局配置 |
| %WINDIR%\my.ini, %WINDIR%\my.cnf  |  全局配置 |
| C:\my.ini, C:\my.cnf  |  全局配置 |
| **BASEDIR**\my.ini, **BASEDIR**\my.cnf | 全局配置 |
| defaults-extra-file | 如果有的话指定该文件`--defaults-extra-file=文件名字` |
| %APPDATA%\MySQL\.mylogin.cnf  | 登录路径选项（仅适用于客户端） |


- **%PROGRAMDATA%** 这个路径默认为 `C:\ProgramData` 老版本的Windows系统， 默认在 ` C:\Documents and Settings\All Users\Application Data\MySQL`
- **%WINDIR%** 表示Windows的目录位置。使用下面的命令从windir环境变量的值确定其精确位置 `C:\> echo %WINDIR%`
- **BASEDIR** 表示MySQL的安装目录。
- **%APPDATA%** 表示Windows的目录位置。使用下面的命令从windir环境变量的值确定其精确位置 `C:\> echo %WINDIR%`

MySQL 提供的二进制安装代码所创建的默认目录，在Windows中，默认安装路径是`C:\Program Files\MySQL\MySQL Server 5.7`

## Linux系统配置文件读取

| 文件名字 |  作用 |
| ---- | ---- |
| /etc/my.cnf | 全局配置 |
| /etc/mysql/my.cnf  | 全局配置 |
| SYSCONFDIR/my.cnf  | 全局配置 |
| $MYSQL_HOME/my.cnf | Server-specific 服务器特定的选项 (仅适用于服务端) |
| defaults-extra-file | 如果有的话指定该文件`--defaults-extra-file=文件名字` |
| ~/.my.cnf  | Server-specific 服务器特定的选项 |
| ~/.mylogin.cnf | User-specific 登录路径选择 （仅适用于客户端） |

- **$HOME** 上表中表示用户的主目录，即用户的根目录。
- **SYSCONFDIR** 代表指定的目录与SYSCONFDIR配置文件的安装路径，默认情况这个是位于安装目录里面的目录。
- **$MYSQL_HOME** 是包含在该服务器的具体my.cnf文件所在的目录的路径环境变量。如果 $MYSQL_HOME 没有设置，你启动服务器使用mysqld_safe程序，mysqld_safe试图设置 $MYSQL_HOME

工具 **mysqld_safe** 使用注意：

- 让BASEDIR和DATADIR分别代表MySQL的基本目录和数据目录的路径名。
- 如果my.cnf文件在DATADIR但不是在BASEDIR中，mysqld_safe设置MYSQL_HOME到DATADIR。
- 否则，如果MYSQL_HOME未设置并且在DATADIR没有my.cnf文件，mysqld_safe设置MYSQL_HOME到BASEDIR。

## 配置文件内容



```bash

# 以下选项会被MySQL客户端应用读取。
# 注意只有MySQL附带的客户端应用程序保证可以读取这段内容。
# 如果你想你自己的MySQL应用程序获取这些值。
# 需要在MySQL客户端库初始化的时候指定这些选项。

# For advice on how to change settings please see
# http://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html
# *** DO NOT EDIT THIS FILE. It's a template which will be copied to the
# *** default location during install, and will be replaced if you
# *** upgrade to a newer version of MySQL.

# mysqld程序

[mysqld]

# Remove leading # and set to the amount of RAM for the most important data
# cache in MySQL. Start at 70% of total RAM for dedicated server, else 10%.
# innodb_buffer_pool_size = 128M

# ★★★这里很重要️能让MySQL登陆链接变快速
skip-name-resolve

# Remove leading # to turn on a very important data integrity option: logging
# changes to the binary log between backups.
# log_bin

# These are commonly set, remove the # and set as required.
# 使用给定目录作为根目录(安装目录)。
# basedir = .....
# 从给定目录读取数据库文件。
# datadir = .....
# 为mysqld程序指定一个存放进程ID的文件(仅适用于UNIX/Linux系统);
# pid-file = .....
# 指定MsSQL侦听的端口
# port = .....
# server_id = .....
# 为MySQL客户程序与服务器之间的本地通信指定一个套接字文件(Linux下默认是/var/lib/mysql/mysql.sock文件)
# socket = .....


sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES

# 一般配置选项
basedir = /data/apps/mysql
datadir = /data/appData/mysql
port = 3306
socket = /var/run/mysqld/mysqld.sock
# 设置
character-set-server=utf8


# 指定MySQL可能的连接数量。
# 当MySQL主线程在很短时间内接收到非常多的连接请求，该参数生效，主线程花费很短时间检查连接并且启动一个新线程。
# back_log参数的值指出在MySQL暂时停止响应新请求之前的短时间内多少个请求可以被存在堆栈中。
# 如果系统在一个短时间内有很多连接，则需要增大该参数的值，该参数值指定到来的TCP/IP连接的侦听队列的大小。
# 试图设定back_log高于你的操作系统的限制将是无效的。默认值为50。对于Linux系统推荐设置为小于512的整数。

# back_log 是操作系统在监听队列中所能保持的连接数,
# 队列保存了在 MySQL 连接管理器线程处理之前的连接.
# 如果你有非常高的连接率并且出现 “connection refused” 报错,
# 你就应该增加此处的值.
# 检查你的操作系统文档来获取这个变量的最大值.
# 如果将back_log设定到比你操作系统限制更高的值，将会没有效果
back_log = 300

# 不在 TCP/IP 端口上进行监听.
# 如果所有的进程都是在同一台服务器连接到本地的 mysqld,
# 这样设置将是增强安全的方法
# 所有 mysqld 的连接都是通过 Unix Sockets 或者命名管道进行的.
# 注意在 Windows下如果没有打开命名管道选项而只是用此项
# (通过 “enable-named-pipe” 选项) 将会导致 MySQL 服务没有任何作用!
#skip-networking

# MySQL 服务所允许的同时会话数的上限
# 其中一个连接将被 SUPER 权限保留作为管理员登录.
# 即便已经达到了连接数的上限.
max_connections = 3000

# 每个客户端连接最大的错误允许数量,如果达到了此限制.
# 这个客户端将会被 MySQL 服务阻止直到执行了 “FLUSH HOSTS” 或者服务重启
# 非法的密码以及其他在链接时的错误会增加此值.
# 查看 “Aborted_connects” 状态来获取全局计数器.
max_connect_errors = 50

# 所有线程所打开表的数量.
# 增加此值就增加了 mysqld 所需要的文件描述符的数量
# 这样你需要确认在 [mysqld_safe] 中 “open-files-limit” 变量设置打开文件数量允许至少等于 table_cache 的值
table_open_cache = 4096

# 允许外部文件级别的锁. 打开文件锁会对性能造成负面影响
# 所以只有在你在同样的文件上运行多个数据库实例时才使用此选项(注意仍会有其他约束!)
# 或者你在文件层面上使用了其他一些软件依赖来锁定 MyISAM 表
#external-locking

# 服务所能处理的请求包的最大大小以及服务所能处理的最大的请求大小(当与大的 BLOB 字段一起工作时相当必要)
# 每个连接独立的大小，大小动态增加
max_allowed_packet = 32M

# 在一个事务中 binlog 为了记录 SQL 状态所持有的 cache 大小
# 如果你经常使用大的,多声明的事务,你可以增加此值来获取更大的性能.
# 所有从事务来的状态都将被缓冲在 binlog 缓冲中然后在提交后一次性写入到 binlog 中
# 如果事务比此值大, 会使用磁盘上的临时文件来替代.
# 此缓冲在每个连接的事务第一次更新状态时被创建
binlog_cache_size = 4M

# 独立的内存表所允许的最大容量。
# 此选项为了防止意外创建一个超大的内存表导致永尽所有的内存资源。
max_heap_table_size = 128M

# 随机读取数据缓冲区使用内存(read_rnd_buffer_size)：和顺序读取相对应，
# 当 MySQL 进行非顺序读取（随机读取）数据块的时候，会利用>这个缓冲区暂存读取的数据
# 如根据索引信息读取表数据，根据排序后的结果集与表进行 Join 等等
# 总的来说，就是当数据块的读取需要满足>一定的顺序的情况下，MySQL 就需要产生随机读取，进而使用到 read_rnd_buffer_size 参数所设置的内存缓冲区
read_rnd_buffer_size = 16M

# 排序缓冲被用来处理类似 ORDER BY 以及 GROUP BY 队列所引起的排序
# 如果排序后的数据无法放入排序缓冲,一个用来替代的基于磁盘的合并分类会被使用
# 查看 “Sort_merge_passes” 状态变量。
# 在排序发生时由每个线程分配
# 每个需要进行排序的线程分配该大小的一个缓冲区。增加这值加速ORDER BY或GROUP BY操作。
# 注意：该参数对应的分配内存是每连接独占！如果有100个连接，那么实际分配的总共排序缓冲区大小为100×6=600MB
sort_buffer_size = 16M

# 此缓冲被使用来优化全联合(FULL JOINS 不带索引的联合)。
# 类似的联合在极大多数情况下有非常糟糕的性能表现,但是将此值设大能够减轻性能影响。
# 通过 “Select_full_join” 状态变量查看全联合的数量
# 当全联合发生时,在每个线程中分配
join_buffer_size = 16M

# 缓存可重用的线程数
# thread_cache = 8

# 避免MySQL的外部锁定，减少出错几率增强稳定性。
# skip-locking                 

# 我们在 cache 中保留多少线程用于重用
# 当一个客户端断开连接后,如果 cache 中的线程还少于 thread_cache_size,则客户端线程被放入cache 中。
# 这可以在你需要大量新连接的时候极大的减少线程创建的开销
# (一般来说如果你有好的线程模型的话,这不会有明显的性能提升。)
thread_cache_size = 16

# 此允许应用程序给予线程系统一个提示在同一时间给予渴望被运行的线程的数量。
# 此值只对于支持 thread_concurrency() 函数的系统有意义( 例如Sun Solaris)。
# 你可可以尝试使用 [CPU数量]*(2..4) 来作为 thread_concurrency 的值
#****(此属性对当前环境无效)****
# thread_concurrency = 8

# 查询缓冲常被用来缓冲 SELECT 的结果并且在下一次同样查询的时候不再执行直接返回结果。
# 打开查询缓冲可以极大的提高服务器速度, 如果你有大量的相同的查询并且很少修改表。
# 查看 “Qcache_lowmem_prunes” 状态变量来检查是否当前值对于你的负载来说是否足够高。
# 注意: 在你表经常变化的情况下或者如果你的查询原文每次都不同,
# 查询缓冲也许引起性能下降而不是性能提升。
query_cache_size = 128M

# 只有小于此设定值的结果才会被缓冲
# 此设置用来保护查询缓冲,防止一个极大的结果集将其他所有的查询结果都覆盖。
query_cache_limit = 4M

# 被全文检索索引的最小的字长。
# 你也许希望减少它，如果你需要搜索更短字的时候。
# 注意在你修改此值之后，你需要重建你的 FULLTEXT 索引
ft_min_word_len = 8

# 如果你的系统支持 memlock() 函数，你也许希望打开此选项用以让运行中的 mysql 在在内存高度紧张的时候，数据在内存中保持锁定并且防止可能被 swapping out
# 此选项对于性能有益
#memlock

# 当创建新表时作为默认使用的表类型，
# 如果在创建表示没有特别执行表类型，将会使用此值
#****(此属性对当前环境无效)****
#default_table_type = InnoDB

# 线程使用的堆大小. 此容量的内存在每次连接时被预留.
# MySQL 本身常不会需要超过 64K 的内存
# 如果你使用你自己的需要大量堆的 UDF 函数或者你的操作系统对于某些操作需要更多的堆，你也许需要将其设置的更高一点.
thread_stack = 512K

# 设定默认的事务隔离级别.可用的级别如下:
# READ-UNCOMMITTED， READ-COMMITTED， REPEATABLE-READ， SERIALIZABLE
transaction_isolation = REPEATABLE-READ

# 内部(内存中)临时表的最大大小
# 如果一个表增长到比此值更大，将会自动转换为基于磁盘的表。
# 此限制是针对单个表的，而不是总和。
tmp_table_size = 128M

# 打开二进制日志功能。
# 在复制(replication)配置中，作为 MASTER 主服务器必须打开此项
# 如果你需要从你最后的备份中做基于时间点的恢复，你也同样需要二进制日志。
log-bin=mysql-bin

# 如果你在使用链式从服务器结构的复制模式 (A->B->C)，
# 你需要在服务器B上打开此项。
# 此选项打开在从线程上重做过的更新的日志， 并将其写入从服务器的二进制日志。
#log_slave_updates

# 打开全查询日志。 所有的由服务器接收到的查询 (甚至对于一个错误语法的查询)
# 都会被记录下来。 这对于调试非常有用， 在生产环境中常常关闭此项。
#log

# 将警告打印输出到错误 log 文件。 如果你对于 MySQL 有任何问题
# 你应该打开警告 log 并且仔细审查错误日志，查出可能的原因。
#log_warnings

# 记录慢速查询。 慢速查询是指消耗了比 “long_query_time” 定义的更多时间的查询。
# 如果 log_long_format 被打开，那些没有使用索引的查询也会被记录。
# 如果你经常增加新查询到已有的系统内的话。 一般来说这是一个好主意，
#log_slow_queries

# 有的使用了比这个时间(以秒为单位)更多的查询会被认为是慢速查询。
# 不要在这里使用“1″, 否则会导致所有的查询,甚至非常快的查询页被记录下来(由于 MySQL 目前时间的精确度只能达到秒的级别)。
long_query_time = 6

# 在慢速日志中记录更多的信息。
# 一般此项最好打开。
# 打开此项会记录使得那些没有使用索引的查询也被作为到慢速查询附加到慢速日志里
#log_long_format

# 此目录被MySQL用来保存临时文件。例如,
# 它被用来处理基于磁盘的大型排序,和内部排序一样。
# 以及简单的临时表。
# 如果你不创建非常大的临时文件,将其放置到 swapfs/tmpfs 文件系统上也许比较好
# 另一种选择是你也可以将其放置在独立的磁盘上。
# 你可以使用”;”来放置多个路径
# 他们会按照 roud-robin 方法被轮询使用。
#tmpdir = /tmp

# *** 主从复制相关的设置

# 唯一的服务辨识号,数值位于 1 到 2^32-1之间。
# 此值在master和slave上都需要设置。
# 如果 “master-host” 没有被设置,则默认为1, 但是如果忽略此选项,MySQL不会作为master生效。
server-id = 1

# 复制的Slave (去掉master段的注释来使其生效)
#
# 为了配置此主机作为复制的slave服务器,你可以选择两种方法:
#
# 1) 使用 CHANGE MASTER TO 命令 (在我们的手册中有完整描述) -
# 语法如下:
#
# CHANGE MASTER TO MASTER_HOST=, MASTER_PORT=,
# MASTER_USER=, MASTER_PASSWORD= ;
#
# 你需要替换掉，等被尖括号包围的字段以及使用master的端口号替换 (默认3306)。
#
# 例子:
#
# CHANGE MASTER TO MASTER_HOST=’125.564.12.1′, MASTER_PORT=3306,
# MASTER_USER=’joe’, MASTER_PASSWORD=’secret’;
#
# 或者
#
# 2) 设置以下的变量. 不论如何, 在你选择这种方法的情况下， 然后第一次启动复制(甚至不成功的情况下，
# 例如如果你输入错密码在master-password字段并且slave无法连接)，
# slave会创建一个 master.info 文件，并且之后任何对于包含在此文件内的参数的变化都会被忽略
# 并且由 master.info 文件内的内容覆盖， 除非你关闭slave服务， 删除 master.info 并且重启slave 服务。
# 由于这个原因，你也许不想碰一下的配置(注释掉的) 并且使用 CHANGE MASTER TO (查看上面) 来代替
#
# 所需要的唯一id号位于 2 和 2^32 – 1之间
# (并且和master不同)
# 如果master-host被设置了.则默认值是2
# 但是如果省略,则不会生效
#server-id = 2
#
# 复制结构中的master – 必须
#master-host =
#
# 当连接到master上时slave所用来认证的用户名 – 必须
#master-user =
#
# 当连接到master上时slave所用来认证的密码 – 必须
#master-password =
#
# master监听的端口.
# 可选 – 默认是3306
#master-port =

# 使得slave只读。只有用户拥有SUPER权限和在上面的slave线程能够修改数据。
# 你可以使用此项去保证没有应用程序会意外的修改slave而不是master上的数据
#read_only

#*** MyISAM 相关选项

# 关键词缓冲的大小， 一般用来缓冲 MyISAM 表的索引块。
# 不要将其设置大于你可用内存的30%，
# 因为一部分内存同样被OS用来缓冲行数据
# 甚至在你并不使用 MyISAM 表的情况下， 你也需要仍旧设置起 8-64M 内存由于它同样会被内部临时磁盘表使用。
# key_buffer_size = 128M

# 用来做 MyISAM 表全表扫描的缓冲大小.
# 当全表扫描需要时,在对应线程中分配.
# read_buffer_size = 8M

# 当在排序之后,从一个已经排序好的序列中读取行时,行数据将从这个缓冲中读取来防止磁盘寻道.
# 如果你增高此值,可以提高很多 ORDER BY 的性能.
# 当需要时由每个线程分配
# read_rnd_buffer_size = 64M

# MyISAM 使用特殊的类似树的 cache 来使得突发插入
# (这些插入是,INSERT … SELECT, INSERT … VALUES (…), (…), …, 以及 LOAD DATA INFILE) 更快.
# 此变量限制每个进程中缓冲树的字节数.
# 设置为 0 会关闭此优化.
# 为了最优化不要将此值设置大于 “key_buffer_size”.
# 当突发插入被检测到时此缓冲将被分配.
# bulk_insert_buffer_size = 256M

# 此缓冲当 MySQL 需要在 REPAIR, OPTIMIZE, ALTER 以及 LOAD DATA INFILE 到一个空表中引起重建索引时被分配.
# 这在每个线程中被分配.所以在设置大值时需要小心.
# myisam_sort_buffer_size = 256M

# MySQL 重建索引时所允许的最大临时文件的大小 (当 REPAIR, ALTER TABLE 或者 LOAD DATA INFILE).
# 如果文件大小比此值更大,索引会通过键值缓冲创建(更慢)
# myisam_max_sort_file_size = 10G

# 如果被用来更快的索引创建索引所使用临时文件大于制定的值,那就使用键值缓冲方法.
# 这主要用来强制在大表中长字串键去使用慢速的键值缓冲方法来创建索引.
# myisam_max_extra_sort_file_size = 10G

# 如果一个表拥有超过一个索引, MyISAM 可以通过并行排序使用超过一个线程去修复他们.
# 这对于拥有多个 CPU 以及大量内存情况的用户,是一个很好的选择.
# myisam_repair_threads = 1

# 自动检查和修复没有适当关闭的 MyISAM 表.
# myisam_recover

# 默认关闭 Federated
# skip-federated

# *** BDB 相关选项 ***

# 如果你运行的MySQL服务有BDB支持但是你不准备使用的时候使用此选项. 这会节省内存并且可能加速一些事.
#****(此属性对当前环境无效)****
#skip-bdb

# *** INNODB 相关选项 ***

# 如果你的 MySQL 服务包含 InnoDB 支持但是并不打算使用的话,
# 使用此选项会节省内存以及磁盘空间,并且加速某些部分
#skip-innodb

# 附加的内存池被 InnoDB 用来保存 metadata 信息(5.6中不再推荐使用)
# 如果 InnoDB 为此目的需要更多的内存,它会开始从 OS 这里申请内存.
# 由于这个操作在大多数现代操作系统上已经足够快, 你一般不需要修改此值.
# SHOW INNODB STATUS 命令会显示当先使用的数量.
#****(此属性对当前环境无效)****
#innodb_additional_mem_pool_size = 64M

# InnoDB使用一个缓冲池来保存索引和原始数据, 不像 MyISAM.
# 这里你设置越大,这能保证你在大多数的读取操作时使用的是内存而不是硬盘,在存取表里面数据时所需要的磁盘 I/O 越少.
# 在一个独立使用的数据库服务器上,你可以设置这个变量到服务器物理内存大小的80%
# 不要设置过大,否则,由于物理内存的竞争可能导致操作系统的换页颠簸.
# 注意在32位系统上你每个进程可能被限制在 2-3.5G 用户层面内存限制,
# 所以不要设置的太高.
innodb_buffer_pool_size = 6G

# InnoDB 将数据保存在一个或者多个数据文件中成为表空间.
# 如果你只有单个逻辑驱动保存你的数据,一个单个的自增文件就足够好了.
# 其他情况下.每个设备一个文件一般都是个好的选择.
# 你也可以配置 InnoDB 来使用裸盘分区 – 请参考手册来获取更多相关内容
innodb_data_file_path = ibdata1:10M:autoextend

# 设置此选项如果你希望InnoDB表空间文件被保存在其他分区.
# 默认保存在MySQL的datadir中.
#innodb_data_home_dir =

# 用来同步IO操作的IO线程的数量.
# 此值在Unix下被硬编码为8,但是在Windows磁盘I/O可能在一个大数值下表现的更好.
#innodb_file_io_threads = 8

# 如果你发现 InnoDB 表空间损坏, 设置此值为一个非零值可能帮助你导出你的表.
# 从1开始并且增加此值知道你能够成功的导出表.
#innodb_force_recovery=1

# 在 InnoDb 核心内的允许线程数量.
# 最优值依赖于应用程序,硬件以及操作系统的调度方式.
# 过高的值可能导致线程的互斥颠簸.
innodb_thread_concurrency = 16

# 如果设置为1 ,InnoDB 会在每次提交后刷新(fsync)事务日志到磁盘上,
# 这提供了完整的 ACID 行为.
# 如果你愿意对事务安全折衷, 并且你正在运行一个小的事物, 你可以设置此值到0或者2来减少由事务日志引起的磁盘I/O
# 0代表日志只大约每秒写入日志文件并且日志文件刷新到磁盘.
# 2代表日志写入日志文件在每次提交后,但是日志文件只有大约每秒才会刷新到磁盘上.
innodb_flush_log_at_trx_commit = 2
#（说明：如果是游戏服务器，建议此值设置为2；如果是对数据安全要求极高的应用，建议设置为1；
#设置为0性能最高，但如果发生故障，数据可能会有丢失的危险！
#默认值1的意思是每一次事务提交或事务外的指令都需要把日志写入（flush）硬盘，这是很费时的。
#特别是使用电池供电缓存（Battery backed up cache）时。
#设成2对于很多运用，特别是从MyISAM表转过来的是可以的，它的意思是不写入硬盘而是写入系统缓存。
#日志仍然会每秒flush到硬盘，所以你一般不会丢失超过1-2秒的更新。
#设成0会更快一点，但安全方面比较差，即使MySQL挂了也可能会丢失事务的数据。而值2只会在整个操作系统挂了时才可能丢数据。）

# 加速 InnoDB 的关闭. 这会阻止 InnoDB 在关闭时做全清除以及插入缓冲合并.
# 这可能极大增加关机时间, 但是取而代之的是 InnoDB 可能在下次启动时做这些操作.
#innodb_fast_shutdown

# 用来缓冲日志数据的缓冲区的大小.
# 当此值快满时, InnoDB 将必须刷新数据到磁盘上.
# 由于基本上每秒都会刷新一次,所以没有必要将此值设置的太大(甚至对于长事务而言)
innodb_log_buffer_size = 16M

# 在日志组中每个日志文件的大小.
# 你应该设置日志文件总合大小到你缓冲池大小的25%~100%
# 来避免在日志文件覆写上不必要的缓冲池刷新行为.
# 不论如何, 请注意一个大的日志文件大小会增加恢复进程所需要的时间.
innodb_log_file_size = 512M

# 在日志组中的文件总数.
# 通常来说2~3是比较好的.
innodb_log_files_in_group = 3

# InnoDB 的日志文件所在位置. 默认是 MySQL 的 datadir.
# 你可以将其指定到一个独立的硬盘上或者一个RAID1卷上来提高其性能
#innodb_log_group_home_dir

# 在 InnoDB 缓冲池中最大允许的脏页面的比例.
# 如果达到限额, InnoDB 会开始刷新他们防止他们妨碍到干净数据页面.
# 这是一个软限制,不被保证绝对执行.
innodb_max_dirty_pages_pct = 90

# InnoDB 用来刷新日志的方法.
# 表空间总是使用双重写入刷新方法
# 默认值是 “fdatasync”, 另一个是 “O_DSYNC”.
# 一般来说，如果你有硬件 RAID 控制器，并且其独立缓存采用 write-back 机制，并有着电池断电保护，那么应该设置配置为 O_DIRECT
# 否则，大多数情况下应将其设为 fdatasync
#innodb_flush_method=fdatasync

# 在被回滚前,一个 InnoDB 的事务应该等待一个锁被批准多久.
# InnoDB 在其拥有的锁表中自动检测事务死锁并且回滚事务.
# 如果你使用 LOCK TABLES 指令, 或者在同样事务中使用除了 InnoDB 以外的其他事务安全的存储引擎
# 那么一个死锁可能发生而 InnoDB 无法注意到.
# 这种情况下这个 timeout 值对于解决这种问题就非常有帮助.
innodb_lock_wait_timeout = 120

# 这项设置告知InnoDB是否需要将所有表的数据和索引存放在共享表空间里（innodb_file_per_table = OFF） 或者为每张表的数据单独放在一个.ibd文件（innodb_file_per_table = ON）
# 每张表一个文件允许你在drop、truncate或者rebuild表时回收磁盘空间
# 这对于一些高级特性也是有必要的，比如数据压缩,但是它不会带来任何性能收益
innodb_file_per_table = on

[mysqldump]
# 不要在将内存中的整个结果写入磁盘之前缓存. 在导出非常巨大的表时需要此项
quick

max_allowed_packet = 32M

[mysql]
no-auto-rehash
default-character-set=utf8
# 仅仅允许使用键值的 UPDATEs 和 DELETEs .
safe-updates

[myisamchk]
key_buffer = 16M
sort_buffer_size = 16M
read_buffer = 8M
write_buffer = 8M

[mysqlhotcopy]
interactive-timeout

[mysqld_safe]
# 增加每个进程的可打开文件数量.
# 警告: 确认你已经将全系统限制设定的足够高!
# 打开大量表需要将此值设大
open-files-limit = 8192

#
# MySQL 服务端
#
[client]
default-character-set=utf8
```


配置好定制配置文件 my.cnf 之后需要初始化一下

```bash
mysqld --initialize
```

初始化之后需要重启服务

```bash
# 重启服务
mysql.server restart

# Linux 这么运行，启动服务
service mysqld start
# Mac 运行去掉 service
mysqld start

# Linux 查看服务运行的状态
service mysqld status
```
