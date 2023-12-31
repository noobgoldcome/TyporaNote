# 慧河后台组 第一学期Java基础(六)

## 第六讲：函数

> 理解函数，最重要的就是理解函数执行的程序

### 一、函数基础

一个典型的函数定义包括以下部分：修饰符、返回类型、函数名字、由0个或多个形参组成的列表以及函数体。

##### 1.1编写函数

我们来编写一个求阶乘的程序。程序如下所示：

```java
public class Main {
    private static int fact(int val) {
        int res = 1;
        for (int i = 1; i <= val; i ++ )
            res *= i;
        return res;
    }
}
```

函数名字是`fact`，它作用于一个整型参数，返回一个整型值。`return`语句负责结束`fact`并返回`res`的值。

修饰符包括`private`、`static`等，它们属于`类`相关的概念，会在下一章解释。

##### 1.2调用函数

```java
public class Main {
    private static int fact(int val) {
        int res = 1;
        for (int i = 1; i <= val; i ++ )
            res *= i;
        return res;
    }

    public static void main(String[] args) {
        int res = fact(5);
        System.out.printf("5! is %d\n", res);
    }
}
```

函数的调用完成两项工作：一是用实参初始化函数对应的形参，二是将控制权转移给被调用函数。此时，主调函数的执行被暂时中断，被调函数开始执行。

##### 1.3 形参和实参

实参是形参的初始值。第一个实参初始化第一个形参，第二个实参初始化第二个形参，依次类推。形参和实参的类型和个数必须匹配。

```java
fact("hello");      // 错误：实参类型不正确
fact();             // 错误：实参数量不足
fact(42, 10, 0);    // 错误：实参数量过多
fact(' ');      // 正确：该实参能自动转换成int类型，' '的ASCII值为32，所以该操作等价于fact(32);
```

##### 1.4 函数的形参列表

函数的形参列表可以为空，但是不能省略。

```java
void f1() {/* …. */}            // 空形参列表
```

形参列表中的形参通常用逗号隔开，其中每个形参都是含有一个声明符的声明。即使两个形参的类型一样，也必须把两个类型都写出来：

```java
int f3(int v1, v2) {/* … */}        // 错误
int f4(int v1, int v2) {/* … */}    // 正确
```

##### 1.5 函数返回类型

大多数类型都能用作函数的返回类型。一种特殊的返回类型是`void`，它表示函数不返回任何值。
函数的返回类型也可以是数组、字符串或者其他对象：

```java
import java.util.Arrays;

public class Main {
    private static int[] newArray() {
        int[] a = {1, 2, 3};
        return a;
    }

    private static String newString() {
        return "Hello HuiHe";
    }

    public static void main(String[] args) {
        System.out.println(Arrays.toString(newArray()));
        System.out.println(newString());
    }
}
```

##### 1.6 变量的作用域

本章中我们只使用静态成员变量和静态成员函数，非静态成员变量/函数及其区别会在下一章中介绍。

函数内定义的变量为局部变量，只能在函数内部使用。
定义在类中的变量为成员变量，可以在类的所有成员函数中调用。
当局部变量与全局变量重名时，会优先使用局部变量。

```java
public class Main{
    private static int x = 4;
    private static void f1() {
        int x = 3;
        System.out.println(x);
    }
    private static void f2(){
        System.out.println(x);
    }
    private static void f3(){
        System.out.println(x + 1);
    }
    
    public static void main(String[] args){
        f1();
        f2();
        f3();
    }
}
```

### 二、参数传递

##### 2.1 值传递

八大基本数据类型和`String`类型等采用值传递。

将实参的初始值拷贝给形参。此时，对形参的改动不会影响实参的初始值。

```java
public class Main {
    private static void f(int x) {
        x = 5;
    }

    public static void main(String[] args) {
        int x = 10;
        f(x);
        System.out.println(x);
    }
}
```

##### 2.2 引用传递

除`String`以外的数据类型的对象，例如数组、`StringBuilder`等采用引用传递。

将实参的引用（地址）传给形参，通过引用找到变量的真正地址，然后对地址中的值修改。所以此时对形参的修改会影响实参的初始值。

```java
import java.util.Arrays;

public class Main {
    private static void f1(int[] a) {
        for (int i = 0, j = a.length - 1; i < j; i ++, j -- ) {
            int t = a[i];
            a[i] = a[j];
            a[j] = t;
        }
    }

    private static void f2(StringBuilder sb) {
        sb.append("Hello World");
    }

    public static void main(String[] args) {
        int[] a = {1, 2, 3, 4, 5};
        f1(a);
        System.out.println(Arrays.toString(a));

        StringBuilder sb = new StringBuilder("");
        f2(sb);
        System.out.println(sb);
    }
}
```

### 三、返回类型和return语句

`return`语句终止当前正在执行的函数并将控制权返回到调用该函数的地方。return语句有两种形式 :

```java
return;
return expression;
```

##### 3.1 无返回值函数

没有返回值的`return`语句只能用在返回类型是`void`的函数中。返回`void`的函数不要求非得有`return`语句，因为在这类函数的最后一句后面会隐式地执行`return`。

通常情况下，`void`函数如果想在它的中间位置提前退出，可以使用`return`语句。`return`的这种用法有点类似于我们用`break`语句退出循环。

```java
public class Main {
    private static void swap(int[] a) {  // 交换a[0]和a[1]
        // 如果两个值相等，则不需要交换，直接退出
        if (a[0] == a[1])
            return;
        // 如果程序执行到了这里，说明还需要继续完成某些功能

        int tmp = a[0];
        a[0] = a[1];
        a[1] = tmp;
        // 此处无须显示的return语句
    }

    public static void main(String[] args) {
        int[] a = {3, 4};
        swap(a);
        System.out.printf("%d %d\n", a[0], a[1]);
    }
}
```

##### 3.2 有返回值的函数

只要函数的返回类型不是`void`，则该函数内的每个分支都必须有`return`语句，且每条`return`语句都必须返回一个值。`return`语句返回值的类型必须与函数的返回类型相同，或者能隐式地转换函数的返回类型。

```java
import java.util.Scanner;

public class Main {
    private static int max(int a, int b) {
        if (a > b)
            return a;
        return b;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int x = sc.nextInt(), y = sc.nextInt();

        System.out.println(max(x, y));
    }
}
```

### 四、函数重载

函数重载是指：在同一个类中存在多个函数，函数名称相同但参数列表不同。

编译器会根据实参的类型选择最匹配的函数来执行。

```java
import java.util.Scanner;

public class Main {
    private static int max(int a, int b) {
        System.out.println("int max");
        if (a > b) return a;
        return b;
    }

    private static double max(double a, double b) {
        System.out.println("double max");
        if (a > b) return a;
        return b;
    }

    public static void main(String[] args) {
        System.out.println(max(3, 4));
        System.out.println(max(3.0, 4.0));
    }
}
```

### 五、函数递归

在一个函数内部，也可以调用函数本身。

```java
import java.util.Scanner;

public class Main {
    private static int fib(int n) {  // 求斐波那切数列第n项
        if (n <= 2) return 1;
        return fib(n - 1) + fib(n - 2);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        System.out.println(fib(n));
    }
}
```

