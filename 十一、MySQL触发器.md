# 触发器
触发器和存储过程一样，都是嵌入到mysql程序的，触发器是由事件来触发某个操作的，如insert、update等。
如果定义了触发程序，当数据库执行这些语句的时候就会激发触发器执行相应的操作。

## 创建触发器

* create trigger trigger_name trigger_time trigger_event on tb for each row trigger_stmt:基础的触发器的语句。
* `create trigger sal_sum before insert on tb_emp for each row set @sum=@sum+NEW.sal;`
在插入数据之前对表中的工资进行求和
* `create trigger testref before insert on tb1 for each row
begin
insert into tb2 set tb2.a2=new.a1;
delete from tb3 where tb3.a3 =new.a1;
end`多条语句设置为触发器

## 查看触发器
* show triggers;
* select * from information_schema.TRIGGERS where TRIGGER_NAME='sal_sum';

## 触发器的应用
* `create trigger trig_insert after insert on tb_emp for each row insert tb2 values()`:向某一个表中插入数据时，
也向另一个表中插入数据。

## 删除触发器
* drop trigger if exist trigger_name;

* **及时删除不必要的触发器**
