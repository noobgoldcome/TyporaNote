# Linux

## 第一节：常用文件管理命令

### Linux的文件系统

> 根目录： /
>
> > bin目录：(常用可执行文件命令)
> >
> > etc目录：(配置文件)
> >
> > var目录：(日志log)
> >
> > lib目录：(安装包、库文件)
> >
> > home目录：(所有用户的家目录)
> >
> > ......

在Linux中如何描述路径

- 绝对路径 ls /home/acs/main.cpp 开头一定是斜杠
- 相对路径 ls tmp/main.cpp 开头一定不是斜杠
  .表示当前目录, ..表示上层目录, ~/表示家目录;

### Linux常用文件管理命令

- Ctrl + C 取消命令并且换行

- Ctrl + U 立即清空当前行

- tab 补全命令 / 文件 / 路径;(按两次会先显示出所以满足前缀要求的选项, trie树实现)

- pwd: 显示当前位置;

- cd: (change directory) cd + 路径;(默认返回家目录, cd .. 返回上一层目录, cd - 返回上一个待过的目录)

- ls: 展示当前文件夹; (ll 等价于ls -la)

  > 参数：
  >
  > -l : 展示详细信息;
  > -h : 人性化的显示详细信息;
  > -a : 显示所有的文件(包括被隐藏的文件, 所有被隐藏的文件都是以.开头的);
  > cp: cp 路径1 路径2; (将路径1内容复制一份放路径2里面, 复制 + 粘贴 + 重命名);
  > touch: 创建一个文件;
  > mkdir: 创建文件夹;(可以加-p创建一系列的文件夹)
  > history: 显示历史用过的指令;
  > rm: 删除, rm xxx: 删除某一文件;rm xxx -r: 删除某文件夹;(支持正则表达式)
  > mv: mv xxx yyy (剪切+ 粘贴)
  > cat: cat xxx(查看xxx文件);

## 第二节：tmux和vim

**简单介绍tmux和vim**

> 开发项目时的两个编辑环境，此为开发项目时所必备

### tmux

#### 作用：

> 1.分屏：可以在一个开发框里分屏
>
> 2.允许terminal在断开连接之后可以继续运行，让进程不会因为断开连接而中断。

#### 结构：

> 一个tmux可以有一堆session（会话）
> 每个sesion可开很多的window（窗口）
> 每个window可以开很多pane（小窗口）	
> 每个pane可以打开一个shell交互
> 如图所示：
>
> ![image-20230404175650588](assets\image-20230404175650588.png)

#### 常规操作：

**前言：tmux创建一个session，session中包含一个window**、

> 1).切分：
> 竖直切分：先按`ctrl+A`松开，输入`%`，也就是按下`shift+5`
> 当按下`ctrl+d`，可以关闭tmux
> 水平切分：先按`ctrl+A`，再按`”`,即 `shift+'`
> 同样的按下`ctrl+d`取消
> 对于切分来说，每一块都可以继续切分
>
> 2).退出：
> `ctrl+d` 退出
> 当window没有pane时，自动退出
> 当session没有window时，自动退出
> 故一直`ctrl+d`下去会直接退出
>
> 3).选择pane：鼠标点击即可或输入`ctrl+a`，然后按方向键选择相邻的pane
>
> 4).调整分割线：选中并拖动即可或者`ctrl+a`同时(同时也不松开)按方向键
>
> 5).全屏与取消全屏：某个窗口全屏：选中并按下`ctrl+A`再按`z`
> 同样取消按`ctrl+A`再按`z`
>
> 6).挂起窗口：`ctrl+a`然后按`d`，此为从session中退出
> 输入tmux a 或tmux attach，再开启session窗口
>
> 7).选择其他的session：先进入tmux，然后在tmux里输入`ctrl+a`再按`s`
> 再session里的方向键操作：
> `→`展开，`→`再按一次是展开所有pane `←`按下是合上所有pane
> `←`合上
> `↑↓`选择session
>
> 如下所示：一共9个session，点开展开是一系列window，再展开window是pane
>
> ![QQ截图20220716231316.png](assets\109718_4086724007-QQ截图20220716231316.png)
>
> 8).session中创建window与选择window：`ctrl+a`再按`c`：创建window
> `ctrl+a`再按`w`：选择其他window也可以展开合上每个window
>
> 注：`ctrl+a+s`与`ctrl+a+w`的区别:前者打开只展开session一级，展示session级中所有的window如图一，后者打开默认是w一级，展开window级中所有的pane，如图二
>
> ![QQ截图20220716231316.png](assets\109718_4086724007-QQ截图20220716231316.png)
>
> ![QQ截图20220716231355.png](assets\109718_8f4fe78d07-QQ截图20220716231355.png)
>
> 9).翻阅内容：`↑`滚轮向上
> 如果没有鼠标：`ctrl+a`再按`Pageup`向上翻，按`PageUp`向下翻
> 按`PageUp`也可以唤醒 按一次`ctrl + a`即可
>
> 10).从tmux中复制文本：
> 按住`shift`键选择文本
> `ctrl+insert`复制
> `shift+insert`粘贴
> mac电脑：`command+c`复制
> `command+v`粘贴

### vim

#### 功能

> 1.命令行模式下的文本编辑器
> 2.根据扩展名判别编程语言，实现代码缩进、代码高亮

#### 使用

> `vim filename`
> 如果有该文件则打开
> 没有则打开一个新的文件，命名为`filename`

#### 模式

