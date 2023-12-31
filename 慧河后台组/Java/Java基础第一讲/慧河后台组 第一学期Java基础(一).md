# 慧河后台组 第一学期Java基础

## 第一讲：变量、运算符、表达式、输入与输出

### 一、编写一段简单的Java程序

```java
public class Main{
    public static void main(String[] args){
        System.out.println("Hello world");
    }
}//照着一个字一个字抄即可，别复制粘贴。
```

### 二、语法基础

##### 1.变量

变量必须先定义，才可以使用，不可以重名。

变量定义的方式：

```java
public class Main{
    public static void main(String[] args){
        int a = 5;
        int b, c = a, d = 10/2;
    }
}
```

内置数据类型：

| 类型         | 字节数 | 举例           |
| ------------ | ------ | -------------- |
| byte         | 1      | 123            |
| short        | 2      | 12345          |
| int          | 4      | 123456789      |
| long         | 8      | 1234567891011L |
| float        | 4      | 1.2F           |
| double       | 8      | 1.2, 1.2D      |
| boolean 布尔 | 1      | ture, false    |
| char         | 2      | 'A'            |

```java
// 字节(byte)  1 byte = 8 bit (计算机导论课应该都上过)
// float 的有效数字 大概是6~7位
// double 的有效数字大概是 15~16位
// char类型 是以数字映射存储的 详情可百度 ASCII 记：'a' == 97， 'A' == 65， '0' == 48；
```

常量：

使用 `final` 修饰：

```Java
final int N = 10；
```

类型转化：

- 显示转化：`int x = (int) 'A';`
- 隐式转化：`double x = 12, y = 4 * 3.3;`

##### 2. 运算符

`A = 10 , B = 20;`

| 运算符 | 描述                                             | 实例                                  |
| ------ | ------------------------------------------------ | ------------------------------------- |
| `+`    | 把两个数相加                                     | `A + B`将得到30                       |
| `-`    | 从第一个数中减去第二个数                         | `A - B`将得到 -10                     |
| `*`    | 把两个数相乘                                     | `A * B`将得到 200                     |
| `/`    | 分子除以分母                                     | `B / A`将得到 2                       |
| `%`    | 取模运算符，向零整除后的余数，注意余数可能为负数 | `B%A`将得到 0                         |
| `++`   | 自增运算符                                       | `A++`先取值后加1 ;`++A`;先加1后取值;  |
| `--`   | 自减运算符                                       | `A--` 先取值后减1; `--A` 先减1后取值; |
| `+=`   | 第一个数加上第二个数                             | `A = A + B`  可以简写为`A+=B`         |
| `-=`   | 第一个数减去第二个数                             | `A = A - B` 可以简写为 `A -= B`       |
| `*=`   | 第一个数乘以第二个数                             | `A = A * B`  可以简写为`A *= B`       |
| `/=`   | 第一个数除以第二个数                             | `A = A / B`  可以简写为`A /= B`       |
| `%=`   | 第一个对第二个数取余数                           | `A = A % B`  可以简写为`A%=B`         |

##### 3. 表达式

整数的加减乘除四则运算：

```java
public class Main{
    public static void main(String[] args){
        int a = 6 + 3 * 4 / 2 - 2;
        System.out.println(a);
        int b = a * 10 + 5 / 2;
        System.out.println(b);
        System.out.println(23 * 56 - 78 / 3);
    }
}
```

浮点数(小数) 的运算:

```java
public class Main{
    public static void main(String[] args){
        double x = 1.5, y = 3.2;
        System.out.println( x * y );
        System.out.println( x / y );
        System.out.println( x + y );
        System.out.println( x - y );
    }
}
```

整型变量的自增、自减：

```java
public class Main{
    public static void main(String[] args){
        int a = 1;
        int b = a++;
        System.out.println( a + " " + b );
        int c = ++a;
        System.out.println( a + " " + c );
    }
}
```

##### 4. 输入

方式1，效率较低，输入规模较小时使用(1e5)

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String str = sc.next( );//读入下一个字符串
        int x = sc.nextInt( ); //读入下一个整数
        float y = sc.nextFloat( );//读入下一个单精度浮点数
        double z = sc.nextDouble( ); //读入下一个双精度浮点数
        String line = sc.nextLine( );// 读入下一行
    }
}
```

方式2，效率较高，输入规模较大时使用。注意需要抛异常！！

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class Main{
    public static void mian(String[] args) throws Exception{
        BufferedReader br = new BufferedReader (new InputStreamReader(System.in));
        String str = br.readLine();
        System.out.println(str);
        
        //若想读入两行数字
        int x = Integer.parseInt(br.readLine());
        int y = Integer.parseInt(br.readLine());
        System.out.println(x + y);
        
        //若想读入一行的两个数字 则需手动分割一下
        String[] strs = br.readLine().split("  ");
        int x = Integer.parseInt(strs[0]);
        int y = Integer.parseInt(strs[1]);
        System.out.println(x + y);
    }
}
```

##### 5.输出

方式1，效率较低，输出规模较小时使用。（1e5）

```java
public class Main {
    public static void main(String[] args) throws Exception {
        System.out.println(123);  // 输出整数 + 换行
        System.out.println("Hello World");  // 输出字符串 + 换行
        System.out.print(123);  // 输出整数
        System.out.print("abc\n");  // 输出字符串
        System.out.printf("%04d %.2f\n", 4, 123.456D);  // 格式化输出，float与double都用%f输出
		//注意 %04d， %4d， %-4d的区别
    }
}
```

`System.out.printf()`中不同类型变量的输出格式：

(1) `int：%d`

(2)`float: %f`, 默认保留6位小数

(3)`double: %f`， 默认保留6位小数

(4)`char: %c`, 回车也是一个字符，用`'\n'`表示

(5)`String: %s`

方式2，效率较高，输出规模较大时使用。注意需要抛异常。

```java
import java.io.BufferedWriter;
import java.io.OutputStreamWriter;
public class Main{
    public static void main(String[] args) throws Exception{
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out);
        bw.write("Hello Huihe\n");
        bw.flush(); //需要手动刷新缓冲区
    }
}
```

