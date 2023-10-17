# 慧河后台组 第二学期MySQL基础（十）

##  一、插入数据

### 1.1 实际问题

> ![image-20230421215328768](assets\image-20230421215328768.png)

解决方式：使用 INSERT 语句向表中插入数据。

### 1.2 方式1：VALUES的方式添加

使用这种语法一次只能向表中插入**一条**数据。

**情况1：为表的所有字段按默认顺序插入数据**

```mysql
INSERT INTO 表名
VALUES (value1,value2,....);
```

值列表中需要为表的每一个字段指定值，并且值的顺序必须和数据表中字段定义时的顺序相同。

举例：

```mysql
INSERT INTO departments
VALUES (70, 'Pub', 100, 1700);
```

```mysql
INSERT INTO departments
VALUES (100, 'Finance', NULL, NULL);
```

**情况2：为表的指定字段插入数据**

```mysql
INSERT INTO 表名(column1 [, column2, …, columnn])
VALUES (value1 [,value2, …, valuen]);
```

为表的指定字段插入数据，就是在INSERT语句中只向部分字段中插入值，而其他字段的值为表定义时的 默认值。

在 INSERT 子句中随意列出列名，但是一旦列出，VALUES中要插入的value1,....valuen需要与 column1,...columnn列一一对应。如果类型不同，将无法插入，并且MySQL会产生错误。

举例：

```mysql
INSERT INTO departments(department_id, department_name)
VALUES (80, 'IT');
```

**情况3：同时插入多条记录**

INSERT语句可以同时向数据表中插入多条记录，插入时指定多个值列表，每个值列表之间用逗号分隔 开，基本语法格式如下：

```mysql
INSERT INTO table_name
VALUES
(value1 [,value2, …, valuen]),
(value1 [,value2, …, valuen]),
……
(value1 [,value2, …, valuen]);
```

或者

```mysql
INSERT INTO table_name(column1 [, column2, …, columnn])
VALUES
(value1 [,value2, …, valuen]),
(value1 [,value2, …, valuen]),
……
(value1 [,value2, …, valuen]);
```

举例：

```mysql
INSERT INTO emp(emp_id,emp_name)
VALUES (1001,'shkstart'),
(1002,'atguigu'),
(1003,'Tom');
```

> 一个同时插入多行记录的INSERT语句等同于多个单行插入的INSERT语句，但是多行的INSERT语句 在处理过程中 `效率更高` 。因为MySQL执行单条INSERT语句插入多行数据比使用多条INSERT语句 快，所以在插入多条记录时最好选择使用单条INSERT语句的方式插入。

**小结：**

- `VALUES` 也可以写成 `VALUE` ，但是VALUES是标准写法。
- 字符和日期型数据应包含在单引号中。

### 1.3 方式2：将查询结果插入到表中

INSERT还可以将SELECT语句查询的结果插入到表中，此时不需要把每一条记录的值一个一个输入，只需 要使用一条INSERT语句和一条SELECT语句组成的组合语句即可快速地从一个或多个表中向一个表中插入 多行。

基本语法格式如下：

```mysql
INSERT INTO 目标表名
(tar_column1 [, tar_column2, …, tar_columnn])
SELECT
(src_column1 [, src_column2, …, src_columnn])
FROM 源表名
[WHERE condition]
```

- 在 INSERT 语句中加入子查询
- 不必书写 VALUES 子句。
- 子查询中的值列表应与 INSERT 子句中的列名对应。

举例：

```mysql
INSERT INTO emp2
SELECT *
FROM employees
WHERE department_id = 90;
```

```mysql
INSERT INTO sales_reps(id, name, salary, commission_pct)
SELECT employee_id, last_name, salary, commission_pct
FROM employees
WHERE job_id LIKE '%REP%';
```

## 二、更新数据

> ![image-20230421220049029](assets\image-20230421220049029.png)

- 使用 UPDATE 语句更新数据。语法如下：

  ```mysql
  UPDATE table_name
  SET column1=value1, column2=value2, … , column=valuen
  [WHERE condition]
  ```

- 可以一次更新`多条`数据。

- 如果需要回滚数据，需要保证在DML前，进行设置：`SET AUTOCOMMIT = FALSE;`

- 使用 `WHERE` 子句指定需要更新的数据。

  ```mysql
  UPDATE employees
  SET department_id = 70
  WHERE employee_id = 113;
  ```

- 如果省略 WHERE 子句，则表中的所有数据都将被更新。

  ```mysql
  UPDATE copy_emp
  SET department_id = 110;
  ```

- **更新中的数据完整性错误**

  ```mysql
  UPDATE employees
  SET department_id = 55
  WHERE department_id = 110;
  ```

  > 说明：不存在 55 号部门

## 三、删除数据

> ![image-20230421220320200](assets\image-20230421220320200.png)

- 使用 DELETE 语句从表中删除数据
  ![image-20230421220358302](assets\image-20230421220358302.png)

  ```mysql
  DELETE FROM table_name [WHERE <condition>];
  ```

  table_name指定要执行删除操作的表；“[WHERE ]”为可选参数，指定删除条件，如果没有WHERE子句， DELETE语句将删除表中的所有记录。

- 使用 WHERE 子句删除指定的记录。

  ```mysql
  DELETE FROM departments
  WHERE department_name = 'Finance';
  ```

- 如果省略 WHERE 子句，则表中的全部数据将被删除

  ```mysql
  DELETE FROM copy_emp;
  ```

- **删除中的数据完整性错误**

  ```mysql
  DELETE FROM departments
  WHERE department_id = 60;
  ```

  > 说明：You cannot delete a row that contains a primary key that is used as a foreign key in another table.