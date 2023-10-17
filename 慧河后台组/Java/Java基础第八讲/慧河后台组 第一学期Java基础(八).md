# 慧河后台组 第一学期Java基础(八)

## 第八讲：常用容器

### 一、List

接口：`java.util.List<>`。

实现：

- `java.util.ArrayList<>`：变长数组
- `java.util.LinkedList<>`：双链表

函数：

- `add()`：在末尾添加一个元素
- `clear()`：清空
- `size()`：返回长度
- `isEmpty()`：是否为空
- `get(i)`：获取第`i`个元素
- `set(i, val)`：将第`i`个元素设置为`val`

```java
//List(链表) 是一个接口 接口是用类来实现的
//数组支持随机访问 时间复杂度为O(1)， 链表访问需要线性寻址，时间复杂度为O(n);
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<Integer> list = new LinkedList<>();
        list.add(1);
        list.add(2);
        list.add(10);
        for(int i = 0; i < list.size(); i++){
            System.out.println(list.get(i));
        }
        for (int i = 0; i < list.size(); i++){
            list.set(i, list.get(i) + 1);
        }
        System.out.println(list);
    }
}
```

### 二、栈

类：`java.util.Stack<>`

函数：

- `push()`：压入元素
- `pop()`：弹出栈顶元素，并返回栈顶元素
- `peek()`：返回栈顶元素
- `size()`：返回长度
- `empty()`：栈是否为空
- `clear()`：清空

```java
//我们讲的其他所有容器都是接口，只有栈 是只有实现没有接口 其实也就是一个类
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Stack<Integer> stk = new Stack<>();
        stk.push(1);
        stk.push(2);
        stk.push(10);
        System.out.println(stk.pop());
        System.out.println(stk.peek());
    }
}
```

### 三、队列

接口：`java.util.Queue<>`

实现：

- `java.util.LinkedList<>`：双链表
- `java.util.PriorityQueue<>`：优先队列（堆）//与C++不同 C++默认大根堆
  默认是小根堆，大根堆写法：`new PriorityQueue<>(Collections.reverseOrder())`

函数：

- `add()`：在队尾添加元素
- `remove()`：删除并返回队头
- `isEmpty()`：是否为空
- `size()`：返回长度
- `peek()`：返回队头
- `clear()`：清空

```java
//栈是一个类， 队列是一个接口
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();//普通队列一定要定义成LinkedList， 定义ArrayList会报错
        q.add(1);
        q.add(2);
        q.add(10);
        System.out.println(q.remove());
        System.out.println(q.peek());
        
    }
}

import java.util.*;

public class Main {
    public static void main(String[] args) {
        Queue<Integer> q = new PriorityQueue<>(Collections.reverseOrder());
        q.add(2);
        q.add(1);
        q.add(10);
        while (q.size() > 0){
            System.out.println(q.remove());
        }
    }
}
```

### 四、Set

接口：`java.util.Set<K>`

实现：

- `java.util.HashSet<K>`：哈希表
- `java.util.TreeSet<K>`：平衡树

函数：

- `add()`：添加元素
- `contains()`：是否包含某个元素
- `remove()`：删除元素
- `size()`：返回元素数
- `isEmpty()`：是否为空
- `clear()`：清空

`java.util.TreeSet`多的函数：

- `ceiling(key)`：返回大于等于`key`的最小元素，不存在则返回`null`
- `floor(key)`：返回小于等于`key`的最大元素，不存在则返回`null`

```java
//哈希表是用来判断一棵树是否存在，平衡树是用来维护一个动态的有序序列，这样就可以二分了（就可以找到大于等于某个数的最小数，以及小于等于某个数的最大数
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Set<Integer> set = new HashSet<>();//哈希表是无序的 不一定是有序的（有序只是意外 增删改查O(1))；
        set.add(1);
        set.add(2);
        set.add(10);
        set.remove(2);
        System.out.println(set.contains(2));
        System.out.println(set.contains(5));
        for(int x: set)
            System.out.println(x);
    }
} 

import java.util.*;

public class Main {
    public static void main(String[] args) {
        TreeSet<Integer> set = new TreeSet<>();//TreeSet是有序的，使用平衡树维护的，维护的性质强一些，那么运行效率也就低一些
        //TreeSet的插入，查找，删除都是（log（n）级别的）
        set.add(111);
        set.add(222);
        set.add(50);
        System.out.println(set.ceiling(100));//注意 要使用ceiling就得用TreeSet初始化
        System.out.println(set.floor(100));
    }
}
```

### 五、Map

接口：`java.util.Map<K, V>`

实现：

- `java.util.HashMap<K, V>`：哈希表
- `java.util.TreeMap<K, V>`：平衡树

函数：

- `put(key, value)`：添加关键字和其对应的值

- `get(key)`：返回关键字对应的值

- `containsKey(key)`：是否包含关键字

- `remove(key)`：删除关键字

- `size()`：返回元素数

- `isEmpty()`：是否为空

- `clear()`：清空

- `entrySet()`：获取Map中的所有对象的集合

- `Map.Entry<K, V>`：Map中的对象类型
- `getKey()`：获取关键字
  
- `getValue()`：获取值

`java.util.TreeMap<K, V>`多的函数：

- `ceilingEntry(key)`：返回大于等于key的最小元素，不存在则返回null
- `floorEntry(key)`：返回小于等于key的最大元素，不存在则返回null

```java
//Set 是维护一个集合， Map是维护一个映射， 它可以将一个元素映射到另一个元素
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("123", 2);
        map.put("321", 3);
        map.put("21", 10);
        map.remove("123");
        System.out.println(map.get("123"));
        System.out.println(map.containsKey("1234"));

        for(Map.Entry<String, Integer> entry: map.entrySet())
            System.out.printf("%s %d\n", entry.getKey(), entry.getValue());
        
    }
}

import java.util.*;

public class Main {
    public static void main(String[] args) {
        TreeMap<Integer, Integer> map = new TreeMap<>();//想用二分必须用TreeMap初始化
        map.put(123, 2);
        map.put(321, 3);
        map.put(21, 10);

//        for(Map.Entry<Integer, Integer> entry: map.entrySet())
//            System.out.printf("%d %d\n", entry.getKey(), entry.getValue());
        Map.Entry<Integer, Integer> up = map.ceilingEntry(123);//大于等于123的数
        System.out.println(up);
        Map.Entry<Integer, Integer> down = map.ceilingEntry(20);//大于等于123的数
        System.out.println(down);
    }
}

```

