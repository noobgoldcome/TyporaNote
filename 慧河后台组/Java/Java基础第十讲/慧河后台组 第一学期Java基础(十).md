# 慧河后台组 第一学期Java基础(十)

## 第十讲：注解，多线程

### 一、注解

1. 注解（Annotation）也被称为元数据（Metadata），用于修饰包、方法、属性、构造器、局部变量等数据信息。
2. 注解不影响**程序逻辑**，但注解可以被编译或运行。
3. 在JavaSE中，注解的使用目的比较简单，例如标记过时的功能，忽略警告等。在JavaEE中注解占据了更重要的角色，例如用来配置应用程序的任何切面，代替JavaEE旧版中所遗留的繁冗代码和XML配置等。

##### （一）、常用注解

1. @Override: 限定某个函数必须重写其他函数，该注解只能用于函数
2. @Deprecated：用于表示某个程序元素（类、函数）已过时
3. @SuppressWarnings：抑制编译器警告

##### （二）、元注解

修饰其他注解的注解，就被称为元注解。

1. Retention：指定注解的作用范围
2. Target：指定注解可以用在哪些地方
3. Document：注定注解是否出出现在javadoc中
4. Inherited：子类会继承父类的注解

### 二、多线程

##### （一）实现多线程

写法一：继承Thread类

```java
class Worker extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 10; i ++ ) {
            System.out.println("Hello! " + this.getName());
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Worker worker1 = new Worker();
        Worker worker2 = new Worker();
        worker1.setName("thread-1");
        worker2.setName("thread-2");
        worker1.start();
        worker2.start();
    }
}
```

写法二：实现Runnable接口

```java
class Worker1 implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 10; i ++ ) {
            System.out.println("Hello! " + "thread-1");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
        }
    }
}

class Worker2 implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 10; i ++ ) {
            System.out.println("Hello! " + "thread-2");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        new Thread(new Worker1()).start();
        new Thread(new Worker2()).start();
    }
}
```

##### （二）常用API

1. start()：开启一个线程
2. Thread.sleep(): 休眠一个线程
3. join()：等待线程执行结束

