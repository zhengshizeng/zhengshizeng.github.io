---
title: JOB定时执行存储过程
date: 2018-11-03 10:07:33
tags: [数据库,Oracle] 
categories: "数据库"
---
### 创建JOB定时执行存储过程
> [Oracle]使用dbms_job包创建Oracle定时任务   
>  在Oracle的包里面，有一个名字叫做DBMS_JOB的包，它的作用是安排和管理作业队列。
<!-- more -->

##### 1.创建JOB 
###### 1.SUBMIT 该过程用于建立一个新的作业.
```
DBMS_JOB.SUBMIT(
   JOB OUT BINARY_INTERGER,
   WHAT IN VARCHAR2，
   NEXT_DATE IN DATE DEFAULT SYSDATE,
   INTERVAL IN VARCHAR2 DEFAULT ‘NULL’,
   NO_PARSE IN BOOLEAN DEFAULT FALSE,
   INSTANCE IN BINARY_INTEGER DEFAULT ANY_INSTANCE,
   FORCE IN BOOLEAN DEFAULT FALSE
);
```
###### 参数说明:
编号 | 参数 | 参数说明
---|---|--- 
1|job|用于指定作业编号
2|what|用于指定作业要执行的操作
3|next_date|用于指定该操作的下一次运行的日期
4|interval|用于指定该操作的时间间隔
5|no_parse|用于指定是否需要解析与作业相关的过程
6|instance|用于指定哪个例程可以运行作业
7|force|用于指定是否强制运行与作业相关的例程

```
declare
  jobno binary_integer;
begin
  --提交,操作的时间间隔设置为1分钟
  dbms_job.submit(jobno,'insert_job();',sysdate,'sysdate+1/(24*60)');
  --打印序列号
  dbms_output.put_line('jobno='||jobno);
  --运行
  dbms_job.run(jobno);
end;
```
```
declare  test_job_PJHGR number;  
begin  
dbms_job.submit(test_job_PJHGR,'SP_JSpjhgr;',sysdate,'TRUNC(SYSDATE + 1)');  
commit;  
end; 

--
begin  
dbms_job.run(21);  
commit;  
end; 
--
select * from sys.user_jobs  
```
下面是存储过程 查询统计并更新

```
CREATE OR REPLACE PROCEDURE SP_JSpjhgr
IS
kfxmNum NUMBER;
cursor c_job is
       select 项目编号,count(*) as XMN from errorrecords where  错误编号='10002' group by 项目编号;
c_row c_job%rowtype;
BEGIN
      for c_row in c_job loop
          if c_row.XMN <>0 then
          select count(*) into kfxmNum from errorrecords where 扣分状态='1' and 错误编号='10002' and 项目编号=c_row.项目编号;
          if kfxmNum<>0 then
          update magercfg set 信息=to_char(kfxmNum/c_row.XMN*100,'999D99') where 类型='pj' and 参数=to_char(c_row.项目编号);
          end if;
          end if;
      end loop;
END SP_JSpjhgr;
```
