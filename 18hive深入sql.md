##  聚合函数
> where  xx=1  having  sum(xxx)>100;
```
select ename, salary, 
       case
        when salary > 1 and salary <= 1000 then 'LOWER'
        when salary > 1000 and salary <= 2000 then 'MIDDLE'
        when salary > 2000 and salary <= 4000 then 'HIGH'
        else 'HIGHEST'
       end
from   ruozedata_emp4;



```


join
create table  a (id  int,name string)
row  format  delimited fields  terminated by '\t';
create table  b (id  int,age int)
row  format  delimited fields  terminated by '\t';


插入的数据 用tab键  隔开  隔开！！！！

load data local inpath '/home/hadoop/data/1.txt' overwrite into table a;



### 分区表
