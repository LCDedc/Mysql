# MySQL日志

## mysql日志简介
* 错误日志：记录mysql服务的启动、运行或停止服务时出现的问题
* 查询日志：记录建立的客户端连接和执行语句
* 二进制日志：记录所有更改数据的语句，可以用于数据复制
* 慢查询日志：记录所有执行时间超过long_query_time的所有查询或不使用索引的查询

## 二进制日志
记录了数据的更改信息，但不包括未更改的信息
### 查看二进制日志
* show binary logs;查看二进制文件个数及文件名,每启动一次产生一个
* mysqlbinlog /usr/local/mysql/data/binlog;终端查看二进制文件，data文件夹没有查看权限，
sudo chmod -R a+rwx /usr/local/mysql/data，然后输入密码。

### 删除二进制日志
* reset master;删除所有的二进制日志
* purge \[master] \[binary] logs to 'log_name'：删除指定日志
* purge \[master] \[binary] logs before 'date'：删除指定日期前的日志

### 使用二进制日志恢复数据
可以恢复数据库到指定时间时的状态
* mysqlbinlog --stop-date="2012-07-15 14:27:48" /usr/local/mysql/data/binlog.000001|mysql -uuser -ppass

### 暂时停止二进制功能
* set sql_log_bin=1;继续二进制日志
* set sql_log_bin=0;暂停二进制日志

## 错误日志

### 启动错误日志
修改配置文件my.ini或my.cnf，mac8.0版的mysql好像是默认开启的

### 查看错误日志
* show variables like '%log_error%';

## 查询日志

### 查看查询日志
这个版本好像没有慢查询日志和查询日志
