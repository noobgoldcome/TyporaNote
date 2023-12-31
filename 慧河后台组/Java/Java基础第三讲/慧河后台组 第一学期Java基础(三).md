# 慧河后台组 第一学期Java基础(三)

## 第三讲：循环语句

> 学习循环语句最重要的一点：理清代码执行顺序

### 一、`while`循环

可以把`while`理解为循环版的`if`语句。`if`语句是判断一次，如果条件成立，则执行后面的语句；`while`是每次判断，如果成立，则执行循环体中的语句，否则停止。

```java
public class Main{
    public static void main(String[] agrs){
        int i = 0;
        while(i < 0){
            System.out.println(i);
            i++;
        }
    }
}
```

练习：求 1 ~ 100 中所有数的立方和

```java
public class Main{
    public static void main(String[] args){
        int i = 1, sum = 0;
        while(i <= 100){
            sum += i * i * i ;
            i++;
        }
        System.out.println(sum) ;
    }
}
```

练习：求斐波那契数列的第`n`项。`f(1) = 1, f(2) = 1, f(3) = 2, f(n) = f(n-1) + f(n-2)`。

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int a = 1, b = 1, i = 1;
        while(i<n){
            c = a + b;
            a = b;
            b = c;
            i++;
        }
        System.out.println(a);
    }
}
```

死循环：循环永久执行，无法结束。我们要避免写出死循环。

```java
public class Main{
    public static void main(String[] agrs){
        int x = 1;
        while( x == 1 ){
            System.out.println("!!");
        }
    }
}
```

### 二、`do while`循环

`do while`循环不常用。
`do while`语句与`while`语句非常相似。唯一的区别是，`do while`语句限制性循环体后检查条件。不管条件的值如何，我们都要至少执行一次循环。

```java
public class Main {
    public static void main(String[] args) {
        int x = 1;
        while (x < 1) {
            System.out.println("x!");
        }
        int y = 1;
        do {
            System.out.println("y!");
        } while (y < 1);
    }
}
```

### 三、`for`循环

基本思想：把控制循环次数的变量从循环体中剥离。

```java
for (init-statement : condition: expression) {
    statement
}
```

`init-statement`可以是声明语句、表达式、空语句，一般用来初始化循环变量；
`condition`是条件表达式，和while中的条件表达式作用一样；可以为空，空语句表示`true`；
`expression`一般负责修改循环变量，可以为空。

```java
public class Main{
    public static void main(String[] args){
        for(int i = 0; i < 10; i++ ){  //循环体中只有一条语句时，可以不加大括号
            System.out.println( i );
        }
    }
}
```

练习：求1~100中所有数的立方和。

```java
public class Main {
    public static void main(String[] args) {
        int sum = 0;
        for (int i = 1; i <= 100; i ++ )
            sum += i * i * i;
        System.out.println(sum);
    }
}
```

练习：求斐波那契数列的第`n`项。`f(1) = 1, f(2) = 1, f(3) = 2, f(n) = f(n-1) + f(n-2)。`

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        int a = 1, b = 1;
        for (int i = 1; i < n; i ++ ) {
            int c = a + b;
            a = b;
            b = c;
        }

        System.out.println(a);
    }
}
```

`init-statement`可以定义多个变量，`expression`也可以修改多个变量。

例如求 `1 * 10 + 2 * 9 + 3 * 8 + 4 * 7 + 5 * 6`：

```java
public class Main {
    public static void main(String[] args) {
        int sum = 0;
        for (int i = 1, j = 10; i < j; i ++, j -- ) {
            sum += i * j;
        }

        System.out.println(sum);
    }
}
```

### 四、跳转语句

##### 1. break

可以提前从循环中退出，一般与`if`语句搭配。
例题：判断一个大于1的数是否是质数：

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        boolean isPrime = true;
        for (int i = 2; i < n; i ++ )
            if (n % i == 0) {
                isPrime = false;
                break;
            }

        if (isPrime)
            System.out.println("yes");
        else
            System.out.println("no");
    }
}
```

##### 2. continue

可以直接跳到当前循环体的结尾。作用与`if`语句类似。
例题：求1~100中所有偶数的和。

```java
public class Main {
    public static void main(String[] args) {
        int sum = 0;

        for (int i = 1; i <= 100; i ++ ) {
            if (i % 2 == 1) continue;
            sum += i;
        }

        System.out.println(sum);
    }
}
```

### 五、多层循环

将1~100打印到一个10 * 10的矩阵中：

```java
public class Main {
    public static void main(String[] args) {
        for (int i = 0, k = 1; i < 10; i ++ ) {
            for (int j = 0; j < 10; j ++, k ++ ) {
                System.out.printf("%d ", k);
            }
            System.out.println();
        }
    }
}
```

练习：打印1~100中的所有质数

```java
public class Main {
    public static void main(String[] args) {
        for (int i = 2; i <= 100; i ++ ) {
            boolean isPrime = true;
            for (int j = 2; j < i; j ++ ) {
                if (i % j == 0) {
                    isPrime = false;
                    break;
                }
            }
            if (isPrime)
                System.out.println(i);
        }
    }
}
```

