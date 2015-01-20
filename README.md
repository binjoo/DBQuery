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
String[] p = {"pass", "password"};
q.select("id", n, p).from("table_name");
System.out.println(q.build());
```
> `SQL: `select id , name as username , pass as password from table_name

#### 带有条件查询
```java
DBQuery q = new DBQuery();
q.select("id", "name", "pass").from("table_name");
q.where("age > 21").where("sex = ?", 2);
System.out.println("`SQL: `" + q.build());
```

> `SQL: `select id , name , pass from table_name where (age > 21) and (sex = ?)

> `Params: `{ 2 }