> 1.一般命令模式/默认模式：无法编写，输入命令，每一个命令对应一个字母，支持复制粘贴删除文本
> 2.编辑模式：在默认模式下按`i`，进入编辑模式，按`esc`退出
> 3.命令行模式：默认模式下按`：/？`三个中任意一个进入命令行模式，命令行在最下面（个人建议用`：`）支持查找、替换、保存、退出、配置编辑器等
> 输入`:wq`,保存并退出

#### 操作

> 1.`i`：进入编辑模式
>
> 2.`esc`：进入一般命令模式
>
> 3.小键盘可以操作前后左右
> 注：在命令模式下：vim会卡在最后一个字符前面，编辑模式会卡在最后一个字符，不像win，移动到最后会直接换行
> 同样的，无论是什么模式，往左移动到开头就会停下
>
> 4.光标的移动操作：`n<Space>` `n`是数字，光标会自动右移`n`个字符
> 一般命令模式下：`0/home` 将光标移动到本行开头
> `$/End `将光标移动到本行结尾
> G:光标移动到最后一行
>
> 5.具体到哪一行的操作：
> 1).`n/nG`:表示想去具体到哪一行（`n`是到某一行的下面，`nG`是直达）
> 2).`gg`:到达第一行
> 3).`n<Enter>` 向下跳`n`行
>
> 6.查找与修改字符串的操作：
> 1).`/word`:在命令行模式下，光标之下寻找第一个值为`word`的字符串
> 2).`?word`:在光标之上第一个值为`word`的字符串
> 3).`n`:重复前一个查找操作
> 4).`N`:反向查找，也就是说前一个命令向前找，此命令下向后找
> 5).`:n1,n2s/word1/word2/g`:`n1`,`n2`为数字，在第`n1`与`n2`之间找`word1`，并替换为`word2`
> `:1,$s/word1/word2/g`: 将全文的`word1`换成`word2`
> `:1,$s/word1/word2/gc`:在每一次替换的时候都会让用户进行确认
>
> 7.`:noh `关闭所查找的关键词的高亮
>
> 8.选中与删除
> `v`:选中文本,按两下`esc`取消
> `d`:删除选中文本(其实有剪切的特性)
> `dd`:删除整行
>
> 9.复制与粘贴：
> `y`:复制(文本)
> `p`:在光标所处位置的下一行或下一个位置(通常当光标在两边时)粘贴
> `yy`:复制当前行
>
> 10.撤销:`u`:撤销
> `ctrl+r`:取消撤销
> 注:在windows里，`ctrl+z`撤销，`ctrl+shift+z`取消撤销
>
> 11.`>` 将选中的文本整体向右移动
> `<` 将选中的文本整体向左移动
>
> 12.保存与退出：
> `:w`保存
> `:w!` 强制保存
> 一般命令模式下:按下`ESC`，按`q`退出
> `:q! `强制退出（不保存）
> `:wq` 保存并退出
> `:wq! `强制保存退出
>
> 13.行号的显示与隐藏:
> `:set nonu` 隐藏行号
> `:set nu` 显示行号
>
> 14.`paste`模式:
> 为什么:当要粘贴过来的代码很长时，命令可能会失效，占用很大带宽，导致出现多重缩进
> `:set paste`取消代码缩进，设置成粘贴模式
> `:set nopaste`开启代码缩进
>
> 15.其他与`gg`有关的
> `gg+d+G` 删除全部内容
> `gg=G` 将全文格式化
>
> 16.`vim`的卡死处理
> `ctrl+q`:当`vim`卡死时，可取消当前正在执行的命令
>
> 17.异常处理:当前进程出现冲突时，会出现异常
> 解决方法：1).找到正在多个打开的文件程序，并关掉，保证同一个进程只有同一个文件能打开
> 2).问题：当一个进程不小心被其他进程杀掉，当再打开`main.cpp`时，此时如果出现一个`.swp`缓存文件时会报错
> 解决：在没有任何一个进程打开该文件时，将`.swp`文件删掉即可

## 第三节：shell语法

### 概论：

shell是我们通过命令行与操作系统沟通的语言。

shell脚本可以直接在命令行中执行，也可以将一套逻辑组织成一个文件，方便复用。
AC Terminal中的命令行可以看成是一个**“shell脚本在逐行执行”**。

Linux中常见的shell脚本有很多种，常见的有：

- Bourne Shell(`/usr/bin/sh`或`/bin/sh`)
- Bourne Again Shell(`/bin/bash`)
- C Shell(`/usr/bin/csh`)
- K Shell(`/usr/bin/ksh`)
- zsh
- …

Linux系统中一般默认使用bash，所以接下来讲解bash中的语法。

文件开头需要写`#! /bin/bash`，指明bash为脚本解释器。

#### 脚本示例

新建一个`test.sh`文件，内容如下：

```shell
#! /bin/bash
echo "Hello World!"
```

#### 运行方式

作为可执行文件

```Linux
acs@9e0ebfcd82d7:~$ chmod +x test.sh  # 使脚本具有可执行权限
acs@9e0ebfcd82d7:~$ ./test.sh  # 当前路径下执行
Hello World!  # 脚本输出
acs@9e0ebfcd82d7:~$ /home/acs/test.sh  # 绝对路径下执行
Hello World!  # 脚本输出
acs@9e0ebfcd82d7:~$ ~/test.sh  # 家目录路径下执行
Hello World!  # 脚本输出
```

