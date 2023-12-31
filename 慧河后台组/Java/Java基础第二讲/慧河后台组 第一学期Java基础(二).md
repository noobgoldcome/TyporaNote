# 慧河后台组 第一学期Java基础(二)

## 第二讲：判断语句

### 一、if 语句

##### 1. 基本if-else语句

当条件成立时，执行某些语句；否则执行另一些语句。

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        if (a > 5) {
            System.out.printf("%d is big!\n", a);
            System.out.printf("%d + 1 = %d\n", a, a + 1);
        } else {
            System.out.printf("%d is small!\n", a);
            System.out.printf("%d - 1 = %d\n", a, a - 1);
        }
    }
}
```

`else`可以省略

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        if (a > 5) {
            System.out.printf("%d is big!\n", a);
            System.out.printf("%d + 1 = %d\n", a, a + 1);
        } 
    }
}
```

当只有一条语句的时候， 大括号可以省略

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        if (a > 5) 
            System.out.printf("%d is big!\n", a);
        else 
            System.out.printf("%d is small!\n", a);
    }
}
```

练习：输入一个整数，输出这个数的绝对值。

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int x = sc.nextInt();

        if (x > 0)
            System.out.println(x);
        else
            System.out.println(-x);
    }
}
```

练习：输入两个整数，输出两个数中较大的那个。

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt(), b = sc.nextInt();

        if (a > b)
            System.out.println(a);
        else
            System.out.println(b);
    }
}
```

`if-else`语句内部也可以是`if-else`语句。( 可嵌套的 )

练习：输入三个整数，输出三个数中最大的那个。

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt(), b = sc.nextInt(), c = sc.nextInt();

        if (a > b) {
            if (a > c)
                System.out.println(a);
            else
                System.out.println(c);
        } else {
            if (b > c)
                System.out.println(b);
            else
                System.out.println(c);
        }
    }
}
```

##### 2. 常用比较运算符

(1) 大于 `>`    

(2) 小于 `<` 

(3) 大于等于 `>=`

(4) 小于等于 `<=`

(5) 等于 `==`

(6) 不等于 `!=`

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt(), b = sc.nextInt();

        if (a > b) System.out.printf("%d > %d\n", a, b);
        if (a >= b) System.out.printf("%d >= %d\n", a, b);
        if (a < b) System.out.printf("%d < %d\n", a, b);
        if (a <= b) System.out.printf("%d <= %d\n", a, b);
        if (a == b) System.out.printf("%d == %d\n", a, b);
        if (a != b) System.out.printf("%d != %d\n", a, b);
    }
}
```

##### 3.`if-else`连写

输入一个0到100之间的分数，
如果大于等于85，输出A；
如果大于等于70并且小于85，输出B；
如果大于等于60并且小于70，输出C；
如果小于60，输出 D；

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int s = sc.nextInt();

        if (s >= 85) {
            System.out.println("A");
        } else if (s >= 70) {
            System.out.println("B");
        } else if (s >= 60) {
            System.out.println("C");
        } else {
            System.out.println("D");
        }
    }
}
```

练习：

1.判断闰年。闰年有两种情况：
(1) 能被100整除时，必须能被400整除；
(2) 不能被100整除时，被4整除即可。
输入一个年份，如果是闰年输出`yes`，否则输出`no`。

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int year = sc.nextInt();

        if (year % 100 == 0) {
            if (year % 400 == 0)
                System.out.println("yes");
            else
                System.out.println("no");
        } else {
            if (year % 4 == 0)
                System.out.println("yes");
            else
                System.out.println("no");
        }
    }
}
```

### 二、条件表达式

(1) 与 `&&`

(2) 或 `| |`

(3) 非 `!`

例题：输入三个数，输出三个数中的最大值。

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt(), b = sc.nextInt(), c = sc.nextInt();

        if (a >= b && a >= c)
            System.out.println(a);
        else if (b >= a && b >= c)
            System.out.println(b);
        else
            System.out.println(c);
    }
}
```

练习：用一条if语句，判断闰年。

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int year = sc.nextInt();

        if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0)
            System.out.println("yes");
        else
            System.out.println("no");
    }
}
```

### 三、switch语句

**注意：** `swtich`语句中如果不加`break`语句，则从上到下匹配到第一个`case`后，会顺次执行后面每个`case`中的语句。

例题：输入一个数，输出星期几。

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int day = sc.nextInt();
        String name;

        switch(day) {
            case 1:
                name = "Monday";
                break;
            case 2:
                name = "Tuesday";
                break;
            case 3:
                name = "Wednesday";
                break;
            case 4:
                name = "Thursday";
                break;
            case 5:
                name = "Friday";
                break;
            case 6:
                name = "Saturday";
                break;
            case 7:
                name = "Sunday";
                break;
            default:
                name = "not valid";
        }

        System.out.println(name);
    }
}
```

