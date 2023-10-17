# 慧河后台组 第二学期MySQL基础（四）

## 第四讲：排序与分页

### 一、排序数据

#### 1.1 排序规则

- 使用ORDER BY子句排序
  - ASC (ascend) : 升序
  - DESC (descend) : 降序
- ORDER BY 子句在SELECT语句的结尾。

#### 1.2 单列排序

```mysql
SELECT last_name, job_id, department_id, hire_date
FROM employees
ORDER BY hire_date ;
```

> ![image-20230401090411784](assets\111.png)

```mysql
SELECT last_name, job_id, department_id, hire_date
FROM employees
ORDER BY hire_date DESC ;
```

> ![image-20230401090510749](assets\image-20230401090510749.png)

#### 1.3 多列排序

```mysql
SELECT last_name, department_id, salary
FROM employees
ORDER BY department_id, salary DESC;
```

> ![image-20230401090616989](assets\image-20230401090616989.png)

- 可以使用不在SELECT列表中的列排序。
- 在对多列进行排序的时候，首先排序的第一列必须有相同的列值，才会对第二列进行排序。如果第 一列数据中所有值都是唯一的，将不再对第二列进行排序。

### 二、分页

#### 2.1 背景

- 查询返回的记录太多了，查看起来很不方便，怎么样能够实现分页查询呢？
- 表里有 4 条数据，我们只想要显示第 2、3 条数据怎么办呢？

#### 2.2  实现规则

- 分页原理
  所谓分页显示，就是将数据库中的结果集，一段一段显示出来需要的条件。

- MySQL中使用 LIMIT 实现分页

- 格式：

  ```mysql
  LIMIT [位置偏移量,] 行数
  ```

  第一个“位置偏移量”参数指示MySQL从哪一行开始显示，是一个可选参数，如果不指定“位置偏移 量”，将会从表中的第一条记录开始（第一条记录的位置偏移量是0，第二条记录的位置偏移量是 1，以此类推）；第二个参数“行数”指示返回的记录条数。

- 举例：

  ```mysql
  --前10条记录：
  SELECT * FROM 表名 LIMIT 0,10;
  或者
  SELECT * FROM 表名 LIMIT 10;
  --第11至20条记录：
  SELECT * FROM 表名 LIMIT 10,10;
  --第21至30条记录：
  SELECT * FROM 表名 LIMIT 20,10;
  ```

- 分页显式公式：（当前页数-1）*每页条数，每页条数

  ```mysql
  SELECT * FROM table
  LIMIT(PageNo - 1)*PageSize,PageSize;
  ```

- 注意：LIMIT 子句必须放在整个SELECT语句的最后！

- 使用 LIMIT 的好处
  约束返回结果的数量可以 `减少数据表的网络传输量` ，也可以 `提升查询效率` 。如果我们知道返回结果只有 1 条，就可以使用 `LIMIT 1` ，告诉 SELECT 语句只需要返回一条记录即可。这样的好处就是 SELECT 不需 要扫描完整的表，只需要检索到一条符合条件的记录即可返回。