```linux
acs@9e0ebfcd82d7:~$ bash test.sh
Hello World!  # 脚本输出
```

### 注释：

#### 单行注释：

每行中`#`之后的内容均是注释。

```bash
# 这是一行注释

echo 'Hello World'  #  这也是注释
```

#### 多行注释

格式：

```bash
:<<EOF
第一行注释
第二行注释
第三行注释
EOF
```

其中`EOF`可以换成其它任意字符串。例如：

```bash
:<<abc
第一行注释
第二行注释
第三行注释
abc

:<<!
第一行注释
第二行注释
第三行注释
!
```

### 变量：

#### 定义变量

定义变量，不需要加`$`符号，例如：

```bash
name1='varus'  # 单引号定义字符串
name2="varus"  # 双引号定义字符串
name3=varus    # 也可以不加引号，同样表示字符串
```

#### 使用变量

使用变量，需要加上`$`符号，或者`${}`符号。花括号是可选的，主要为了帮助解释器识别变量边界。

```bash
name=varus
echo $name  # 输出varus
echo ${name}  # 输出varus
echo ${name}huihe  # 输出varushuihe
```

#### 只读变量

使用`readonly`或者`declare`可以将变量变为只读。

```bash
name=varus
readonly name
declare -r name  # 两种写法均可

name=abc  # 会报错，因为此时name只读
```

#### 删除变量

`unset`可以删除变量。

```bash
name=varus
unset name
echo $name  # 输出空行
```

#### 变量类型

1. 自定义变量（局部变量）
   子进程不能访问的变量
2. 环境变量（全局变量）
   子进程可以访问的变量

自定义变量改成环境变量：

```bash
acs@9e0ebfcd82d7:~$ name=varus  # 定义变量
acs@9e0ebfcd82d7:~$ export name  # 第一种方法
acs@9e0ebfcd82d7:~$ declare -x name  # 第二种方法
```

环境变量改为自定义变量：

```bash
acs@9e0ebfcd82d7:~$ export name=varus   # 定义环境变量
acs@9e0ebfcd82d7:~$ declare +x name  # 改为自定义变量
```

#### 字符串

字符串可以用单引号，也可以用双引号，也可以不用引号。

单引号与双引号的区别：

- 单引号中的内容会原样输出，不会执行、不会取变量；
- 双引号中的内容可以执行、可以取变量；

```bash
name=varus  # 不用引号
echo 'hello, $name \"hh\"'  # 单引号字符串，输出 hello, $name \"hh\"
echo "hello, $name \"hh\""  # 双引号字符串，输出 hello, varus "hh"
```

获取字符串长度

```bash
name="varus"
echo ${#name}  # 输出5
```

提取子串

```bash
name="hello, varus"
echo ${name:0:5}  # 提取从0开始的5个字符
```

### 默认变量：

#### 文件参数变量

在执行shell脚本时，可以向脚本传递参数。`$1`是第一个参数，`$2`是第二个参数，以此类推。特殊的，`$0`是文件名（包含路径）。例如：

创建文件`test.sh`：

```bash
#! /bin/bash

echo "文件名："$0
echo "第一个参数："$1
echo "第二个参数："$2
echo "第三个参数："$3
echo "第四个参数："$4
```

然后执行该脚本：

```bash
acs@9e0ebfcd82d7:~$ chmod +x test.sh 
acs@9e0ebfcd82d7:~$ ./test.sh 1 2 3 4
文件名：./test.sh
第一个参数：1
第二个参数：2
第三个参数：3
第四个参数：4
```

#### 其它参数相关变量

| 参数                                | 说明                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| `$#`                                | 代表文件传入的参数个数，如上例中值为4                        |
| `$*`                                | 由所有参数构成的用空格隔开的字符串，如上例中值为`"$1 $2 $3 $4"` |
| `$@`                                | 每个参数分别用双引号括起来的字符串，如上例中值为`"$1" "$2" "$3" "$4"` |
| `$$`                                | 脚本当前运行的进程ID                                         |
| `$?`                                | 上一条命令的退出状态（注意不是stdout，而是exit code）。0表示正常退出，其他值表示错误 获取返回值的 |
| `$(command)`                        | 返回`command`这条命令的stdout（可嵌套）获取输出的 例如想获得ls的标准输出： $(ls) 即可 |
| `command`<br />(左右就是两个着重号) | 返回command这条命令的stdout（不可嵌套）获取输出的            |

### 数组：

数组中可以存放多个不同类型的值，只支持一维数组，初始化时不需要指明数组大小。
**数组下标从0开始。**

#### 定义

数组用小括号表示，元素之间用空格隔开。例如：

```bash
array=(1 abc "def" varus)
```

也可以直接定义数组中某个元素的值：

```bash
array[0]=1
array[1]=abc
array[2]="def"
array[3]=varus
```

#### 读取数组中某个元素的值

格式：

```bash
${array[index]}
```

例如：

```bash
array=(1 abc "def" yxc)
echo ${array[0]}
echo ${array[1]}
echo ${array[2]}
echo ${array[3]}
```

#### 读取整个数组

格式：

```bash
${array[@]}  # 第一种写法
${array[*]}  # 第二种写法
```

例如：

```bash
array=(1 abc "def" yxc)

echo ${array[@]}  # 第一种写法
echo ${array[*]}  # 第二种写法
```

#### 数组长度

类似于字符串

```bash
${#array[@]}  # 第一种写法
${#array[*]}  # 第二种写法
```

例如：

