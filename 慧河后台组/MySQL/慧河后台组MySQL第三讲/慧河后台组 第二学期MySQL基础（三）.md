# 慧河后台组 第二学期MySQL基础（三）

## 第三讲：运算符

### 一、算术运算符

算术运算符主要用于数学运算，其可以连接运算符前后的两个数值或表达式，对数值或表达式进行加 （+）、减（-）、乘（*）、除（/）和取模（%）运算。

> ![image-20230325112711392](assets\image-20230325112711392.png)

#### 1. 加法与减法运算符

```mysql
SELECT 100, 100 + 0, 100 - 0, 100 + 50, 100 + 50 -30, 100 + 35.5, 100 - 35.5
FROM DUAL;
```

> ![image-20230325112841462](assets\image-20230325112841462.png)

**结论：**

- 一个整数类型的值对整数进行加法和减法操作，结果还是一个整数；
- 一个整数类型的值对浮点数进行加法和减法操作，结果是一个浮点数；
- 加法和减法的优先级相同，进行先加后减操作与进行先减后加操作的结果是一样的；
- 在Java中，+的左右两边如果有字符串，那么表示字符串的拼接。但是在MySQL中+只表示数 值相加。如果遇到非数值类型，先尝试转成数值，如果转失败，就按0计算。（补充：MySQL 中字符串拼接要使用字符串函数CONCAT()实现）

#### 2. 乘法与除法运算符

```mysql
SELECT 100, 100 * 1, 100 * 1.0, 100 / 1.0, 100 / 2,100 + 2 * 5 / 2,100 /3, 100
DIV 0 FROM dual;
```

> ![image-20230325113048966](assets\image-20230325113048966.png)

**结论：**

- 一个数乘以整数1和除以整数1后仍得原数；
- 一个数乘以浮点数1和除以浮点数1后变成浮点数，数值与原数相等；
- 一个数除以整数后，不管是否能除尽，结果都为一个浮点数；
- 一个数除以另一个数，除不尽时，结果为一个浮点数，并保留到小数点后4位；
- 乘法和除法的优先级相同，进行先乘后除操作与先除后乘操作，得出的结果相同。
- 在数学运算中，0不能用作除数，在MySQL中，一个数除以0为NULL。

#### 3. 求模（求余）运算符

```mysql
SELECT 12 % 3, 12 MOD 5 FROM DUAL;
```

> ![image-20230325113227072](assets\image-20230325113227072.png)

**实例：**

```mysql
#筛选出employee_id是偶数的员工
SELECT * FROM employees
WHERE employee_id MOD 2 = 0;
```

### 二、比较运算符

- 比较运算符用来对表达式左边的操作数和右边的操作数进行比较，比较的结果为真则返回1，比较的结果 为假则返回0，其他情况则返回NULL。

-  比较运算符经常被用来作为SELECT查询语句的条件来使用，返回符合条件的结果记录。

> ![image-20230325113530535](assets\image-20230325113530535.png)

#### 1. 等号运算符

- 等号运算符（=）判断等号两边的值、字符串或表达式是否相等，如果相等则返回1，不相等则返回 0。
- 在使用等号运算符时，遵循如下规则：
  - 如果等号两边的值、字符串或表达式都为字符串，则MySQL会按照字符串进行比较，其比较的 是每个字符串中字符的ANSI编码是否相等。
  - 如果等号两边的值都是整数，则MySQL会按照整数来比较两个值的大小。
  - 如果等号两边的值一个是整数，另一个是字符串，则MySQL会将字符串转化为数字进行比较。
  - 如果等号两边的值、字符串或表达式中有一个为NULL，则比较结果为NULL。

- 对比：SQL中赋值符号使用 :=

```mysql
SELECT 1 = 1, 1 = '1', 1 = 0, 'a' = 'a', (5 + 3) = (2 + 6), '' = NULL , NULL = NULL;
```

> ![image-20230325113830912](assets\image-20230325113830912.png)

```mysql
SELECT 1 = 2, 0 = 'abc', 1 = 'abc' FROM dual;
```

> ![image-20230325113905875](assets\image-20230325113905875.png)

```mysql
#查询salary=10000
SELECT employee_id,salary FROM employees WHERE salary = 10000;
```

> ![image-20230325113956360](assets\image-20230325113956360.png)

#### 2. 安全等于运算符

安全等于运算符（<=>）与等于运算符（=）的作用是相似的，` 唯一的区别` 是‘<=>’可 以用来对NULL进行判断。在两个操作数均为NULL时，其返回值为1，而不为NULL；当一个操作数为NULL 时，其返回值为0，而不为NULL。

```mysql
 SELECT 1 <=> '1', 1 <=> 0, 'a' <=> 'a', (5 + 3) <=> (2 + 6), '' <=> NULL,NULL
<=> NULL FROM dual;
```

> ![image-20230325114132976](assets\image-20230325114132976.png)

