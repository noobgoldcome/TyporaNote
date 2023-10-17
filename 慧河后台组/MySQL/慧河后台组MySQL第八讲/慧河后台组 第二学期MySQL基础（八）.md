# 慧河后台组 第二学期MySQL基础（八）

子查询指一个查询语句嵌套在另一个查询语句内部的查询，这个特性从MySQL 4.1开始引入。 SQL 中子查询的使用大大增强了 SELECT 查询的能力，因为很多时候查询需要从结果集中获取数据，或者 需要从同一个表中先计算得出一个数据结果，然后与这个数据结果（可能是某个标量，也可能是某个集合）进行比较。

## 一、 需求分析与问题解决

### 1.1 实际问题

![image-20230415151922600](assets\image-20230415151922600.png)

现有解决方式：

```mysql
#方式一：
SELECT salary
FROM employees
WHERE last_name = 'Abel';
SELECT last_name,salary
FROM employees
WHERE salary > 11000;
#方式二：自连接
SELECT e2.last_name,e2.salary
FROM employees e1,employees e2
WHERE e1.last_name = 'Abel'
AND e1.`salary` < e2.`salary`
#方式三：子查询
SELECT last_name,salary
FROM employees
WHERE salary > (
SELECT salary
FROM employees
WHERE last_name = 'Abel'
);
```

![image-20230415152122349](assets\image-20230415152122349.png)

### 1.2 子查询的基本使用

![image-20230415152152243](assets\image-20230415152152243.png)

- 子查询（内查询）在主查询之前一次执行完成。
- 子查询的结果被主查询（外查询）使用 。
- 注意事项
  - 子查询要包含在括号内
  - 将子查询放在比较条件的右侧
  - 单行操作符对应单行子查询，多行操作符对应多行子查询

### 1.3 子查询的分类

**分类方式1：**

我们按内查询的结果返回一条还是多条记录，将子查询分为 `单行子查询` 、 `多行子查询` 。

- 单行子查询
  ![image-20230415152255618](assets\image-20230415152255618.png)
- 多行子查询
  ![image-20230415152305709](assets\image-20230415152305709.png)

**分类方式2：**

我们按内查询是否被执行多次，将子查询划分为 `相关(或关联)子查询` 和 `不相关(或非关联)子查询` 。

子查询从数据表中查询了数据结果，如果这个数据结果只执行一次，然后这个数据结果作为主查询的条 件进行执行，那么这样的子查询叫做不相关子查询。

同样，如果子查询需要执行多次，即采用循环的方式，先从外部查询开始，每次都传入子查询进行查 询，然后再将结果反馈给外部，这种嵌套的执行方式就称为相关子查询。'

## 二、 单行子查询

### 2.1 单行比较操作符

![image-20230415152507839](assets\image-20230415152507839.png)

### 2.2 代码示例

**题目：查询工资大于149号员工工资的员工的信息**

![image-20230415152530071](assets\image-20230415152530071.png)

**题目：返回job_id与141号员工相同，salary比143号员工多的员工姓名，job_id和工资**

```mysql
SELECT last_name, job_id, salary
FROM employees
WHERE job_id =
(SELECT job_id
FROM employees
WHERE employee_id = 141)
AND salary >
(SELECT salary
FROM employees
WHERE employee_id = 143);
```

![image-20230415152616481](assets\image-20230415152616481.png)

**题目：返回公司工资最少的员工的last_name,job_id和salary**

```mysql
SELECT last_name, job_id, salary
FROM employees
WHERE salary =
(SELECT MIN(salary)
FROM employees);
```

![image-20230415152711802](assets\image-20230415152711802.png)

### 2.3 HAVING 中的子查询

- 首先执行子查询。
- 向主查询中的HAVING 子句返回结果。

**题目：查询最低工资大于50号部门最低工资的部门id和其最低工资**

```mysql
SELECT department_id, MIN(salary)
FROM employees
GROUP BY department_id
HAVING MIN(salary) >
(SELECT MIN(salary)
FROM employees
WHERE department_id = 50);
```

![image-20230415153019089](assets\image-20230415153019089.png)

## 三、 多行子查询

- 也称为集合比较子查询
- 内查询返回多行
- 使用多行比较操作符

### 3.1 多行比较操作符

![image-20230415153119480](assets\image-20230415153119480.png)

> 注意ANY 和 ALL的区别

### 3.2 代码示例

**题目：返回其它job_id中比job_id为‘IT_PROG’部门任一工资低的员工的员工号、姓名、job_id 以及salary**

```mysql
SELECT employee_id, last_name, job_id, salary
FROM employees
WHERE salary < ANY
		  (SELECT salary
		  FROM employees
		  WHERE job_id = 'IT_PROG'
		  )
AND job_id <> 'IT_PROG';
```

![image-20230417200654321](assets\image-20230417200654321.png)

**题目：返回其它job_id中比job_id为‘IT_PROG’部门所有工资都低的员工的员工号、姓名、job_id以及 salary**

