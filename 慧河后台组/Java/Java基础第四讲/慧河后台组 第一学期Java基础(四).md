# 慧河后台组 第一学期Java基础(四)

## 第四讲：数组

> 数组是存储数据的强而有力的手段。

### 一、一维数组

##### 1.1 数组的定义

数组的定义方式和变量类似。

```java
public class Main{
    public static void main(String[] args){
        int[] a = new int[10], b;
        float[] f = new float [23];
        double[] d = new double[128];
        char[] c = new char[21];
        //不一定是基本变量才有数组
        String[] strs = new String[10]; 
    }
}
// 定义完之后， 数组a为十个int类型的 0 ； f 为23个值为0的float变量....
//与C / C++ 不同(局部变量定义完是随机变量)  java里面定义后都是0
// String数组里面全是 null
//b也是数组 只不过是空数组 长度为0
//char数组默认初始化也是值为0的字符 ASCII码也是有0值的 代表的是'\0'  就是空 什么都没有 注意不是空格！！;
//数组定义的理解： 可以把int[] 整体看成一个类型，后面定义的全是整型数组； 与C++/C 不同 int a[]；
```

##### 1.2 数组的初始化

```java
public class Main{
    public static void main(String[] args){
        int[] a = {0, 1, 2}; //含有三个元素，元素分别为0， 1， 2；
        int[] b = new int[3]; //含有三个元素，元素的值均为0 （默认初始化）
        char[] d = { 'a', 'b', 'c' }; //字符数组的初始化
    }
}
```

##### 1.3 访问数组元素

通过下标访问数组。

```java
public class Main{
    public static void main(String[] args){
        int a = {0 ,1 ,2};
        System.out.printf("%d %d %d\n", a[0], a[1], a[2]);
        a[0] = 5;
        System.out.printf("%d %d %d\n", a[0], a[1], a[2]);
    }
}
```

练习题1： 使用数组实现求斐波那契数列的第 **N** 项。

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
		Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] f = new int[n+1]; //注意 java可以使用变量定义数组长度 C++/C 最好用常量定义数组！！
        f[0] = 1;
        f[1] = 1;
        for(int i = 2; i<=n; i++){
            f[i] = f[i-1] + f[i-2];
        }
        System.out.println(f[n]);
    }
}
```

练习题2：输入一个 **n**，再输入 **n** 个整数。将这 **n** 个整数逆序输出。

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int a[] = new int[n];
        for(int i = 0; i<n; i++){
            a[i] = sc.nextInt();
        }
        for(int i = n -1; i >=0; i++ ){
            System.out.printf("%d ", a[i]);
        }
    }
}
```

练习题3：输入 **n** 个数，将这 **n** 个数按从小到大的顺序输出。

```java
import java.util.Scanner; //选择排序
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] a = new int[n];
        for(int i = 0; i < n ; i++){
            a[i] = sc.nextInt();
        }
        for(int i = 0; i<n; i++){
            for(int j = i + 1; j <n; j++){
                if(a[j] < a[i]){
                    int t = a[i];
                    a[i] = a[j];
                    a[j] = t;
                }
            }
        }
        
        for(int i = 0; i<n; i++) 
            System.out.printf("%d ", a[i]);
    }
}
```

### 二、多维数组

多维数组就是数组的数组。

```java
public class Main {
    public static void main(String[] args) {
        int[][] a = new int[3][4]; // 大小为3的数组，每个元素是含有4个整数的数组。
        int[][][] b = new int[10][20][30]; // 将所有元素的初值为0
        // 大小为10的数组，它的每个元素是含有20个数组的数组
        // 这些数组的元素是含有30个整数的数组
    }
}
```

```java
public class Main{
    public static void main(String[] args){
        int[][] a = {
            {0, 1, 2, 3},
            {4, 5, 6, 7},
            {8, 9, 10, 11},//最后一个逗号可有可无都可以通过编译
        }
        
        for(int i = 0; i<4; i++)
            a[0][i] = 0;
        for(int i = 0; i < 3; i++){
             for(int j = 0; j < 4; j++)
                System.out.printf("%d ",a[i][j]);
            System.out.println();
        }       
        	
    }
}
```

### 三、数组的范围遍历（foreach）

> foreach 语句用于循环访问集合以获取所需信息，但不应用于更改集合内容以避免产生不可预知的副作用。 **因此不要对foreach的循环变量赋值。**

```java
public class Main{
    public static void main(String[] args){
        int[][] a = {
            {0, 1, 2, 3},
            {4, 5, 6, 7},
            {8, 9, 10, 11},
        };
        for(int[] row : a)
            for(int x : row)
                System.out.printf("%d ", x);
        	System.out.println();
    }
}
```



### 四、常用API

- 属性`length`: 返回数组长度，注意不加小括号

  ```java
  public class Main{
      public static void main(String[] args){
          int[][] a = {
              {0, 1, 2, 3},
              {4, 5, 6},
              {8, 9, 10, 11},//最后一个逗号可有可无都可以通过编译
          }
          System.out.println(a.length);
        	for(int i = 0; i < 3; i++)
              System.out.println(a[i].length);
      }
  }
  ```

- `Arrays.sort()` : 数组排序

- `Arrays.toString()`：将数组转化为字符串

  ```java
  import java.util.Scanner;
  import java.util.Arrays;
  public class Main{
      public static void main(String[] args){
          Scanner sc = new Scanner(System.in);
          int n = sc.nextInt();
          int[] q = new int[n];
          for(int i = 0; i < n; i++){
              q[i] = sc.nextInt();
          }
          Arrays.sort(q);
          System.out.println(Arrays.toString(q));//[1,2,3,4,5]
      }
  }
  ```

  ```java
  //（拓展内容）若想降序
  // 1. 变量类型不能是基本变量 而应该是对象（以后会讲什么是对象）int 的对象是Integer
  // 2. sort方法里面要加入一个比较函数
  import java.util.Scanner;
  import java.util.Arrays;
  public class Main{
      public static void main(String[] args){
          Scanner sc = new Scanner(System.in);
          int n = sc.nextInt();
          Integer[] q = new Integer[n];
          for(Integer i = 0; i < n; i++){
              q[i] = sc.nextInt();
          }//接下来加入比较函数 比较函数传入两个值 x和y 后面写一个 -> 意思是实现了一个匿名函数 
          //这个函数的返回值如果是负数 意味着x要排在y的前面，正数意味x排在y的后面
          Arrays.sort(q, (x, y)->{
              return x - y;
          });
          System.out.println(Arrays.toString(q));//[1,2,3,4,5]
      }
  }
  ```

- `Arrays.deepToString()`：将多维数组转化为字符串

  ```java
  //(拓展内容) 若想要排序多维数组
  import java.util.Scanner;
  import java.util.Arrays;
  public class Main{
      public static void main(String[] args){
         	int[][] a = {
              {4, 5, 6, 7},
              {0, 1, 2, 3},
              {8, 9, 10, 11}
          };
          Arrays.sort(a,(x,y)->{
              return x[0] - y[0];
          });
         //System.out.println(Arrays.toString(a));
          System.out.println(Arrays.deepToString(a));
      }
  }
  ```

- `Arrays.fill(int[] a, int val)`：填充数组

  ```java
  import java.util.Arrays;
  public class Main{
      public static void main(String[] args){
  		int[] a = new int[10];
          Arrays.fill(a,-1);
          System.out.println(Arrays.toString(a));//fill方法只能初始化一维数组 不能初始化二维数组
      }
  }
  ```

- 使用`Arrays`需要`import java.util.Arrays`;

