# 慧河后台组 第一学期Java基础(七)

## 第七讲：类与接口

> 类可以将变量、函数完美地打包在一起

### 一、类与对象

类定义一种全新的数据类型，包含一组变量和函数；对象是类这种类型对应的实例。
例如在一间教室中，可以将`Student`定义成类，表示“学生”这个抽象的概念。那么每个同学就是`Student`类的一个对象（实例）。

##### 1.源文件命名规则

- 一个源文件中只能有一个`public`类。
- 一个源文件可以有多个非`public`类。
- 源文件的名称应该和`public`类的类名保持一致。
- 每个源文件中，先写`package`语句，再写`import`语句，最后定义类。

##### 2.类的定义

- public: 所有对象均可以访问
- private: 只有本类内部可以访问
- protected：同一个包或者子类中可以访问
- 不添加修饰符：在同一个包中可以访问 
- 静态（带static修饰符）成员变量/函数与普通成员变量/函数的区别：
  - 所有static成员变量/函数在类中只有一份，被所有类的对象共享；
  - 所有普通成员变量/函数在类的每个对象中都有独立的一份；
  - 静态函数中只能调用静态函数/变量；普通函数中既可以调用普通函数/变量，也可以调用静态函数/变量。

```java
class Point {
    private int x;
    private int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public void setX(int x) {
        this.x = x;
    }

    public void setY(int y) {
        this.y = y;
    }

    public int getX() {
        return x;
    }

    public int getY() {
        return y;
    }

    public String toString() {
        return String.format("(%d, %d)", x, y);
    }
}
```

##### 3.类的继承

​	每个类只能继承一个类

​	类的继承是一个抽象的概念，是将很多东西的共性抽离出来并且打包，目的是减少代码量

```java
class ColorPoint extends Point {
    private String color;

    public ColorPoint(int x, int y, String color) {
        super(x, y);
        this.color = color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public String toString() {
        return String.format("(%d, %d, %s)", super.getX(), super.getY(), this.color);
    }
}
```

##### 4.类的多态

同一种对象， 调用同一个函数，会有不同的行为 

```java
public class Main {
    public static void main(String[] args) {
        Point point = new Point(3, 4);//子类的对象是可以赋给父类的（向上转型）
        Point colorPoint = new ColorPoint(1, 2, "red");

        // 多态，同一个类的实例，调用相同的函数，运行结果不同
        System.out.println(point.toString());
        System.out.println(colorPoint.toString());
    }
}
```

### 二、接口

`interface`与`class`类似。主要用来定义类中所需包含的函数。

接口也可以继承其他接口，一个类可以实现多个接口。

##### 1.接口的定义

接口中不添加修饰符时，默认为`public`。

```java
interface Role {
    public void greet();
    public void move();
    public int getSpeed();
}
```

##### 2. 接口的继承

每个接口可以继承多个接口

```java
interface Hero extends Role {
    public void attack();
}
```

##### 3.接口的实现

每个类可以实现多个接口

```java
class Varus implements Hero {
    private final String name = "Varus";
    public void attack() {
        System.out.println(name + ": Attack!");
    }

    public void greet() {
        System.out.println(name + ": Hi!");
    }

    public void move() {
        System.out.println(name + ": Move!");
    }

    public int getSpeed() {
        return 10;
    }
}
```

##### 4.接口的多态

一个对象可以赋给本类，可以赋给父类，也可以赋给接口

```java
class Wayne implements Hero {
    private final String name = "Vayne";
    public void attack() {
        System.out.println(name + ": Attack!!!");
    }

    public void greet() {
        System.out.println(name + ": Hi!!!");
    }

    public void move() {
        System.out.println(name + ": Move!!!");
    }

    public int getSpeed() {
        return 10;
    }
}

public class Main {
    public static void main(String[] args) {
        Hero[] heros = {new Varus(), new Vayne()};
        for (Hero hero: heros) {
            hero.greet();
        }
    }
}
```