```mysql
SELECT employee_id, last_name, job_id, salary
FROM employees
WHERE salary < ALL
		  (
		  SELECT salary
		  FROM employees
		  WHERE job_id = 'IT_PROG'
		  )
AND job_id <> 'IT_PROG';
```

![image-20230417200859388](assets\image-20230417200859388.png)

## 四、相关子查询

### 4.1 相关子查询执行流程	

如果子查询的执行依赖于外部查询，通常情况下都是因为子查询中的表用到了外部的表，并进行了条件 关联，因此每执行一次外部查询，子查询都要重新计算一次，这样的子查询就称之为 `关联子查询` 。

相关子查询按照一行接一行的顺序执行，主查询的每一行都执行一次子查询。

![image-20230417201041415](assets\image-20230417201041415.png)

![image-20230417201056110](assets\image-20230417201056110.png)

说明：**子查询中使用主查询中的列**

### 4.2 代码示例

**题目：查询员工中工资大于本部门平均工资的员工的last_name,salary和其department_id**

**方式一：相关子查询**

```mysql
SELECT last_name, salary, department_id
FROM employees `outer`
WHERE salary > 
	      (
	      SELECT AVG(salary)
	      FROM employees
	      WHERE department_id = outer.department_id
	      );
```

![image-20230417201335095](assets\image-20230417201335095.png)

**方式二：在 FROM 中使用子查询**

```mysql
SELECT last_name,salary,e1.department_id
FROM employees e1,(SELECT department_id,AVG(salary) dept_avg_sal FROM employees GROUP
BY department_id) e2
WHERE e1.`department_id` = e2.department_id
AND e2.dept_avg_sal < e1.`salary`;
```

> from型的子查询：子查询是作为from的一部分，子查询要用()引起来，并且要给这个子查询取别 名， 把它当成一张“临时的虚拟的表”来使用。

在ORDER BY 中使用子查询：

**题目：查询员工的id,salary,按照department_name 排序**

```mysql
SELECT employee_id,salary
FROM employees e
ORDER BY (
SELECT department_name
FROM departments d
WHERE e.`department_id` = d.`department_id`
);
```

![image-20230417201546569](assets\image-20230417201546569.png)

**题目：若employees表中employee_id与job_history表中employee_id相同的数目不小于2，输出这些相同 id的员工的employee_id,last_name和其job_id**

```mysql
SELECT e.employee_id, last_name,e.job_id
FROM employees e
WHERE 2 <= (SELECT COUNT(*)
FROM job_history
WHERE employee_id = e.employee_id);
```

![image-20230417201721688](assets\image-20230417201721688.png)

### 4.3 EXISTS 与 NOT EXISTS关键字

- 关联子查询通常也会和 EXISTS操作符一起来使用，用来检查在子查询中是否存在满足条件的行。
- 如果在子查询中不存在满足条件的行：
  - 条件返回 FALSE
  - 继续在子查询中查找
- 如果在子查询中存在满足条件的行：
  - 不在子查询中继续查找
  - 条件返回 TRUE
- NOT EXISTS关键字表示如果不存在某种条件，则返回TRUE，否则返回FALSE。

**题目：查询公司管理者的employee_id，last_name，job_id，department_id信息**

方式一：

```mysql
SELECT employee_id, last_name, job_id, department_id
FROM employees e1
WHERE EXISTS ( SELECT *
FROM employees e2
WHERE e2.manager_id =
e1.employee_id);
```

方式二：自连接

```mysql
SELECT DISTINCT e1.employee_id, e1.last_name, e1.job_id, e1.department_id
FROM employees e1 JOIN employees e2
WHERE e1.employee_id = e2.manager_id;
```

方式三：

```mysql
SELECT employee_id,last_name,job_id,department_id
FROM employees
WHERE employee_id IN (
SELECT DISTINCT manager_id
FROM employees
);
```

**题目：查询departments表中，不存在于employees表中的部门的department_id和department_name**

```mysql
SELECT department_id, department_name
FROM departments d
WHERE NOT EXISTS (SELECT 'X'
FROM employees
WHERE department_id = d.department_id);
```

### 4.4 相关更新

```mysql
UPDATE table1 alias1
SET column = (SELECT expression
FROM table2 alias2
WHERE alias1.column = alias2.column);
```

使用相关子查询依据一个表中的数据更新另一个表的数据。

**题目：在employees中增加一个department_name字段，数据为员工对应的部门名称**

```mysql
# 1）
ALTER TABLE employees
ADD(department_name VARCHAR2(14));
# 2）
UPDATE employees e
SET department_name = (SELECT department_name
FROM departments d
WHERE e.department_id = d.department_id);
```

### 4.5 相关删除

```mysql
DELETE FROM table1 alias1
WHERE column operator (SELECT expression
FROM table2 alias2
WHERE alias1.column = alias2.column);
```

使用相关子查询依据一个表中的数据删除另一个表的数据。

**题目：删除表employees中，其与emp_history表皆有的数据**

```mysql
DELETE FROM employees e
WHERE employee_id in
(SELECT employee_id
FROM emp_history
WHERE employee_id = e.employee_id);
```