```mysql
#查询commission_pct等于0.40
SELECT employee_id,commission_pct FROM employees WHERE commission_pct = 0.40;
SELECT employee_id,commission_pct FROM employees WHERE commission_pct <=> 0.40;
#如果把0.40改成 NULL 呢？
SELECT employee_id,commission_pct FROM employees WHERE commission_pct = NULL;
SELECT employee_id,commission_pct FROM employees WHERE commission_pct <=> NULL;
```

#### 3. 不等于运算符

不等于运算符（<>和!=）用于判断两边的数字、字符串或者表达式的值是否不相等， 如果不相等则返回1，相等则返回0。不等于运算符不能判断NULL值。如果两边的值有任意一个为NULL， 或两边都为NULL，则结果为NULL。

```mysql
 SELECT 1 <> 1, 1 != 2, 'a' != 'b', (3+4) <> (2+6), 'a' != NULL, NULL <> NULL;
```

> ![image-20230325114416908](assets\image-20230325114416908.png)



**此外，还有非符号类型的运算符：**

> ![image-20230325114515132](assets\image-20230325114515132.png)
>
> ![image-20230325114527793](assets\image-20230325114527793.png)

#### 4. 空运算符

空运算符（IS NULL或者ISNULL）判断一个值是否为NULL，如果为NULL则返回1，否则返回 0。

```mysql
SELECT NULL IS NULL, ISNULL(NULL), ISNULL('a'), 1 IS NULL;
```

> ![image-20230325114714527](assets\image-20230325114714527.png)

```mysql
#查询commission_pct等于NULL。比较如下的四种写法
SELECT employee_id,commission_pct FROM employees WHERE commission_pct IS NULL;
SELECT employee_id,commission_pct FROM employees WHERE commission_pct <=> NULL;
SELECT employee_id,commission_pct FROM employees WHERE ISNULL(commission_pct);
SELECT employee_id,commission_pct FROM employees WHERE commission_pct = NULL;
```

#### 5. 非空运算符

非空运算符（IS NOT NULL）判断一个值是否不为NULL，如果不为NULL则返回1，否则返 回0。 

```mysql
SELECT NULL IS NOT NULL, 'a' IS NOT NULL, 1 IS NOT NULL;
```

> ![image-20230325114949455](assets\image-20230325114949455.png)

```mysql
#查询commission_pct不等于NULL
SELECT employee_id,commission_pct FROM employees WHERE commission_pct IS NOT NULL;
SELECT employee_id,commission_pct FROM employees WHERE NOT commission_pct <=> NULL;
SELECT employee_id,commission_pct FROM employees WHERE NOT ISNULL(commission_pct);
```

#### 6. 最小值运算符

语法格式为：LEAST(值1，值2，...，值n)。其中，“值n”表示参数列表中有n个值。在有 两个或多个参数的情况下，返回最小值。

```mysql
SELECT LEAST (1,0,2), LEAST('b','a','c'), LEAST(1,NULL,2);
```

> ![image-20230325115246657](assets\image-20230325115246657.png)

由结果可以看到，当参数是整数或者浮点数时，LEAST将返回其中最小的值；当参数为字符串时，返回字 母表中顺序最靠前的字符；当比较值列表中有NULL时，不能判断大小，返回值为NULL。

#### 7.  最大值运算符

语法格式为：GREATEST(值1，值2，...，值n)。其中，n表示参数列表中有n个值。当有 两个或多个参数时，返回值为最大值。假如任意一个自变量为NULL，则GREATEST()的返回值为NULL。

```mysql
 SELECT GREATEST(1,0,2), GREATEST('b','a','c'), GREATEST(1,NULL,2);
```

> ![image-20230325115343537](assets\image-20230325115343537.png)

#### 8. BETWEEN AND运算符

BETWEEN运算符使用的格式通常为`SELECT D FROM TABLE WHERE C BETWEEN A AND B`，此时，当C大于或等于A，并且C小于或等于B时，结果为1，否则结果为0。

```mysql
SELECT 1 BETWEEN 0 AND 1, 10 BETWEEN 11 AND 12, 'b' BETWEEN 'a' AND 'c';
```

> ![image-20230325115521017](assets\image-20230325115521017.png)

```mysql
SELECT last_name, salary
FROM employees
WHERE salary BETWEEN 2500 AND 3500;
```

#### 9.  IN运算符

 IN运算符用于判断给定的值是否是IN列表中的一个值，当左侧和右侧都不是 `NULL` 时，右侧值列表中包含左侧的值时返回 `1`，否则返回 `0`。

当左侧操作数为 `NULL`，返回 `NULL`。

当右侧值列表含有 `NULL`，如果包括左侧的非 NULL 值，返回 `1`，否则返回 `NULL`

```mysql
SELECT 'a' IN ('a','b','c'), 1 IN (2,3), NULL IN ('a','b'), 'a' IN ('a', NULL);
```

> ![image-20230325120328565](assets\image-20230325120328565.png)

```mysql
SELECT employee_id, last_name, salary, manager_id
FROM employees
WHERE manager_id IN (100, 101, 201);
```

> ![image-20230325120435717](assets\image-20230325120435717.png)

#### 10. NOT IN运算符

NOT IN运算符用于判断给定的值是否不是IN列表中的一个值，如果不是IN列表中的一 个值，则返回1，否则返回0。