```bash
array=(1 abc "def" yxc)

echo ${#array[@]}  # 第一种写法
echo ${#array[*]}  # 第二种写法
```

### expr命令：

`expr`命令用于求表达式的值，格式为：

```bash
expr 表达式
```

表达式说明：

- 用空格隔开每一项
- 用反斜杠放在shell特定的字符前面（发现表达式运行错误时，可以试试转义）
- 对包含空格和其他特殊字符的字符串要用引号括起来
- expr会在`stdout`中输出结果。如果为逻辑关系表达式，则结果为真时，`stdout`输出1，否则输出0。//返回值是标准输出
- expr的`exit code`：如果为逻辑关系表达式，则结果为真时，`exit code`为0，否则为1。

#### 字符串表达式

- `length STRING`
  返回`STRING`的长度
- `index STRING CHARSET`
  `CHARSET中`任意单个字符在`STRING`中最前面的字符位置，**下标从1开始**。如果在`STRING`中完全不存在`CHARSET中`的字符，则返回0。
- `substr STRING POSITION LENGTH`
  返回`STRING`字符串中从`POSITION`开始，长度最大为`LENGTH`的子串。如果`POSITION`或`LENGTH`为负数，0或非数值，则返回空字符串。

示例：

```bash
str="Hello World!"

echo `expr length "$str"`  # ``不是单引号，表示执行该命令，输出12
echo `expr index "$str" aWd`  # 输出7，下标从1开始
echo `expr substr "$str" 2 3`  # 输出 ell
```

#### 整数表达式

`expr`支持普通的算术操作，算术表达式优先级低于字符串表达式，高于逻辑关系表达式。

- `+ -`
  加减运算。两端参数会转换为整数，如果转换失败则报错。
- `* / %`
  乘，除，取模运算。两端参数会转换为整数，如果转换失败则报错。
- `()`
  可以改变优先级，但需要用反斜杠转义

示例：

```bash
a=3
b=4

echo `expr $a + $b`  # 输出7
echo `expr $a - $b`  # 输出-1
echo `expr $a \* $b`  # 输出12，*需要转义
echo `expr $a / $b`  # 输出0，整除
echo `expr $a % $b` # 输出3
echo `expr \( $a + 1 \) \* \( $b + 1 \)`  # 输出20，值为(a + 1) * (b + 1)
```

#### 逻辑关系表达式

- `|`
  如果第一个参数非空且非0，则返回第一个参数的值，否则返回第二个参数的值，但要求第二个参数的值也是非空或非0，否则返回0。如果第一个参数是非空或非0时，不会计算第二个参数。(短路原则)
- `&`
  如果两个参数都非空且非0，则返回第一个参数，否则返回0。如果第一个参为0或为空，则不会计算第二个参数。
- `< <= = == != >= >`
  比较两端的参数，如果为true，则返回1，否则返回0。”==”是”=”的同义词。”expr”首先尝试将两端参数转换为整数，并做算术比较，如果转换失败，则按字符集排序规则做字符比较。
- `()`
  可以改变优先级，但需要用反斜杠转义

示例：

```bash
a=3
b=4

echo `expr $a \> $b`  # 输出0，>需要转义
echo `expr $a '<' $b`  # 输出1，也可以将特殊字符用引号引起来
echo `expr $a '>=' $b`  # 输出0
echo `expr $a \<\= $b`  # 输出1

c=0
d=5

echo `expr $c \& $d`  # 输出0
echo `expr $a \& $b`  # 输出3
echo `expr $c \| $d`  # 输出5
echo `expr $a \| $b`  # 输出3
```

### read命令：

`read`命令用于从标准输入中读取单行数据。当读到文件结束符时，`exit code`为1，否则为0。

参数说明

- `-p`: 后面可以接提示信息
- `-t`：后面跟秒数，定义输入字符的等待时间，超过等待时间后会自动忽略此命令

实例：

```bash
acs@9e0ebfcd82d7:~$ read name  # 读入name的值
varus  # 标准输入
acs@9e0ebfcd82d7:~$ echo $name  # 输出name的值
varus  #标准输出
acs@9e0ebfcd82d7:~$ read -p "Please input your name: " -t 30 name  # 读入name的值，等待时间30秒
Please input your name: varus  # 标准输入
acs@9e0ebfcd82d7:~$ echo $name  # 输出name的值
varus  # 标准输出
```

### echo命令:

`echo`用于输出字符串。命令格式：

```bash
echo STRING
```

#### 显示普通字符串

```bash
echo "Hello World"
echo Hello World  # 引号可以省略
```

#### 显示转义字符

```bash
echo "\"Hello World\""  # 注意只能使用双引号，如果使用单引号，则不转义
echo \"Hello World\"  # 也可以省略双引号
```

#### 显示变量

```bash
name=varus
echo "My name is $name"  # 输出 My name is varus
```

#### 显示换行

```bash
echo -e "Hi\n"  # -e 开启转义
echo "varus"
```

输出结果：

```
Hi

varus
```

#### 显示不换行

```bash
echo -e "Hi \c" # -e 开启转义 \c 不换行
echo "varus"
```

输出结果：

```
Hi acwing
```

#### 显示结果定向至文件

```bash
echo "Hello World" > output.txt  # 将内容以覆盖的方式输出到output.txt中
```

#### 原样输出字符串，不进行转义或取变量(用单引号)

```bash
name=varus
echo '$name\"'
```

输出结果

```
$name\"
```

