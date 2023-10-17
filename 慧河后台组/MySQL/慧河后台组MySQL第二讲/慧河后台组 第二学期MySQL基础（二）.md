# 慧河后台组 第二学期MySQL基础（二）

## 第二讲：简单的SELECT语句

### 一：导入数据库

法一：用cmd命令行导入

![image-20230322170217057](assets\image-20230322170217057.png)

然后会弹很多行指令， 等指令结束后即导入成功。

法二：利用图形化界面导入

![image-20230322170525543](assets\image-20230322170525543.png)

导入成功后重启SQLyog即可完成。

### 二：简单的SELECT语句

#### 2.0 SELECT ...

```mysql
SELECT 1; #没有任何子句
SELECT 1 + 1 ; #没有任何子句
```

#### 2.1 SELECT ... FROM

- 语法：

  ```mysql
  SELECT 标识选择哪些列
  FROM 标识从哪个表中选择
  ```

- 选择全部列：

  ```mysql
  SELECT *
  FROM employees;
  ```

  > ![image-20230322171132613](assets\image-20230322171132613.png)

- 选择特定的列：

  ```mysql
  SELECT employee_id, first_name, last_name
  FROM employees;
  ```

  > ![image-20230322171236160](assets\image-20230322171236160.png)

#### 2.2 列的别名

- 重命名一个列

- 便于计算

- 紧跟列名，也可以在**列名和别名之间加入关键字AS，别名使用双引号**，以便在别名中包含空格或特殊的字符并区分大小写。

- AS可以省略

- 建议别名简短，见名知意

- 例子：

  ```mysql
  SELECT employee_id emp_id, last_name AS "lname", salary * 12 "Anuual Salary"
  FROM employees;			
  ```

  > ![image-20230322171736133](assets\image-20230322171736133.png)

#### 2.3 去除重复行：

默认情况下， 查询会返回全部行， 包括重复行

这时可以使用关键字 `DISTINCT`去除重复行

```mysql
SELECT DISTINCT department_id
FROM employees;
```

> ![](assets\image-20230322171935608.png)

#### 2.4 空值参与运算

- 所有运算符或列值遇到null值， 运算的结果都为null

  ```mysql
  SELECT employee_id,salary,commission_pct,
  12 * salary * (1 + commission_pct) "annual_sal"
  FROM employees;
  ```

- 注意：
  null 不等于 0 也不等于“” 更不等于“null”！！！！！

#### 2.5 着重号：

- 意义：
  着重号的意义就是用来解决起名字冲突的

- 例子：

  ```mysql
  SELECT * 
  FROM ORDER;
  
  SELECT * 
  FROM `order`;
  ```

  这两条语句运行结果显然不同， 同学们请自行尝试。

#### 2.6 查询常数

所谓的查询常数就是指在SELECT的查询结果中添加一列常数列，这列的值是我们指定的而不是从表中动态抓取的。

例子：

```mysql
SELECT 'huihe' AS "组织", employee_id, last_name
FROM employees;
```

### 三：显示表结构

`使用DESCRIBE 或 DESC 命令，表示表结构。`

```mysql
DESCRIBE employees;
或
DESC employees;
```

> ![image-20230322173109875](assets\image-20230322173109875.png)

其中，各个字段的含义分别解释如下：

- Field：表示字段名称。 
- Type：表示字段类型。
- Null：表示该列是否可以存储NULL值。 
- Key：表示该列是否已编制索引。PRI表示该列是表主键的一部分；UNI表示该列是UNIQUE索引的一 部分；MUL表示在列中某个给定值允许出现多次。 
- Default：表示该列是否有默认值，如果有，那么值是多少。 
- Extra：表示可以获取的与给定列有关的附加信息，例如AUTO_INCREMENT等。

### 四：过滤数据

- 背景：

> ![image-20230325111114077](assets\image-20230325111114077.png)

- 语法：

  ```mysql
  SELECT 字段1,字段2
  FROM 表名
  WHERE 过滤条件
  ```

  - 使用WHERE 子句，将不满足条件的行过滤掉
  - WHERE子句紧随 FROM子句

- 举例：

  ```mysql
  SELECT employee_id, first_name, last_name, department_id
  FROM employees
  WHERE department_id = 90;
  ```

  > ![image-20230325111459220](assets\image-20230325111459220.png)