```mysql
SELECT 'a' NOT IN ('a','b','c'), 1 NOT IN (2,3);
```

> ![image-20230325120528464](assets\image-20230325120528464.png)

#### 11. LIKE运算符

LIKE运算符主要用来匹配字符串，通常用于模糊匹配，如果满足条件则返回1，否则返回 0。如果给定的值或者匹配条件为NULL，则返回结果为NULL。

LIKE运算符通常使用如下通配符：

```mysql
“%”：匹配0个或多个字符。
“_”：只能匹配一个字符。
```

```mysql
 SELECT NULL LIKE 'abc', 'abc' LIKE NULL;
```

> ![image-20230325120641266](assets\image-20230325120641266.png)

```mysql
SELECT first_name
FROM employees
WHERE first_name LIKE 'S%';
```

```mysql
SELECT last_name
FROM employees
WHERE last_name LIKE '_o%';
```

#### 12. ESCAPE

ESCAPE出现的意义就是来解决模糊匹配运算的冲突的。

- 如果使用\表示转义，要省略ESCAPE。如果不是\，则要加上ESCAPE。

```mysql
SELECT job_id
FROM jobs
WHERE job_id LIKE ‘IT\_%‘;
```

```mysql
SELECT job_id
FROM jobs
WHERE job_id LIKE ‘IT$_%‘ escape ‘$‘;
```

### 三、逻辑运算符

> 逻辑运算符主要用来判断表达式的真假，在MySQL中，逻辑运算符的返回结果为1、0或者NULL。

MySQL中支持4种逻辑运算符如下：

> ![image-20230325121027623](assets\image-20230325121027623.png)

#### 1. 逻辑非运算符

逻辑非（NOT或!）运算符表示当给定的值为0时返回1；当给定的值为非0值时返回0； 当给定的值为NULL时，返回NULL。

```mysql
SELECT NOT 1, NOT 0, NOT(1+1), NOT !1, NOT NULL;
```

> ![image-20230325121124517](assets\image-20230325121124517.png)

```mysql
SELECT last_name, job_id
FROM employees
WHERE job_id NOT IN ('IT_PROG', 'ST_CLERK', 'SA_REP');
```

> ![image-20230325121208164](assets\image-20230325121208164.png)

#### 2. 逻辑与运算符

 逻辑与（AND或&&）运算符是当给定的所有值均为非0值，并且都不为NULL时，返回 1；当给定的一个值或者多个值为0时则返回0；否则返回NULL。

```mysql
 SELECT 1 AND -1, 0 AND 1, 0 AND NULL, 1 AND NULL;
```

> ![image-20230325121316199](assets\image-20230325121316199.png)

```mysql
SELECT employee_id, last_name, job_id, salary
FROM employees
WHERE salary >=10000
AND job_id LIKE '%MAN%';
```

> ![image-20230325121355847](assets\image-20230325121355847.png)

#### 3. 逻辑或运算符

逻辑或（OR或||）运算符是当给定的值都不为NULL，并且任何一个值为非0值时，则返 回1，否则返回0；当一个值为NULL，并且另一个值为非0值时，返回1，否则返回NULL；当两个值都为 NULL时，返回NULL。

```mysql
SELECT 1 OR -1, 1 OR 0, 1 OR NULL, 0 || NULL, NULL || NULL;
```

> ![image-20230325121440444](assets\image-20230325121440444.png)

```mysql
#查询基本薪资不在9000-12000之间的员工编号和基本薪资
SELECT employee_id,salary FROM employees
WHERE NOT (salary >= 9000 AND salary <= 12000);

SELECT employee_id,salary FROM employees
WHERE salary <9000 OR salary > 12000;

SELECT employee_id,salary FROM employees
WHERE salary NOT BETWEEN 9000 AND 12000;
```

`注意： `

`OR可以和AND一起使用，但是在使用时要注意两者的优先级，由于AND的优先级高于OR，因此先对AND两边的操作数进行操作，再与OR中的操作数结合。`

#### 4. 逻辑异或运算符

逻辑异或（XOR）运算符是当给定的值中任意一个值为NULL时，则返回NULL；如果 两个非NULL的值都是0或者都不等于0时，则返回0；如果一个值为0，另一个值不为0时，则返回1。

```mysql
SELECT 1 XOR -1, 1 XOR 0, 0 XOR 0, 1 XOR NULL, 1 XOR 1 XOR 1, 0 XOR 0 XOR 0;
```

> ![image-20230325121612126](assets\image-20230325121612126.png)

### 四、位运算符

位运算符是在二进制数上进行计算的运算符。位运算符会先将操作数变成二进制数，然后进行位运算， 最后将计算结果从二进制变回十进制数。

由于不太常用， 遇到再自行了解即可。

> ![image-20230325121723016](assets\image-20230325121723016.png)

### 五、运算符的优先级

> ![image-20230325121811326](assets\image-20230325121811326.png)

数字编号越大，优先级越高，优先级高的运算符先进行计算。可以看到，赋值运算符的优先级最低，使 用“()”括起来的表达式的优先级最高。