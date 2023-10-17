# 慧河后台组 第二学期MySQL基础（五）

## 第五讲：多表查询

> 多表查询，也称为关联查询，指两个或更多个表一起完成查询操作。
>
> 前提条件：这些一起查询的表之间是有关系的（一对一、一对多），它们之间一定是有关联字段，这个 关联字段可能建立了外键，也可能没有建立外键。比如：员工表和部门表，这两个表依靠“部门编号”进 行关联。

### 一、一个案例引发的多表连接

#### 1.1 案例说明：

```mysql
#案例：查询员工的姓名及其部门名称
SELECT last_name, department_name
FROM employees, departments;
```

> 理想情况：
> ![image-20230401091829961](assets\image-20230401091829961.png)

> 现实情况：
> ![image-20230401091853962](assets\image-20230401091853962.png)

**分析错误情况**：

```mysql
SELECT COUNT(employee_id) FROM employees;
#输出107行
SELECT COUNT(department_id)FROM departments;
#输出27行
SELECT 107*27 FROM dual;
```

错误原因：缺少表的连接条件

我们把上述多表查询中出现的问题称为：笛卡尔积的错误。

#### 1.2 笛卡尔积（或交叉连接）的理解

笛卡尔乘积是一个数学运算。假设我有两个集合 X 和 Y，那么 X 和 Y 的笛卡尔积就是 X 和 Y 的所有可能 组合，也就是第一个对象来自于 X，第二个对象来自于 Y 的所有可能。组合的个数即为两个集合中元素 个数的乘积数。

> ![image-20230401092231361](assets\image-20230401092231361.png)

#### 1.3案例分析与问题解决

- 笛卡尔积的错误会在下面条件下产生：

  - 省略多个表的连接条件（或关联条件）
  - 连接条件（或关联条件）无效
  - 所有表中的所有行互相连接

- 为了避免笛卡尔积， 可以在 WHERE 加入有效的连接条件。

- 加入连接条件后，查询语法：

  ```mysql
  SELECT table1.column, table2.column
  FROM table1, table2
  WHERE table1.column1 = table2.column2; #连接条件
  ```

  - 在 WHERE子句中写入连接条件。

- 正确写法：

  ```mysql
  #案例：查询员工的姓名及其部门名称
  SELECT last_name, department_name
  FROM employees, departments
  WHERE employees.department_id = departments.department_id;
  ```

- 在表中有相同列时，在列名之前加上表名前缀。

### 二、多表查询分类讲解

#### 类型一：等值连接与非等值连接

**等值连接**

```mysql
SELECT employees.employee_id, employees.last_name,
employees.department_id, departments.department_id,
departments.location_id
FROM employees, departments
WHERE employees.department_id = departments.department_id;
```

> ![image-20230401093009830](assets\image-20230401093009830.png)

- 多个表中有相同列时，必须在列名之前加上表名前缀。
- 在不同表中具有相同列名的列可以用 表名 加以区分。

```mysql
SELECT employees.last_name, departments.department_name,employees.department_id
FROM employees, departments
WHERE employees.department_id = departments.department_id;
```

- 使用别名可以简化查询。
- 列名前使用表名前缀可以提高查询效率。

```mysql
SELECT e.employee_id, e.last_name, e.department_id,
d.department_id, d.location_id
FROM employees e , departments d
WHERE e.department_id = d.department_id;	
```

> 需要注意的是，如果我们使用了表的别名，在查询字段中、过滤条件中就只能使用别名进行代替， 不能使用原有的表名，否则就会报错。

- 连接多个表

  > ![image-20230401093210813](assets\image-20230401093210813.png)

  连接 n个表,至少需要n-1个连接条件。比如，连接三个表，至少需要两个连接条件。

- 练习：查询出公司员工的 last_name,department_name, city

**非等值连接**

> ![image-20230401093801778](assets\image-20230401093801778.png)

```mysql
SELECT e.last_name, e.salary, j.grade_level
FROM employees e, job_grades j
WHERE e.salary BETWEEN j.lowest_sal AND j.highest_sal;
```

> ![image-20230401093827676](assets\image-20230401093827676.png)

#### 类型二：自连接与非自连接

前面写的都是非自连接

自己表与自己表连接叫做自连接

> 题目：查询employees表，返回 员工姓名以及管理者姓名

#### 类型三：内连接和外连接

- 内连接: 合并具有同一列的两个以上的表的行, 结果集中不包含一个表与另一个表不匹配的行
- 外连接: 两个表在连接过程中除了返回满足连接条件的行以外还返回左（或右）表中不满足条件的 行 ，这种连接称为左（或右） 外连接。没有匹配的行时, 结果表中相应的列为空(NULL)。
- 如果是左外连接，则连接条件中左边的表也称为 主表 ，右边的表称为 从表 。
  如果是右外连接，则连接条件中右边的表也称为 主表 ，左边的表称为 从表 。
  都要的话叫做满外连接

### 三、SQL99语法实现多表查询

#### 3.1 基本语法

- 使用JOIN...ON子句创建连接的语法结构：

  ```mysql
  SELECT table1.column, table2.column,table3.column
  FROM table1
  	JOIN table2 ON table1 和 table2 的连接条件
  		JOIN table3 ON table2 和 table3 的连接条件
  ```