#### 显示命令的执行结果

```bash
echo `date`
```

输出结果：

```bash
Wed Sep 1 11:45:33 CST 2021
```

### printf命令：

`printf`命令用于格式化输出，类似于`C/C++`中的`printf`函数。

**默认不会在字符串末尾添加换行符。**

命令格式：

```bash
printf format-string [arguments...]
```

#### 用法示例

脚本内容：

```bush
printf "%10d.\n" 123  # 占10位，右对齐
printf "%-10.2f.\n" 123.123321  # 占10位，保留2位小数，左对齐
printf "My name is %s\n" "varus"  # 格式化输出字符串
printf "%d * %d = %d\n"  2 3 `expr 2 \* 3` # 表达式的值作为参数
```

输出结果：

```bush
       123.
123.12    .
My name is varus
2 * 3 = 6 
```

### test命令与判断符号[]:

#### 逻辑运算符&&和||

- `&& 表示与，|| 表示或`
- 二者具有短路原则：可以利用短路原则实现ifelse 
  `expr1 && expr2`：当`expr1`为假时，直接忽略`expr2`
  `expr1 || expr2`：当`expr1`为真时，直接忽略`expr2`
- 表达式的`exit code`为0，表示真；为非零，表示假。（与`C/C++`中的定义相反）

#### test命令

在命令行中输入`man test`，可以查看`test`命令的用法。

`test`命令用于判断文件类型，以及对变量做比较。

`test`命令用`exit code`返回结果，而不是使用`stdout`。0表示真，非0表示假。

例如：

```bash
test 2 -lt 3  # 为真，返回值为0
echo $?  # 输出上个命令的返回值，输出0
```

```bash
acs@9e0ebfcd82d7:~$ ls  # 列出当前目录下的所有文件
homework  output.txt  test.sh  tmp
acs@9e0ebfcd82d7:~$ test -e test.sh && echo "exist" || echo "Not exist"
exist  # test.sh 文件存在
acs@9e0ebfcd82d7:~$ test -e test2.sh && echo "exist" || echo "Not exist"
Not exist  # testh2.sh 文件不存在
```

#### 文件类型判断

命令格式：

```bash
test -e filename  # 判断文件是否存在
```

| 测试参数 | 代表意义     |
| -------- | ------------ |
| -e       | 文件是否存在 |
| -f       | 是否为文件   |
| -d       | 是否为目录   |

#### 文件权限判断

命令格式：

```bash
test -r filename  # 判断文件是否可读
```

| 测试参数 | 代表意义       |
| -------- | -------------- |
| -r       | 文件是否可读   |
| -w       | 文件是否可写   |
| -x       | 文件是否可执行 |
| -s       | 是否为非空文件 |

#### 整数间比较

命令格式：

```bash
test $a -eq $b  # a是否等于b
```

| 测试参数 | 代表意义       |
| -------- | -------------- |
| -eq      | a是否等于b     |
| -ne      | a是否不等于b   |
| -gt      | a是否大于b     |
| -lt      | a是否小于b     |
| -ge      | a是否大于等于b |
| -le      | a是否小于等于b |

#### 字符串比较

| 测试参数          | 代表意义                                               |
| ----------------- | ------------------------------------------------------ |
| test -z STRING    | 判断STRING是否为空，如果为空，则返回true               |
| test -n STRING    | 判断STRING是否非空，如果非空，则返回true（-n可以省略） |
| test -n STRING    | 判断str1是否等于str2                                   |
| test str1 != str2 | 判断str1是否不等于str2                                 |

#### 多重条件判定

命令格式：

```bash
test -r filename -a -x filename
```

| 测试参数 | 代表意义                                            |
| -------- | --------------------------------------------------- |
| -a       | 两条件是否同时成立                                  |
| -o       | 两条件是否至少一个成立                              |
| ！       | 取反。如 test ! -x file，当file不可执行时，返回true |

#### 判断符号[]

`[]`与`test`用法几乎一模一样，更常用于`if`语句中。另外`[[]]`是`[]`的加强版，支持的特性更多。

例如：

```bash
[ 2 -lt 3 ]  # 为真，返回值为0
echo $?  # 输出上个命令的返回值，输出0
```

```bash
acs@9e0ebfcd82d7:~$ ls  # 列出当前目录下的所有文件
homework  output.txt  test.sh  tmp
acs@9e0ebfcd82d7:~$ [ -e test.sh ] && echo "exist" || echo "Not exist"
exist  # test.sh 文件存在
acs@9e0ebfcd82d7:~$ [ -e test2.sh ] && echo "exist" || echo "Not exist"
Not exist  # testh2.sh 文件不存在
```

注意：

- `[]`内的每一项都要用空格隔开
- 中括号内的变量，最好用双引号括起来
- 中括号内的常数，最好用单或双引号括起来

例如：

```bash
name="varus"
[ $name == "varus" ]  # 错误，等价于 [ acwing yxc == "acwing yxc" ]，参数太多
[ "$name" == "varus" ]  # 正确
```

### 判断语句

#### if…then形式

类似于`C/C++`中的`if-else`语句。

##### 单层if

命令格式：

```bash
if condition 判断的是condition的exit code
then
    语句1
    语句2
    ...
fi
```

示例：

```bash
a=3
b=4

if [ "$a" -lt "$b" ] && [ "$a" -gt 2 ]
then
    echo ${a}在范围内
fi
```

输出结果：

```
3在范围内
```

##### 单层if-else

命令格式

