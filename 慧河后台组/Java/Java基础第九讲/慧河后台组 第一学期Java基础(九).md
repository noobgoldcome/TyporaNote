# 慧河后台组 第一学期Java基础(九)

## 第九讲：异常处理

> 异常处理可以让我们在程序运行的时候进行判断与补救。

### 一、Error与Exception的区别

Error是程序无法处理的错误，比如OutOfMemoryError、ThreadDeath等。这些异常发生时，Java虚拟机(JVM)一般会选择线程终止。此类异常是程序的致命异常，是无法捕获处理的。

Exception是程序本身可以处理的异常，（遇到了问题可以去补救）这种异常分两大类：运行时异常和非运行时异常。 程序中应当尽可能去处理这些异常。

### 二、Exception类的继承关系

![image-20221203134110897](assets\image-20221203134110897.png)

主要关注`Exception`，RuntimeException和其他类处理不一样，这一类的异常处理起来要求不是那么严格，其他类异常需要捕获或者抛出去，运行时异常没有这个问题，管得比较松。

### 三、运行时异常和非运行时异常的区别

运行时异常都是RuntimeException类及其子类异常，如NullPointerException、IndexOutOfBoundsException等， 这些异常是`非检查型异常`，程序中可以选择捕获处理，也可以不处理。这些异常一般是由程序逻辑错误引起的，程序应该从逻辑角度尽可能避免这类异常的发生。

非运行时异常是RuntimeException以外的异常，类型上都属于Exception类及其子类。从程序语法角度讲是必须进行处理的异常，如果不处理，程序就不能编译通过。如IOException、SQLException等以及用户自定义的Exception异常，这些是`检查型异常`。一般情况下不自定义检查型异常。

### 四、内置异常类

##### 非检查性异常

| 异常                            | 描述                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| ArithmeticException             | 当出现异常的运算条件时，抛出此异常。例如，一个整数”除以零”时，抛出此类的一个实例。 |
| ArrayIndexOutOfBoundsException  | 用非法索引访问数组时抛出的异常。如果索引为负或大于等于数组大小，则该索引为非法索引。 |
| ArrayStoreException             | 试图将错误类型的对象存储到一个对象数组时抛出的异常。         |
| ClassCastException              | 当试图将对象强制转换为不是实例的子类时，抛出该异常。         |
| IllegalArgumentException        | 抛出的异常表明向方法传递了一个不合法或不正确的参数。         |
| IllegalMonitorStateException    | 抛出的异常表明某一线程已经试图等待对象的监视器，或者试图通知其他正在等待对象的监视器而本身没有指定监视器的线程。 |
| IllegalStateException           | 在非法或不适当的时间调用方法时产生的信号。换句话说，即 Java 环境或 Java 应用程序没有处于请求操作所要求的适当状态下。 |
| IllegalThreadStateException     | 线程没有处于请求操作所要求的适当状态时抛出的异常。           |
| IndexOutOfBoundsException       | 指示某排序索引（例如对数组、字符串或向量的排序）超出范围时抛出。 |
| NegativeArraySizeException      | 如果应用程序试图创建大小为负的数组，则抛出该异常。           |
| NullPointerException            | 当应用程序试图在需要对象的地方使用 null 时，抛出该异常。     |
| NumberFormatException           | 当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时，抛出该异常。 |
| SecurityException               | 由安全管理器抛出的异常，指示存在安全侵犯。                   |
| StringIndexOutOfBoundsException | 此异常由 String 方法抛出，指示索引或者为负，或者超出字符串的大小。 |
| UnsupportedOperationException   | 当不支持请求的操作时，抛出该异常。                           |

##### 检查性异常

| 异常                       | 描述                                                         |
| -------------------------- | ------------------------------------------------------------ |
| ClassNotFoundException     | 应用程序试图加载类时，找不到相应的类，抛出该异常。           |
| CloneNotSupportedException | 当调用 Object 类中的 clone 方法克隆对象，但该对象的类无法实现 Cloneable 接口时，抛出该异常。 |
| IllegalAccessException     | 拒绝访问一个类的时候，抛出该异常。                           |
| InstantiationException     | 当试图使用 Class 类中的 newInstance 方法创建一个类的实例，而指定的类对象因为是一个接口或是一个抽象类而无法实例化时，抛出该异常。 |
| InterruptedException       | 一个线程被另一个线程中断，抛出该异常。                       |
| NoSuchFieldException       | 请求的变量不存在                                             |
| NoSuchMethodException      | 请求的方法不存在                                             |

### 五、内置异常方法

| 方法                                        | 说明                                                         |
| ------------------------------------------- | ------------------------------------------------------------ |
| public String getMessage()                  | 返回关于发生的异常的详细信息。这个消息在Throwable 类的构造函数中初始化了。 |
| public Throwable getCause()                 | 返回一个 Throwable 对象代表异常原因。                        |
| public String toString()                    | 返回此 Throwable 的简短描述。                                |
| public void printStackTrace()               | 将此 Throwable 及其回溯打印到标准错误流                      |
| public StackTraceElement [] getStackTrace() | 返回一个包含堆栈层次的数组。下标为0的元素代表栈顶，最后一个元素代表方法调用堆栈的栈底。 |
| public Throwable fillInStackTrace()         | 用当前的调用栈层次填充Throwable 对象栈层次，添加到栈层次任何先前信息中。 |

### 六、捕获异常

```java
package org.hjl;


import java.util.*;

public class Main {
    private static void foo(){
        int [] array = new int[5];
        for(int i = 0; i < 5; i++){
            array[i] = i;
        }
        Scanner sc = new Scanner(System.in);
        int k = sc.nextInt();
        int x = sc.nextInt();
        try{
            array[k] /= x;
        }catch (ArithmeticException e){
            System.out.println("除以0啦");
        }catch (IndexOutOfBoundsException e){
            System.out.println("下标越界啦！");
        }finally {
            for (int i = 0; i < 5; i++){
                System.out.printf("array[%d] = %d\n", i, array[i]);
            }
        }
    }
    public static void main(String[] args) {
        foo();
    }
}

//		try{
//           array[k] /= x;
//        }catch (ArithmeticException | IndexOutOfBoundsException e){
//            e.printStackTrace();
//        }
```

### 七、抛出异常

throw: 在函数内抛出一个异常。
throws：在函数定义时抛出一些可能的异常。

检查型异常必须被捕获或者抛出。

```java
package org.hjl;


import java.io.IOException;
import java.nio.file.NoSuchFileException;
import java.util.*;

public class Main {
    private static void foo() throws IOException, NoSuchFieldException {
        Scanner sc = new Scanner(System.in);
        int x = sc.nextInt();
        if(x == 1){
            throw new IOException("找不到文件！");
        }else{
            throw new NoSuchFieldException("无方法异常！");
        }
    }

    public static void main(String[] args)  {
        try {
            foo();
        } catch (IOException | NoSuchFieldException e) {
            System.out.println(e.getMessage());
        }
        System.out.println("HAha");
    }
}

```

