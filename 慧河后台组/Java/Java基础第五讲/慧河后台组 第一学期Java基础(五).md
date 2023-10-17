# 慧河后台组 第一学期Java基础(五)

> 没有字符串，就很难与计算机交流😥

一、字符与整数的联系——ASCII码

每个常用字符都对应一个`-128 ~ 127`的数字，二者之间可以相互转化。注意：目前负数没有与之对应的字符。

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        char c = 'a';
        System.out.println((int)c);

        int a = 66;
        System.out.println((char)a);
    }
}
```

常用ASCII值：`'A'- 'Z'`是`65 ~ 90`，`'a' - 'z'`是`97 - 122`，`0 - 9`是 `48 - 57`。
字符可以参与运算，运算时会将其当做整数：

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int a = 'B' - 'A';
        int b = 'A' * 'B';
        char c = 'A' + 2;

        System.out.println(a);
        System.out.println(b);
        System.out.println(c);
    }
}
```

### 二、`String`类

初始化：

```java
String a = "Hello World";
String b = "My name is ";
String x = b;  // 存储到了相同地址
String c = b + "HuiHe";  // String可以通过加号拼接
String d = "My age is " + 18;  // int会被隐式转化成字符串"18"
String str = String.format("My age is %d", 18);  // 格式化字符串，类似于C++中的sprintf
String money_str = "123.45";
double money = Double.parseDouble(money_str);  // String转double
//整形转换字符串
int m = 123;
String m_str = "" + m;
或者
Integer mm = 123;
String mm_str = mm.toString();
```

String是只读变量，不能修改，例如：

```java
String a = "Hello ";
a += "World";  // 会构造一个新的字符串
```

访问`String`中的字符：

```java
String str = "Hello World";
for (int i = 0; i < str.length(); i ++ ) {
    System.out.print(str.charAt(i));  // 只能读取，不能写入
}
```

常用API：

- `length()`: 返回长度

  ```java
  public class Main {
      public static void main(String[] args) {
         String str = "Hello world";
         for(int i = 0; i < str.length(); i++){
             System.out.println(str.charAt(i));
         }
      }
  }
  ```

  

- `split(String regex)`：分割字符串

  ```java
  import java.util.Arrays;
  public class Main {
      public static void main(String[] args) {
         String str = "Hello Hui He";
         String[] strs = str.split(" ");
         System.out.println(Arrays.toString(strs));
      }
  }
  ```

  

- `indexOf(char c)`、`indexOf(String str)`、`lastIndexOf(char c)`、`lastIndexOf(String str)`：查找，找不到返回-1

  ```java
  public class Main {
      public static void main(String[] args) {
         String str = "Hello Huihe";
         System.out.println(str.indexOf('l'));
         System.out.println(str.indexOf("ui"));
         System.out.println(str.indexOf("haha"));
         System.out.println(str.lastIndexOf('l'));
         System.out.println(str.lastIndexOf("lo"));
      }
  }
  ```

- `equals()`：判断两个字符串是否相等，注意不能直接用==

  ```java
  public class Main {
      public static void main(String[] args) {
         String str = "Hello Hui He";
         if("Hello Hui He".equals(str)){
             System.out.println("YESSS!");
         }
      }
  }
  ```

- `compareTo()`：判断两个字符串的字典序大小，负数表示小于，0表示相等，正数表示大于

  ```java
  public class Main {
      public static void main(String[] args) {
         String str = "Hello Huihe";
         System.out.println(str.compareTo("Hello Huihe"));
         System.out.println(str.compareTo("hello Huihe"));
         System.out.println(str.compareTo("Aello Huihe"));
      }
  }
  ```

- `startsWith()`：判断是否以某个前缀开头

- `endsWith()`：判断是否以某个后缀结尾

  ```java
  public class Main {
      public static void main(String[] args) {
         String str = "Hello Huihe";
         System.out.println(str.startsWith("Hel"));
         System.out.println(str.endsWith("ihe"));
      }
  }
  ```

- `trim()`：去掉首尾的空白字符

  ```java
  public class Main {
      public static void main(String[] args) {
         String str = "   Hello Huihe   ";
         System.out.println(str.trim());
      }
  }
  ```

- `toLowerCase()`：全部用小写字符

- `toUpperCase()`：全部用大写字符

  ```java
  public class Main {
      public static void main(String[] args) {
         String str = "   Hello Huihe   ";
         System.out.println(str.trim());
         System.out.println(str.toLowerCase());
         System.out.println(str.toUpperCase());
      }
  }
  ```

- `replace(char oldChar, char newChar)`：替换字符

- `replace(String oldRegex, String newRegex)`：替换字符串

  ```java
  public class Main {
      public static void main(String[] args) {
         String str = "Hello Huihe";
         System.out.println(str.replace('l', 'a'));
         System.out.println(str.replace("ll", "aaaaa"));
      }
  }
  ```

- `substring(int beginIndex, int endIndex)`：返回[beginIndex, endIndex)中的子串

  ```java
  public class Main {
      public static void main(String[] args) {
         String str = "Hello Huihe";
         System.out.println(str.substring(1,3));
  	   System.out.println(str.substring(1));
      }
  }
  ```

- `toCharArray()`：将字符串转化成字符数组

  ```java
  import java.util.Arrays;
  public class Main {
      public static void main(String[] args) {
         String str = "Hello Huihe";
         char[] cs = str.toCharArray();
         System.out.println(Arrays.toString(cs));
      }
  }
  ```

**以上所有API均不会改变原串内容**

### 三、输入与输出

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String str1 = sc.next();  // 输入字符串，遇到空格、回车等空白字符时停止输入
        String str2 = sc.nextLine();  // 输入一整行字符串，遇到空格不会停止输入，遇到回车才会停止

        System.out.println(str1);  // 可以直接输出
        System.out.printf("%s\n", str2);  // 也可以格式化输出，用 %s 表示字符串
    }
}
```

### 四、`StringBuilder`、`StringBuffer`	

`String`不能被修改，如果打算修改字符串（若平时做题时，需要插入一个字符十万次，每次需要复制1，2，3，... ，1e5 约等于1e10次，非常的慢，所以介绍下面两个格外的工具），可以使用`StringBuilder`和`StringBuffer`。

`StringBuffer`线程安全，速度较慢（写多线程要用这个）；`StringBuilder`线程不安全，速度较快。（算法题较多，不支持多线程，限制少）

```java
StringBuilder sb = new StringBuilder("Hello ");  // 初始化
sb.append("World");  // 拼接字符串
System.out.println(sb);

for (int i = 0; i < sb.length(); i ++ ) {
    sb.setCharAt(i, (char)(sb.charAt(i) + 1));  // 读取和写入字符
}

System.out.println(sb);
```

常用API：

- `reverse()`：翻转字符串		