```bash
if condition
then
    语句1
    语句2
    ...
else
    语句1
    语句2
    ...
fi
```

示例：

```bash
a=3
b=4

if ! [ "$a" -lt "$b" ]
then
    echo ${a}不小于${b}
else
    echo ${a}小于${b}
fi
```

输出结果：

```
3小于4
```

##### 多层if-elif-elif-else

命令格式:

```bash
if condition
then
    语句1
    语句2
    ...
elif condition
then
    语句1
    语句2
    ...
elif condition
then
    语句1
    语句2
else
    语句1
    语句2
    ...
fi
```

示例：

```bash
a=4

if [ $a -eq 1 ]
then
    echo ${a}等于1
elif [ $a -eq 2 ]
then
    echo ${a}等于2
elif [ $a -eq 3 ]
then
    echo ${a}等于3
else
    echo 其他
fi
```

输出结果：

```
其他
```

#### case…esac形式

类似于`C/C++`中的`switch`语句。

命令格式 分号分号不可以删除

```bash
case $变量名称 in
    值1)
        语句1
        语句2
        ...
        ;;  # 类似于C/C++中的break
    值2)
        语句1
        语句2
        ...
        ;;
    *)  # 类似于C/C++中的default
        语句1
        语句2
        ...
        ;;
esac
```

示例：

```bash
a=4

case $a in
    1)
        echo ${a}等于1
        ;;  
    2)
        echo ${a}等于2
        ;;  
    3)                                                
        echo ${a}等于3
        ;;  
    *)
        echo 其他
        ;;  
esac
```

输出结果：

```
其他
```

### 循环语句

#### for…in…do…done

命令格式：

```bash
for var in val1 val2 val3
do
    语句1
    语句2
    ...
done
```

示例1，输出a 2 cc，每个元素一行：

```bash
for i in a 2 cc
do
    echo $i
done
```

示例2，输出当前路径下的所有文件名，每个文件名一行：

```bash
for file in `ls`
do
    echo $file
done
```

示例3，输出1-10

```bash
for i in $(seq 1 10)
do
    echo $i
done
```

示例4，使用{1..10} 或者 {a..z}

```bash
for i in {a..z}
do
    echo $i
done
```

#### for ((…;…;…)) do…done

命令格式：

```bash
for ((expression; condition; expression))
do
    语句1
    语句2
done
```

示例，输出1-10，每个数占一行：

```bash
for ((i=1; i<=10; i++))
do
    echo $i
done
```

#### while…do…done循环

命令格式：

```bash
while condition
do
    语句1
    语句2
    ...
done
```

示例，文件结束符为`Ctrl+d`，输入文件结束符后`read`指令返回false。

```bash
while read name
do
    echo $name
done
```

#### until…do…done循环

当条件为真时结束。

命令格式：

```bash
until condition
do
    语句1
    语句2
    ...
done
```

示例，当用户输入yes或者YES时结束，否则一直等待读入。

```bash
until [ "${word}" == "yes" ] || [ "${word}" == "YES" ]
do
    read -p "Please input yes/YES to stop this program: " word
done
```

#### break命令

跳出当前一层循环，注意与`C/C++`不同的是：`break`不能跳出`case`语句。

示例

```bash
while read name
do
    for ((i=1;i<=10;i++))
    do
        case $i in
            8)
                break
                ;;
            *)
                echo $i
                ;;
        esac
    done
done
```

该示例每读入非EOF的字符串，会输出一遍1-7。
该程序可以输入`Ctrl+d`文件结束符来结束，也可以直接用`Ctrl+c`杀掉该进程。

#### continue命令

跳出当前循环。

示例：

```bash
for ((i=1;i<=10;i++))
do
    if [ `expr $i % 2` -eq 0 ]
    then
        continue
    fi
    echo $i
done
```

该程序输出1-10中的所有奇数。

#### 死循环的处理方式

如果AC Terminal可以打开该程序，则输入`Ctrl+c`即可。

否则可以直接关闭进程：

1. 使用`top`命令找到进程的PID
2. 输入`kill -9 PID`即可关掉此进程

### 函数

`bash`中的函数类似于`C/C++`中的函数，但`return`的返回值与`C/C++`不同，返回的是`exit code`，取值为0-255，0表示正常结束。

如果想获取函数的输出结果，可以通过`echo`输出到`stdout`中，然后通过`$(function_name)`来获取`stdout`中的结果。

函数的`return`值可以通过`$?`来获取。

命令格式：

```bash
[function] func_name() {  # function关键字可以省略
    语句1
    语句2
    ...
}
```

#### 不获取` return`值和`stdout`值

示例

```bash
func() {
    name=varus
    echo "Hello $name"
}

func
```

输出结果：

```bash
Hello varus
```

#### 获取` return`值和`stdout`值

不写`return`时，默认`return 0`。

示例

```bash
func() {
    name=varus
    echo "Hello $name"

    return 123
}

output=$(func)
ret=$?

echo "output = $output"
echo "return = $ret"
```

输出结果：

```bash
output = Hello varus
return = 123
```

#### 函数的输入参数

在函数内，`$1`表示第一个输入参数，`$2`表示第二个输入参数，依此类推。

注意：函数内的`$0`仍然是文件名，而不是函数名。

示例：