- 语法说明：

  - 可以使用 ON 子句指定额外的连接条件。
  - 这个连接条件是与其它条件分开的。
  - ON 子句使语句具有更高的易读性。
  - 关键字 JOIN、INNER JOIN、CROSS JOIN 的含义是一样的，都表示内连接

#### 3.2 内连接(INNER JOIN)的实现

- 语法：

  ```mysql
  SELECT 字段列表
  FROM A表 INNER JOIN B表
  ON 关联条件
  WHERE 等其他子句;
  ```

题目1：

```mysql
SELECT e.employee_id, e.last_name, e.department_id,
d.department_id, d.location_id
FROM employees e JOIN departments d
ON (e.department_id = d.department_id);
```

> ![image-20230401095346464](assets\image-20230401095346464.png)

题目2：

```mysql
SELECT employee_id, city, department_name
FROM employees e
JOIN departments d
ON d.department_id = e.department_id
JOIN locations l
ON d.location_id = l.location_id;
```

> ![image-20230401095419666](assets\image-20230401095419666.png)

#### 3.3 外连接(OUTER JOIN)的实现

##### 3.3.1 左外连接(LEFT OUTER JOIN)

- 语法：

  ```mysql
  #实现查询结果是A
  SELECT 字段列表
  FROM A表 LEFT JOIN B表
  ON 关联条件
  WHERE 等其他子句;
  ```

- 举例：

  ```mysql
  SELECT e.last_name, e.department_id, d.department_name
  FROM employees e
  LEFT OUTER JOIN departments d
  ON (e.department_id = d.department_id) ;
  ```

  > ![image-20230401095552081](assets\image-20230401095552081.png)

##### 3.3.2 右外连接(RIGHT OUTER JOIN)

- 语法：

  ```mysql
  #实现查询结果是B
  SELECT 字段列表
  FROM A表 RIGHT JOIN B表
  ON 关联条件
  WHERE 等其他子句;
  ```

- 举例：

  ```mysql
  SELECT e.last_name, e.department_id, d.department_name
  FROM employees e
  RIGHT OUTER JOIN departments d
  ON (e.department_id = d.department_id) ;
  ```

  > ![image-20230401095704480](assets\image-20230401095704480.png)

##### 3.3.3 满外连接(FULL OUTER JOIN)

- 满外连接的结果 = 左右表匹配的数据 + 左表没有匹配到的数据 + 右表没有匹配到的数据。
- SQL99是支持满外连接的。使用FULL JOIN 或 FULL OUTER JOIN来实现。
- 需要注意的是，MySQL不支持FULL JOIN，但是可以用 LEFT JOIN UNION RIGHT join代替。

### 四、UNION的使用

`合并查询结果 `利用UNION关键字，可以给出多条SELECT语句，并将它们的结果组合成单个结果集。合并 时，两个表对应的列数和数据类型必须相同，并且相互对应。各个SELECT语句之间使用UNION或UNION ALL关键字分隔。

语法格式：

```mysql
SELECT column,... FROM table1
UNION [ALL]
SELECT column,... FROM table2
```

> UNION
>
> ![image-20230401100937973](assets\image-20230401100937973.png)
>
> UNION 操作符返回两个查询的结果集的并集，去除重复记录。

> UNION ALL
>
> ![image-20230401100954039](assets\image-20230401100954039.png)
>
> UNION ALL操作符返回两个查询的结果集的并集。对于两个结果集的重复部分，不去重。

注意：执行UNION ALL语句时所需要的资源比UNION语句少。如果明确知道合并数据后的结果数据 `不存在重复数据`，或者不需要去除重复的数据，则尽量使用UNION ALL语句，以提高数据查询的效率。

例题：

查询部门编号>90或邮箱包含a的员工信息

```mysql
SELECT * FROM employees WHERE email LIKE '%a%' OR department_id>90;
```

```mysql
SELECT * FROM employees WHERE email LIKE '%a%'
UNION
SELECT * FROM employees WHERE department_id>90;
```

### 五、 7种SQL JOINS的实现

> ![image-20230401101149394](assets\image-20230401101149394.png)

### 六、SQL99语法新特性

#### 6.1 自然连接

SQL99 在 SQL92 的基础上提供了一些特殊语法，比如 `NATURAL JOIN `用来表示自然连接。我们可以把 自然连接理解为 SQL92 中的等值连接。它会帮你自动查询两张连接表中 `所有相同的字段` ，然后进行 `等值 连接` 。

在SQL92标准中：

```mysql
SELECT employee_id,last_name,department_name
FROM employees e JOIN departments d
ON e.`department_id` = d.`department_id`
AND e.`manager_id` = d.`manager_id`;
```

在 SQL99 中你可以写成：

```mysql
SELECT employee_id,last_name,department_name
FROM employees e NATURAL JOIN departments d;
```

#### 6.2 USING连接

当我们进行连接的时候，SQL99还支持使用 USING 指定数据表里的` 同名字段` 进行等值连接。但是只能配 合JOIN一起使用。比如：

```mysql
SELECT employee_id,last_name,department_name
FROM employees e JOIN departments d
USING (department_id);
```

你能看出与自然连接 NATURAL JOIN 不同的是，USING 指定了具体的相同的字段名称，你需要在 USING 的括号 () 中填入要指定的同名字段。同时使用` JOIN...USING `可以简化 JOIN ON 的等值连接。它与下 面的 SQL 查询结果是相同的：

```mysql
SELECT employee_id,last_name,department_name
FROM employees e ,departments d
WHERE e.department_id = d.department_id;
```

