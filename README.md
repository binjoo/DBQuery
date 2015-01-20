# DBQuery
参照Typecho的SQL构建类而写的JAVA版

## 查询语句
#### 简单查询
```java
DBQuery q = new DBQuery();
q.select().from("table_name");
System.out.println(q.build());
```
> `SQL: `select * from table_name

#### 指定字段查询
```java
DBQuery q = new DBQuery();
String[] n = {"name", "username"};
q.select("id", n, "pass as password").from("table_name");
System.out.println(q.build());
```
> `SQL: `select id , name as username , pass as password from table_name

#### 带有条件查询
```java
DBQuery q = new DBQuery();
q.select("id", "name", "pass").from("table_name");
q.where("age > 21 or age = ?", 18);
q.where("sex = ?", "男");
q.where("name like '%杰伦%'");
q.where("name like '%' || ? || '%'", "周");
System.out.println(q.build());
```

> `SQL: `select id , name , pass from table_name where (age > 21 or age = ?) and (sex = ?) and (name like '%杰伦%') and (name like '%' || ? || '%')
> `Params: `{ 18, "男", "周" }

#### 根据排序查询
```java
DBQuery q = new DBQuery();
q.select("id", "name", "pass").from("table_name");
q.order("id").order("name", DBQuery.SORT_DESC);
System.out.println(q.build());
```
> `SQL: `select id , name , pass from table_name order by id asc, name desc