```bash
func() {  # 递归计算 $1 + ($1 - 1) + ($1 - 2) + ... + 0
    word=""
    while [ "${word}" != 'y' ] && [ "${word}" != 'n' ]
    do
        read -p "要进入func($1)函数吗？请输入y/n：" word
    done

    if [ "$word" == 'n' ]
    then
        echo 0
        return 0
    fi  

    if [ $1 -le 0 ] 
    then
        echo 0
        return 0
    fi  

    sum=$(func $(expr $1 - 1))
    echo $(expr $sum + $1)
}

echo $(func 10)
```

输出结果：

```
55
```

#### 函数内的局部变量

可以在函数内定义局部变量，作用范围仅在当前函数内。

可以在递归函数中定义局部变量。

命令格式：

```bash
local 变量名=变量值
```

例如：

```bash
#! /bin/bash

func() {
    local name=varus
    echo $name
}
func

echo $name
```

输出结果：

```
varus
```

第一行为函数内的name变量，第二行为函数外调用name变量，会发现此时该变量不存在。

### exit命令

`exit`命令用来退出当前`shell`进程，并返回一个退出状态；使用`$?`可以接收这个退出状态。

`exit`命令可以接受一个整数值作为参数，代表退出状态。如果不指定，默认状态值是 0。

`exit`退出状态只能是一个介于 0~255 之间的整数，其中只有 0 表示成功，其它值都表示失败。

示例：

创建脚本`test.sh`，内容如下：

```bash
#! /bin/bash

if [ $# -ne 1 ]  # 如果传入参数个数等于1，则正常退出；否则非正常退出。
then
    echo "arguments not valid"
    exit 1
else
    echo "arguments valid"
    exit 0
fi
```

执行该脚本：

```bash
acs@9e0ebfcd82d7:~$ chmod +x test.sh 
acs@9e0ebfcd82d7:~$ ./test.sh v
arguments valid
acs@9e0ebfcd82d7:~$ echo $?  # 传入一个参数，则正常退出，exit code为0
0
acs@9e0ebfcd82d7:~$ ./test.sh 
arguments not valid
acs@9e0ebfcd82d7:~$ echo $?  # 传入参数个数不是1，则非正常退出，exit code为1
1
```

### 文件重定向

每个进程默认打开3个文件描述符：

- `stdin`标准输入，从命令行读取数据，文件描述符为0
- `stdout`标准输出，向命令行输出数据，文件描述符为1
- `stderr`标准错误输出，向命令行输出数据，文件描述符为2

可以用文件重定向将这三个文件重定向到其他文件中。

#### 重定向命令列表

| 命令               | 说明                                      |
| ------------------ | ----------------------------------------- |
| `command > file`   | 将`stdout`重定向到`file`中                |
| `command < file`   | 将`stdin`重定向到`file`中                 |
| `command >> file`  | 将`stdout`以追加方式重定向到`file`中      |
| `command n> file`  | 将文件描述符`n`重定向到`file`中           |
| `command n>> file` | 将文件描述符`n`以追加方式重定向到`file`中 |

#### 输入和输出重定向

```bash
echo -e "Hello \c" > output.txt  # 将stdout重定向到output.txt中
echo "World" >> output.txt  # 将字符串追加到output.txt中

read str < output.txt  # 从output.txt中读取字符串

echo $str  # 输出结果：Hello World
```

#### 同时重定向stdin和stdout

创建bash脚本：

```bash
#! /bin/bash

read a
read b

echo $(expr "$a" + "$b")
```

创建input.txt，里面的内容为：

```
3
4
```

执行命令：

```bash
acs@9e0ebfcd82d7:~$ chmod +x test.sh  # 添加可执行权限
acs@9e0ebfcd82d7:~$ ./test.sh < input.txt > output.txt  # 从input.txt中读取内容，将输出写入output.txt中
acs@9e0ebfcd82d7:~$ cat output.txt  # 查看output.txt中的内容
7
```

### 引入外部脚本

类似于`C/C++`中的`include`操作，`bash`也可以引入其他文件中的代码。

语法格式：

```bash
. filename  # 注意点和文件名之间有一个空格

或

source filename
```

**示例**

创建`test1.sh`，内容为：

```bash
#! /bin/bash

name=varus  # 定义变量name
```

然后创建`test2.sh`，内容为：

```bash
#! /bin/bash

source test1.sh # 或 . test1.sh

echo My name is: $name  # 可以使用test1.sh中的变量
```

执行命令：

```bash
acs@9e0ebfcd82d7:~$ chmod +x test2.sh 
acs@9e0ebfcd82d7:~$ ./test2.sh 
My name is: varus
```

## 第四节：ssh

### ssh登录

#### 基本用法

远程登录服务器：

```linux
ssh user@hostname
```

- `user` : 用户名
  - `hostname` : IP地址或域名


第一次登录会提示：

```
The authenticity of host '123.57.47.211 (123.57.47.211)' can't be established.
ECDSA key fingerprint is SHA256:iy237yysfCe013/l+kpDGfEG9xxHxm0dnxnAbJTPpG8.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

输入`yes`，然后回车即可。
这样会将该服务器的信息记录在`~/.ssh/known_hosts`文件中。

然后输入密码即可登录到远程服务器中。

默认登录端口号为22。如果想登录某一特定端口：

```
ssh user@hostname -p 22
```

#### 配置文件

创建文件 `~/.ssh/config`。

然后在文件中输入：

```
Host myserver1
    HostName IP地址或域名
    User 用户名

Host myserver2
    HostName IP地址或域名
    User 用户名
```

之后再使用服务器时，可以直接使用别名`myserver1`、`myserver2`。

#### 密钥登录

创建密钥：

```
ssh-keygen
```

然后一直回车即可。

执行结束后，`~/.ssh/`目录下会多两个文件：

- `id_rsa`：私钥
- `id_rsa.pub`：公钥

之后想免密码登录哪个服务器，就将公钥传给哪个服务器即可。

例如，想免密登录`myserver`服务器。则将公钥中的内容，复制到`myserver`中的`~/.ssh/authorized_keys`文件里即可。

也可以使用如下命令一键添加公钥：

```
ssh-copy-id myserver
```

#### 执行命令

命令格式：

```
ssh user@hostname command
```

例如：

```
ssh user@hostname ls -a
```

或者

```
# 单引号中的$i可以求值
ssh myserver 'for ((i = 0; i < 10; i ++ )) do echo $i; done'
```

或者

```
# 双引号中的$i不可以求值
ssh myserver "for ((i = 0; i < 10; i ++ )) do echo $i; done"
```

### scp传文件

#### 基本用法

命令格式：

```
scp source destination
```

将`source`路径下的文件复制到`destination`中



一次复制多个文件：

```
scp source1 source2 destination
```



复制文件夹：

```
scp -r ~/tmp myserver:/home/acs/
```

将本地家目录中的`tmp`文件夹复制到`myserver`服务器中的`/home/acs/`目录下。

```
scp -r ~/tmp myserver:homework/
```

将本地家目录中的`tmp`文件夹复制到`myserver`服务器中的`~/homework/`目录下。

```
scp -r myserver:homework .
```

将`myserver`服务器中的`~/homework/`文件夹复制到本地的当前路径下。



指定服务器的端口号：

```
scp -P 22 source1 source2 destination
```

注意： `scp`的`-r` `-P`等参数尽量加在`source`和`destination`之前。

#### 使用`scp`配置其他服务器的`vim`和`tmux`

```
scp ~/.vimrc ~/.tmux.conf myserver:
```

## 第五节：git

### 1.1git基本概念

- 工作区：仓库的目录。工作区是独立于各个分支的。
- 暂存区：数据暂时存放的区域，类似于工作区写入版本库前的缓存区。暂存区是独立于各个分支的。
- 版本库：存放所有已经提交到本地仓库的代码版本
- 版本结构：树结构，树中每个节点代表一个代码版本。

### 1.2 git常用命令

1. `git config --global user.name xxx`：设置全局用户名，信息记录在`~/.gitconfig`文件中

2. `git config --global user.email xxx@xxx.com`：设置全局邮箱地址，信息记录在`~/.gitconfig`文件中

3. `git init`：将当前目录配置成git仓库，信息记录在隐藏的`.git`文件夹中

4. `git add XX`：将XX文件添加到暂存区

   `git add .`：将所有待加入暂存区的文件加入暂存区

5. `git rm --cached XX`：将文件从仓库索引目录中删掉

6. `git commit -m` "给自己看的备注信息"：将暂存区的内容提交到当前分支

7. `git status`：查看仓库状态

8. `git diff XX`：查看XX文件相对于暂存区修改了哪些内容

9. `git log`：查看当前分支的所有版本

10. `git reflog`：查看HEAD指针的移动历史（包括被回滚的版本）

11. `git reset --hard HEAD^` 或 `git reset --hard HEAD~`：将代码库回滚到上一个版本

    `git reset --hard HEAD^^`：往上回滚两次，以此类推

    `git reset --hard HEAD~100`：往上回滚100个版本

    `git reset --hard` 版本号：回滚到某一特定版本

12. `git checkout — XX`或`git restore XX`：将XX文件尚未加入暂存区的修改全部撤销

13. `git remote add origin git@git.acwing.com:xxx/XXX.git`：将本地仓库关联到远程仓库

14. `git push -u` (第一次需要-u以后不需要)：将当前分支推送到远程仓库

    `git push origin branch_name`：将本地的某个分支推送到远程仓库

15. `git clone git@git.acwing.com:xxx/XXX.git`：将远程仓库XXX下载到当前目录下

16. `git checkout -b branch_name`：创建并切换到`branch_name`这个分支

17. `git branch`：查看所有分支和当前所处分支

18. `git checkout branch_name`：切换到`branch_name`这个分支

19. `git merge branch_name`：将分支`branch_name`合并到当前分支上

20. `git branch -d branch_name`：删除本地仓库的`branch_name`分支

21. `git branch branch_name`：创建新分支

22. `git push --set-upstream origin branch_name`：设置本地的`branch_name`分支对应远程仓库的`branch_name`分支

23. `git push -d origin branch_name`：删除远程仓库的`branch_name`分支

24. `git pull`：将远程仓库的当前分支与本地仓库的当前分支合并

    `git pull origin branch_name`：将远程仓库的`branch_name`分支与本地仓库的当前分支合并

25. `git branch --set-upstream-to=origin/branch_name1 branch_name2`：将远程的`branch_name1`分支与本地的`branch_name2`分支对应

26. `git checkout -t origin/branch_name` 将远程的`branch_name`分支拉取到本地

27. `git stash`：将工作区和暂存区中尚未提交的修改存入栈中

28. `git stash apply`：将栈顶存储的修改恢复到当前分支，但不删除栈顶元素

29. `git stash drop`：删除栈顶存储的修改

30. `git stash pop`：将栈顶存储的修改恢复到当前分支，同时删除栈顶元素

31. `git stash list`：查看栈中所有元素
