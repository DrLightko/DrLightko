# Java 入门
> 摘自陈宝峰老师的网课，如有侵权请联系删除
## 第一章：Java的简介
### 1.1 历史
* Java本由*SUN公司*开发，之后被*Oracle公司*收购，原名叫做*Oak (橡树)*，1995年Java才正式诞生，1996年发布第一个非Beta版
* ***Java是分平台的***：
    * ***Java SE (Java Standard Edtion) 标准版平台***，负责**单机平台开发**，应用面最广
    * **Java EE (Java Enterprise Edition) 企业平台**，用于**开发大型、复杂分布型软件**
    * **Java ME (Java Micro Edition) 微平台**，**嵌入式、移动应用开发**
> 无论是 Java EE 还是 Java ME 都站在 Java SE 的肩膀上，都需要SE提供的开发组件，本文就介绍Java SE
* ***Java是编译运行的***，但是过程略有不同，运行过程如下：
```
program.java --> --> --> program.class (字节码) --> --> 0100101 (机器码) --> CPU
^                 ^                         ^
|                 |                         |
源码    compiler (Java编译器)    Java Virtual Machine (Java虚拟机)
```
> 相当于解决了传统编译运行的痛点，比如在编译时就已经可以检查错误，在**解释时速度就会提高**，并且经过编译后的**字节码是可以跨平台的** (机器码当然不可以)，也就是***先编译后解释***
### 1.2 开发环境
* 开发环境简介：
    * **JVM是Java的解释器***，负责生成最后的机器码，***JVM不能跨平台***
    * JRE (Java Runtime Environment) 是***Java运行时环境***，它是java程序运行所必须的环境集合，主要由java虚拟机、java平台核心类和若干支持文件组成
    * JDK (Java Development Kit)，简称Java开发工具包，***包含JRE以及其他开发套件***
```
JDK--------------------
| 包含
|   JRE---------------
|    | 包含
|    |      JVM-----
|    |       |
```
> 我们一般直接使用JDK
### 1.3 下载与安装
* ***下载与安装*** (以Windows为例)：
    * Java发展至今版本极多，一般使用 **LTSC (长久支持) 版本为保稳定性**，而且Java被收购后并不完全免费，**最后一个完全免费可商用的版本是Java 8的一个版本** (版本号可以上网找)
    * Java LTSC 目前最新版是 Java 21，但是这里**以Java 17 为例** (不建议使用过老的版本)，并且是 **OpenJDK 版本** (因为是免费商用)，图省事可以看[微软的打包版本](https://learn.microsoft.com/zh-cn/java/openjdk/download)
    * 在Windows下面直接**解压文件添加到环境变量**即可，十分简单 (Linux也一样)
        * 首先新建一个**个人变量** (系统变量也行，但是养成好习惯) 名字为 **JAVA_HOME**，值为JDK文件夹目录
        * 再去**Path变量**里新建两个变量：**变量1：%Java_Home%\bin，变量2：%Java_Home%\jre\bin**
        > ClassPath 无所谓配置，嫌麻烦可以不配置  
        > bin目录里面是Java的可执行文件，里面的java.exe和javac.exe就是Java的虚拟机和编译器，添加到环境变量里就是方便引用
    * 最重要的是打开cmd，输入**java -version 和 javac -version**看有无输出，因为JDK不能跨平台所以一定**要确定自己电脑的指令集、位数和操作系统**
* Java的运行：
```java
// hello.java

public class hello {

    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}

// 看不懂没关系，马上会讲
```
* **源码编写完以后首先需要编译器编译为Java字节码**
```java
javac hello.java

// 这样目录下会多出一个class文件
```
* 之后**再由虚拟机解释执行**
```java
java hello

// 不用打扩展名

>>>
Hello World
```
## 第二章：基本类型与变量定义
### 2.1 数据类型
> 程序不断的进行输入、数据处理、输出的过程，不同的数据类型需要的不同的处理方式和存储方式，这里是Java中的**最基本类型**

|类型|字节|位数|最小值|最大值|
|---|---|---|---|---|
|byte|1|8|-2^7|2^7-1|
|short|2|16|-2^15|2^15-1|
|int|4|32|-2^31|2^31-1|
|long|8|64|-2^63|2^63-1|
|float|4|32|
|double|8|64|
|char|2|16|
|boolean|视情况而定|视情况而定|false|true|

> 注意别忘了**一个字节等于8位**，至于为什么要减一去看C入门

> 没有写布尔值的占用是因为理论上只需要一个bit足矣，但是计算机只能从1byte开始处理，具体的占用这个没有规范，按照官方的规范单独使用和作为数组使用竟然还不一样，单独使用跟int一样，作为数组跟byte一样，到了后面再讲

> 浮点数跟整数表达方式不同，所以没有写出具体最大小值

> Java***字符类型采用unicode编码，所以占用两字节***
### 2.2 变量定义
* ***变量的定义与使用***：
```java
// 定义语法

<类型> <变量名> ;

int num;
```
```java
// 赋值语法

<变量名> = 值;
<类型> <变量名> = 值;

int num;
num = 90;

int num = 90;
```
```java
// 当然也可以多个变量连写

int num1 = 23,num2 = 90;
```
* Java中的***类型转换从低级到高级是自动转换，从高级转换为低级需要强制转换***
```java
int num = 90;

byte b = (byte)num;

// 如果不强制类型转换会报错
// 可能会损失精度

byte b = 12;
short s = b;
int n = b;
n = 203;

// 都是可以的，数据引用不影响原值
```
* ***常量的定义与使用***：
    * ***字面量是常量***
    ```java
    int num = 2;

    // 我不能说这个2是3，或者2其实是1005对吧
    ```
    * ***利用final关键字自定义常量***
    ```java
    final int num = 90;

    num = 89;
    // 报错

    final int num;

    num = 23;
    // 也可以先定义再初始化
    ```
* 注意，下面的b变量是一个byte类型没有错，但是右边的 8 请注意，如果***字面量是一个整数类型的字面量，Java默认按照int来处理***，但是把int赋值给byte不会报错吗
```java
byte b = 8;
```
> ***对于byte short类型的变量而言，在赋值的时候，如果被赋的值为可预知的常量，即便是高于  byte或 Short的类型，系统也会自动判断其常量值是否能够放置于byte或short类型的变量中。如果能够则编译正确，否则将会产生编译错误***
```java
byte b = 127;
// 正确

byte b = 128;
// 错误
```
> 可预知的常量是什么意思，看一下
```java
final int i;
i = 12;

byte b = i;

// 报错，因为先是定义了i这个常量，之后再赋值，赋值语句不执行的话编译器是不知道i的值的，恰好Java编译器不负责执行
// 所以i未知无法自动赋值
```
> 所以注意**定义赋值语句在不在一行区别很大**
* 再来看一下字面量的处理
```java
long l = 2147483648;

// 会报错，为什么？是因为编译器把右边的整形字面量当作int来处理，但是这个字面量的值已经超过int的值了，所以会溢出
// 只能强制类型转换了

long l = (long)2147483648;

// 还是报错，因为你告诉编译器后面的是一个long，编译器说好，但是他还是按照int来处理，
// 那只能这样了

long l = 2147483648L;

// 这个后缀告诉编译器按照long来处理
```
* 还要注意，***整数类型字面量默认当做int类型，浮点数默认为double***
```java
float f = 2.3;

// 你猜会怎样，2.3是一个双精度浮点数，但是并没有超过float的极限啊
// 但是之前说了，只有byte和short才有这个功能，所以有以下选项

float f = (float)2.3;
float f = 2.3F;
```
* ***字符赋值使用单引号***：
```java
char c = 'c';
char c = '\n';

// 转义字符

char c = '\u0065';

// 也可以直接使用utf编码引用，想知道编码值可以这样

System.out.println((int)c);
```
> 这里还是注意，老生常谈**Windows的控制台编码是GBK**，输出结果报错信息为编码 GBK 的不可映射字符 (0xB8)，需要在***javac的参数列表多一条 -encoding UTF-8***参数即可
* **布尔值的使用**：
```java
boolean b = true;
boolean b = false;

// true 和 false也是两个内置常量
```
### 2.3 标识符
* ***标识符包括包名、类名、方法名、参数名、变量名等 (这里只关注变量名)***
> 换句话说这些名称命名遵守标识符命名法则：
1. 标识符可以***由字母、数字、下划线_ 和 美元符号 $ 组成***
2. 标识符***不能以数字开头***
3. ***Java 区分大小写***，因此 myvar 和 MyVar 是两个不同的标识符
4. **不可以使用关键字和保留字作为标识符**，但标识符中能包含关键字和保留字
5. 标识符**不能包含空格**
* 保持良好的书写习惯也有利，比如Java推荐***变量或方法名采用驼峰命名法 (myMathGrade)，常量名大写 (PI)，类型和接口名首字母大写，包名全小写***
> 采用有意义的名称作为变量名
* Java 内保留的**关键字如下**，他们不能单独作为标识符：

|类型|关键字|
|----|----|
数据类型|boolean、int、long、short、byte、float、double、char、class、interface、enum、void|
流程控制|if、else、do、while、for、switch、case、default、break、continue、return|
异常处理|try、catch、finally、throw、throws|
修饰符|public、protected、private、final、void、static、strict、abstract、transient、synchronized、volatile、native|
类与类之间关系|extends、implements|
建立实例及引用实例|this、supper、instanceof、new|
导包|package、impor|
> java**关键字和保留字都是小写**，即null是关键字，NULL不是关键字；TRUE、FALSE也不是关键字

* **保留字是 Java 为以后版本预留可能会加入功能的字符，也不能作为标识符**
> goto、const、byValue、cast、future、 generic、 inner、 operator、 outer、 rest、 var
* 注意：***Java中true、false、friendly和null不属于关键字，也不是保留字，它们只是显式常量值，但是你在程序中不能使用它们作为标识符***

## 第三章：操作符与表达式
* ***表达式由操作数 (运算子)和运算符组成，没有分号结尾***，比如下面
### 3.1 算术运算操作符
* \+    加法运算符
* \-    减法运算符
* \*    乘法运算符
* \/    除法运算符
* %     取余
* ++    自增运算符
* --    自减运算符
```java
3 + 2

// 这是一个由操作数和操作符构成的表达式，但不是语句

int num = 3 + 2;

// 这就是一条语句
```
* 对于加减运算，原来的数据是什么类型结果就是什么类型，但是乘除请注意：
* ***整数之间 byte，short，int 这三种类型的整数之间运算，结果都为int类型***
```java
short s1 = 2,s2 = 3;
short s3 = s1 + s2;

// 错误: 不兼容的类型: 从int转换到short可能会有损失
```
* long比int范围大，为了让long与其他三种整数类型参与运算，***整数与long运算结果结果为long (自动向上提升范围)***
* ***当一个整数与浮点数运算，为保证精度结果会自动提升为浮点数***
```java
5/2 = 2;
5/2.0 = 2.5;

// 请注意上面
// 所以在对两个int进行除法时请注意先将其中一个运算数转为浮点
// 而且注意浮点数默认运算结果为double，比如

float s4 = 5/2.0;

// 也是会报错的，因为从double转为float
```
> 无论如何在**涉及浮点数的运算时一定要小心谨慎**，计算机跟人不一样
* 还请注意***自增自减运算符位置也是可变动的，区别在于先返回操作数还是先自增*** (详情请看C入门)
```java
int n = 2;
int m = n++;
// m = 2,n = 3
int m = ++n;
// m = 3,n = 3

// 区别在于是先返回自己还是先自增再返回自己
```
```java
int n = 2;
int m = n++ + n++;
// m = 2 + 3,n = 4

int n = 2;
int m = n++ + ++n;
// m = 2 + 4,n = 4
```
### 3.2 位运算操作符
* ~     按位取反
* &     与
* |     或
* ^     异或
* \>>   有符号右移
* \>>>  无符号右移
* <<    左移
```java
byte n1 = 10;
byte n2 = (byte) ~n1;
System.out.println(n2);

// 打印结果是 -11 为啥
// 打开计算器，可以看到对 0000 1010 (因为一个 byte 等于 8 位) 按位取反就是 1111 0101，也就是 245
// 但是byte最大显示 127，245 - 127 = 118 从 -128 开始往正数方向再数 118 个，也就是 -11 (注意是从 128 开始所以数到 -11 还剩下 10 个)

// 还请注意，Java整数运算默认int，上面不加强制转换的话会报错
```
> 忘了说，***Java没有无符号整型原生支持***，可能是为了简化，反正从 C 到 Python 这些杂七杂八的底层工具都被简化掉了
```java
byte m1 = 2;
byte m2 = 3;
byte m3 = (byte) (m1 & m2);

// m1 = 0000 0010
// m2 = 0000 0011

// m1 & m2 = 0000 0010
// m1 | m2 = 0000 0011
// m1 ^ m2 = 0000 0001
```
> 上面要注意**不能直接加强制类型转换，应注意运算优先级**，实在不确定就加上小括号
```java
byte m1 = 2;
byte m2 = m1 >> 1;

// 0000 0010 >> 0000 0001 这就是右移的意思
```
* ***右移时，最高位是0，左边补齐0；最高为是1，左边补齐1***，这是右移的补全规则，左移没有统统补齐0
* ***无符号右移无论最高位是0还是1，左边补齐0***
* **左移 m<<n 代表把数字m在无溢出的前提下乘以2的n次方，右移m>>n 代表把数字m除以2的n次方，原来是正数的还是正数，负数还是负数。注意，如果是单数，也就是二进制末位为1，则结果是将m除以2的n次方的整数商**
> 小技巧，可以利用位移来存储信息，比如把一个byte的八个字节当作八个开关，每一个开关用0和1来表示，那怎样去读取这个一个数的某一位信息呢？
```java
byte num = 3; // 0000 0011
byte res = (num >> 1) & 1;

// 什么意思，把要比较的那一位 (这里是第二位) 对齐到最右面与 1 做与运算，只有都是一的时候才返回一，根据这个结果便可以进行判断

System.out.println(res);
```
### 3.3 比较运算符
* \>     大于
* <     小于
* \>=   大于等于
* <=    小于等于
* ==    等于
* !=    不等于
```java
int num = 10;

boolean res = 10 > 5;

// 如果一个表达式的结果是布尔值，也可以叫他布尔表达式
```
### 3.4 逻辑运算操作符
* &&    与操作
* ||    或操作
* !     非操作
* ^     异或
> ***跟之前位运算的区别在于这里操作符接受的是布尔值，返回也是布尔值***
```java
int num = 20;

boolean res = (num > 10) && (num < 30);

// 只有同时满足上面两个条件res才是true

res = !res;
```
* & 和 | 也可以用作逻辑判断，所以这里重点阐述 ***& 和 && 以及 | 和 || 的区别，单个 & 前面表达式为真时，继续执行后面的表达式，最后再得出结果，而两个 && 则是前面表达式为假时就不会再执行后面的表达式，直接得出FALSE的结果；单个 | 前面的表达式为真时，程序会继续执行后面的表达式，然后在得出TRUE的结果，两个 || 前面的表达式结果为真，则程序不会再执行后面的表达式，直接得出TRUE的结果***
> 在后面的逻辑判断语句中可以自己尝试
### 3.5 其他操作符
* ***三元表达式 ? :***，**问号前面是一个布尔值，后面两个数据类型要一致，根据布尔值返回一或二**
```java
int num = 23;
int m = num > 20 ? 1 : 0;

// num > 20 返回 1，num < 20 返回 0
```
* ***连写运算符***，可以把运算符与等号连写简化
```java
int num = 10;

num += 10;  // num = num + 10;
num -= 10;
num /= 10;
num *= 10;
num %= 10;

num >>= 1; // num = num >> 1;
num <<= 1;
num >>>= 1;

num &= 1; // num = num & 1;
num ^= 1;
num |= 1;
```
### 3.6 表达式的自动提升
* ***表达式也有返回类型，由表达式中精度最高的类型决定，如果最高精度类型低于int类型，返回值自动提升为int***
> 也就是Java表达式返回结果不能比int小
```java
byte b1 = 12;
byte b2 = 34;

byte b3 = b1 + b2;

// 报错，必须要强制类型转换

byte b3 = (byte) (b1 + b2);
```
```java
byte b1 = 12;

byte b2 = b1 >>> 5;

// 所有的运算都要注意，比如上面 b1 是 byte，但是 5 是 int，结果自动提升为 int，再赋给 byte 是不对的
```
## 第四章：基本语句
### 4.1 条件语句
* ***if……else……语句语法***
```java
if (布尔表达式) {
    语句;
} else if (布尔表达式) {
    语句;
} else if (布尔表达式) {
    语句;
} 
···
else {
    语句;
}

// 注意必须是布尔表达式，不能是0或者1
```
```java
int grade = 70;

if (grade >= 90) {
    System.out.println("优");
} else if (grade >= 80) {
    System.out.println("良");
} else if (grade >= 70) {
    System.out.println("中");
} else {
    System.out.println("差");   
}

// 这里还是注意可以少写几个判断
```
> 当**大括号内的语句只有一句时也可以省略括号**
```java
if (grade >= 90) System.out.println("优");

// 但是阅读不便
```
### 4.2 分支语句
* ***switch分支语句语法***
```java
switch (表达式) {
    case 常量1:
        语句;
    case 常量2:
        语句;
    case 常量3:
        语句;
    ···
    default:
        语句;
}

// 注意表达式类型只能为 byte short int char 不能是其他类型
// 首先执行表达式得到一个值
// 然后从case1开始一步一步往下找哪个常量等于这个值
// 找到之后从这个case开始执行自己的语句，再往下每个case中的语句都执行一遍
// 如果找不到则从default开始执行

int num = 90;

switch (num) {
    case 10:
        System.out.println("num is 10");
    case 50:
        System.out.println("num is 50");
    case 90:
        System.out.println("num is 90");
    default:
        System.out.println("num dont know");
}

// 注意会把 case 90 和 default 都打印
```
> default可以不写
* 如果不想让都打印一遍，***可以加入 break 关键字打断***
```java
int month = 2;

switch (month) {
    default:
        System.out.println("未知月份");
        break;
    case 1:
        System.out.println("一月份");
        break;
    case 2:
        System.out.println("二月份");
        break;
    case 3:
        System.out.println("三月份");
        break;
}

// default 未知不影响判断，永远是先判断case
// 这样每一个月份就只会打印一次

switch (month) {
    default:
        System.out.println("未知月份");
    case 1:
        System.out.println("一月份");
    case 2:
        System.out.println("二月份");
    case 3:
        System.out.println("三月份");
}

// 那这样子他是从未知开始打印还是从一月份开始
// 因为没有符合的，所以从default开始往下，从未知开始
```
### 4.3 循环语句
#### 4.3.1 while语句
```java
while (布尔表达式) {
    语句;
}

// 先判断布尔值为不为真，在执行语句
// 执行完成回来再判断一遍，再执行
```
```java
int num = 1;
int res = 0;

while (num < 101) {
    res += num;
    num++;
}

System.out.println(res);

// 高斯没错
```
#### 4.3.2 do……while……语句
```java
do {
    语句;
} while (布尔表达式);

// 记住while后面有个分号
// 先执行后判断，无论如何都要执行一次
```
```java
char star = '*';
int num = 1;

do {
    System.out.print(star);
    // 这个不是println代表结果不会换行
    num ++;
} while (num < 100);

// 利用循环打印星号
```
#### 4.3.3 for语句
```java
for (初始化表达式;条件表达式;步进表达式) {
    语句;
}

// 一上来先初始化，一定会执行
// 接着条件判断，根据真假执行循环体语句，之后执行步进表达式
// 接着回到条件表达式，直到判断为假跳出

// 控制表达式的初始化和步进控制部分，可以使用一系列由逗号分隔的语句，而且那些语句均会独立执行
// 通过逗号操作符，可以在for语句定义多个变量，但是它们必须是相同的类型


for (int i = 0,j = 78; i < 10; i++, j++) {
    System.out.println(i);
    System.out.println(j);
}

// 也可以不写，只写上分号表示忽略条件

for (;;) {
    // 死循环
}
```
```java
for (int i = 0; i < 100; i++) {
    System.out.println(i);
}
```
### 4.4 练习
> 打印出从一到一百的素数
* 这个案例其实在 C 入门里也应该讲一下，但是在这里一块讲解，首先***判断一个整数m是否是素数，只需把 m 被 2 ~ m-1 之间的每一个整数去除，如果都不能被整除，那么 m 就是一个素数***，这是因为素数的定义***是指除了 1 和它本身以外，不能被任何整数整除的数***
> 基于这个思路可以写出以下:
```c
// 单独判断

#include <stdio.h>


int main(int argc, char const *argv[]){
    int n;

    printf("enter a num < 2:\n");
    scanf("%i",&n);

    if (n < 3) {
        printf("sorry i cant determine 0 1 & 2\n");
        return 1;
    }

    // 因为我们的程序不能判断2以前的，所以先淘汰
    
    for (int i = 2; i < n ; i++) {
        // 从 2 循环到本身小一

        if  ((i == n - 1) && (n%i != 0)) {
            printf("%i is a prime",n);
            return 0;
        } else if (n%i == 0){
            printf("%i is not a prime",n);
            break;
        }

        // 这里第一个if是检测如果i已经循环一遍了并且这一遍也不能整除的话就完成
        // 第二个是检测途中如果整除了可以直接打断
        // 那剩下的不能整除并且没有循环完的就继续循环
    }

    return 0;
}
```
```java
// 连续判断

public class b {
    public static void main(String[] args) {
        
        for (int i = 3; i <= 100; i++) {
            // 这里我们判断一到一百范围内的整数，同样不包括 1 和 2
            for (int j = 2; (j < i) && (i%j != 0); j++) {
                // 这里可以简单一些在判断部分直接筛选出不能整除的，下面的if只需判断循环完了没有即可
                if (j == i - 1) {
                    System.out.println(i);
                    // 判断出来的打印
                }
            }

            //当这个 for 循环完 第一层的 for 进入下一阶段

        }
    }
}
```
* 这个思路还能进一步简化，其实 ***m 不必被 2 ~ m-1 之间的每一个整数去除，只需被 2 ~ $\sqrt{m}$ 之间的每一个整数去除就可以了。如果 m 不能被 2 ~ $\sqrt{m}$ 间任一整数整除，m 必定是素数，因为如果 m 能被 2 ~ m-1 之间任一整数整除，其二个因子必定有一个小于或等于 $\sqrt{m}$，另一个大于或等于 $\sqrt{m}$***
> 根据这个思路可以简化 C 的，使用开方记得导入 <math.h>
## 第五章：类的定义与使用
> 终于进入了Java最强大也是最基础的一个功能
### 5.1 面向对象的概念
* 对象：
> 这些概念听听就好，主要是实例理解
* ***万物皆是对象，对象具有唯一性，对象具有属性和行为 (属性是静态的特征，行为是动态的)***
* 类：
* ***类是一组具有相同属性和行为的对象的抽象，类是一个概念、是一个规范***
> 比如一张我问你什么是汽车，你想到很多品牌的车子型号，奔驰宝马或者大众的等等，这每一辆叫的上名字的车辆就是对象，他是实实在在的存在的实例；但如果你想到的是汽车的原理或者发动机，这个叫类，他不是实例，只是一个抽象，或者说一张图纸，设计图纸拿给各个厂家他们自己实现不同的功能

> 或者说明白一点，**方法就是函数，属性就是成员变量**
### 5.2 类的定义
* 语法如下，注意包含了函数语法以及变量使用，看过之前的话会省略很多
```java
<修饰符> class <类名字> {

    <修饰符> <类型> <属性名称>;
    // 就是变量

    ···

    <修饰符> <返回值类型> <方法名字>(参数列表) {
        方法体的=中的语句;
    }
    // 就是函数

    ···
}


// Student.java

public class Student {
    // 这里注意，虽然还没有讲修饰符，但是被这里的public修饰符名称必须跟文件名相同，也就是一个文件只能定一个public类

    public int age;

    public void doSomething(int a,int b) {
        System.out.println("你好世界");
    }

    // 注意这个函数返回void而不是没有返回值

    public int add(int a,int b) {
        int res = a + b;

        return res;

        // return后面的语句不会执行
    }
}
```
### 5.3 对象的定义与使用
* **创建对象**
```java
<类名字> <引用变量的名字> = new 类名字();

// 这就相当于给那个类起了个别名，这个对象绑定一个类

Student s1 = new Student();
Student s2 = new Student();

// 这里的s1、s2叫做引用类型的变量，他不是对象，只是一个别名
// 引用类型的变量存储的就是那个对象的地址

Student s3 = s1;

// 这样的话是把s1的值也就是对象的地址赋值给s3，这两个引用类型指向的一个对象
// 很像指针对吧
```
* ***对象是通过对象引用变量来访问的，该变量包含了对对象的引用***。假设我们自己定义一个类Circle，这个类是一种引用类型。**该类类型的变量都可以引用该类的一个实例**
从表面上看，对象引用变量种似乎存放了一个对象；但是事实上，***它只是存放了对该对象的引用***
* 我们之前介绍的***基本类型变量和引用类型变量有根本上的差别***：
    * 对于**基本类型变量**，***在内存种存储的是一个基本类型值，可以在栈中直接分配内存***
    ```java
    int n = 23;
    int m;
    m = n;

    // n 里面就是 23 的补码，直接将 23 赋给了 m
    ```
    * 对于**引用类型变量**，***对应内存所存储的值是一个引用，是对象的存储地址，对象的引用在栈中，对象实际存放在堆中***
    ```java
    Student s1 = new Student();
    Student s2 = new Student();
    
    s2 = s1;

    // 这里是将 s1 指向的对象地址赋给 s2 ，s2 和 s1 指向同一个对象，之前 s2 指向的对象就访问不到了，在 C 里面我们讲过这个内存就无法被释放了，会一直占用，但是 Java 有一个垃圾回收机制，下面会讲
    ```
* ***调用属性和方法***
```java
// 属性赋值的语法

<引用名>.<属性名> = 值;

s1.age = 23;
s2.age = 90;
// 这就是使用类之前要实例的作用，可以实例化多个各不相同的对象

// 使用方法的语法

<引用名>.<方法名>(参数列表);

int i = 12,j = 23;
int res = s1.add(i,j);
```
### 5.3 方法的传递与返回
* ***方法中的参数传递是值传递 (拷贝传递)***，任何函数中的修改都不会影响原值
```java
// d.java

class Data {
    public int id;

// 这个类只有一个属性 (成员变量)
}

class Util {
    public void change(Data d) {
        d.id++;
    }

// 这个类只有一个方法 (函数)
// 注意参数d的类型是Data，也就是需要接收一个对象的引用变量
}

public class d {

    public static void main(String[] args) {
        
        // main函数

        Data d1 = new Data();
        d1.id = 5;
        
        // 这里实例化一个类，内存中多出一个对象，这个对象里的一个整形变量赋值为5

        Util u1 = new Util();
        u1.change(d1);

        // 又实例化一个类，这块空间内的一个函数调用，把 d1 这个引用类型变量传递给它
        // 确实是值传递，但是这里 d1 的值是一个地址，传递给 Util 里的 change 函数里的 d 实参，d 和 d1 都指向一个对象，相当于是通过地址访问到另一块空间

        System.out.println(d1.id);
    
        // 所以自然id的值被修改了
    }
}
```
```java
class Data {
    public int id;
}

class Util {
    public void change(Data d) {
        d = new Data();
        d.id = 9;

        // 你这里看清楚，加了一个new之后这是新建了一个对象，只能被 d 引用到
        // 所以出了这个函数谁都访问不到这个新建对象了，自然main里面的d1值也不会变

        d.id++;
    }
}

public class d {

    public static void main(String[] args) {
        Data d1 = new Data();
        d1.id = 5;
        
        Util u1 = new Util();
        u1.change(d1);

        System.out.println(d1.id);
    }
}
```
* ***所有方法都有返回值类型，void不能被称为没有返回值，而是要被看成void类型***
### 5.4 类的构造方法
* 构造方法的定义语法：
```java
<修饰符> class <类名字> {
    <修饰符> <构造方法名 (和类名字完全一样)>(参数列表) {
        // 最大的区别就在于他不用写返回值，并且名称和类名完全一样，大小写也是
        
        方法体内容;
    }
}
```
* ***构造方法的作用就是新建对象时初始化的***
> 比如这里 Data 有自己的构造方法，**这个函数就是你在新建对象时的后面那个括号，没有写构造方法时系统会自动写一个空的方法**，也就是之前见到的没有参数的新建。  

> 现在写了参数列表就要求新建对象时也写明参数，这个参数在这里被用作给 id 参数初始化，你可以看到即使没有对 id 赋值他里面也已经有了值
```java
class Data {
    public Data(int i) {
        id = i;
    }

    // 这是有参构造，上文是无参构造

    public int id;
}

class Util {
    public void change(Data d) {
        d.id++;
    }
}

public class d {

    public static void main(String[] args) {
        Data d1 = new Data(9);
        System.out.println(d1.id);
        d1.id = 5;
        
        Util u1 = new Util();
        u1.change(d1);

        System.out.println(d1.id);
    }
}
```
> **构造方法只能在 new 后面用**
## 第六章：类的初始化与方法的重载
### 6.1 类的初始化步骤
* 第一步：**属性的默认初始化**
    * **首先创建出类的实例：对象**
    ```java
    // Book.java

    public class Book {
        public double price;
        // 这个叫成员变量
    }

    class App {
        public static void main(String args[]) {
            Book b = new Book();
            System.out.println(b.price);
            // 但是这种

            int i;
            // 这个是函数内的本地变量
            System.out.println(i); // 这种变量不初始化会报错

        }
    }
    ```
    * **如果一个对象的属性值没有显性的赋值，Java会自动初始化缺省值**，比如浮点数就是0.0，整形是0，字符是 '\0'，布尔值是 false，那么缺省值怎样写？
    ```java
    public class Book {
        public double price = 8;
        // 这个就是默认缺省值，他不是在赋值而是缺省值，只有在实例化对象时才会使用
    }
    ```
* 第二步：**初始化模块的初始化**
    > 这里使用的花括号还有其他的作用，以后再讲
    ```java
    class Test {
        public int id;
        public float price = 15.69;

        {
            id = 24;
            price = 85.3;
        }

        // 注意这是在类里面和属性和方法并列的地方
        // 每一次新建对象就会执行这里面的
    }
    ```
    > 注意**先执行属性缺省值，再初始化模块**
    * ***可存在多个初始化模块，优先级从上至下执行***
    ```java
    class Test {
        {
            id = 89;
            price = -96.5;
        }

        // 没用因为被后面的覆盖掉

        public int id;
        public float price = 15.69;

        {
            id = 24;
            price = 85.3;
        }

    }  
    ```
* 第三步：**执行构造方法**
    * ***只有当所有初始化模块执行完之后才执行构造方法***
### 6.2 重载
#### 6.2.1 类的方法重载
> 先看一个示例：
```java
class Calculater {
    public int add(int a,int b) {
        return a + b;
    }

    public double addDouble(double a,double b) {
        return a + b;
    }
}

// 能不能让这两个函数拥有一个名字？
```
* ***方法重载的目的就是让类似的方法具有相同的名字，简化对方法的调用***
* ***在方法重载时，任意两个重载的方法之间在方法参数的个数上或是一一对应的参数类型上，至少有一项存在差别，方法的返回值类型不收任何限制***
> 至少有一点区别，不然完全一样也不行，我们上面的就符合要求
```java
class Calculater {
    public int add(int a,int b) {
        System.out.println("int add");
        return a + b;
    }

    public double add(double a,double b) {
        System.out.println("double add");
        return a + b;
    }
}

public class e {

    public static void main(String[] args) {
        Calculater cal = new Calculater();
        
        System.out.println(cal.add(6,8));

    }
}

// 这就是方法重载
```
> 方法重载在编译期间就确定了，并且系统会自动选择最适合的，比如把上面的8改成8.0就会调用addDouble
#### 6.2.2 构造方法的重载
* **没错，构造方法也可以重载，与普通方法重载完全一样**
```java
class Book {
    int id;
    double price = 9.3;

    public Book() {
        id = 89;
        price = 10.6;
    }

    public Book(int a,int b) {
        id = a + 10;
        price = b + 8.9;
    }
}

// 调用时根据你输入的类型自动选择一个构造方法初始化
```
* ***重载的构造方法之间也可以互相调用使用 this 关键字***
```java
class Book {
    int id;
    double price = 9.3;

    public Book() {
        this(56,32);

        // 就是 
        // Book(65,32);
        // 这个 this 以后还会讲，这里不必了解原理
    }

    public Book(int a,int b) {
        id = a + 10;
        price = b + 8.9;
    }
}
```
* ***但是如果本地变量 (就是函数中的局部变量) 跟成员变量同名怎么办***谁知道自己是谁
* ***可以使用 this 关键字表示当前对象***：
    * **this.属性 区别成员变量和局部变量**
    * **this.() 调用本类的某个方法**
    * **this() 表示调用本类构造方法，只能用在构造方法的第一行语句**
    * **this关键字只能出现在非static修饰的代码中**

> ***成员变量 (属性) 位于类里面，与方法同级；本地变量就是局部变量的意思，位于函数 (方法) 中，也在参数声明 (形参) 中***
* Java 中***本地优先***
```java
class Book {
    int id;
    double price = 9.3;

    public Book() {
        id = 89;
        price = 10.6;
    }

    public Book(int id,int b) {
        // id = id; // ?

        // 使用 this 关键字

        this.id = id;
        // this 后面的是属性，等号右面的是局部变量
        // this 必须在第一句话

        price = b + 8.9;
    }
}
```
* ***对于常量属性，系统不会自动初始化，那么我们可以在缺省值、初始化模块和构造方法里初始化，这时候请注意每一个构造方法中都要定义常量值并且不能重定义***
```java
class Calculater {
    public int add(int a,int b) {
        System.out.println("int add");
        return a + b;
    }

    public double add(double a,double b) {
        System.out.println("double add");
        return a + b;
    }
}


class Book {
    public final double PI;
    // 如果在这里定义缺省值的话下面就不能再定义了
    public int id;
    public double price = 9.3;

    public Book() {
        this(90, 50);

        // PI = 3.1415926;
        // 这里不能定义因为他还会引用下面的重载会重定义
        // 如果不使用this就要定义了:
    /* 
    public Book() {
        PI = 3.14159;
    }

    public Book(int a,int b) {
        id = a + 10;
        price = b + 8.9;

        PI = 3.14;
    }
    */
        // 没错是可以定义不同的
    }

    public Book(int a,int b) {
        id = a + 10;
        price = b + 8.9;

        PI = 3.14;
    }
}


public class e {

    public static void main(String[] args) {
        Calculater cal = new Calculater();
        
        System.out.println(cal.add(6,8));

        Book b = new Book();

        System.out.println(b.PI);

    }
}
```
## 第七章：类的继承和方法覆盖
### 7.1 概念
```java
汽车
 |  \
 |   \
轿车  大卡车
 |  \
 |   \
宝马  奥迪

// 轿车一定是汽车，但汽车一定是轿车吗？
// 轿车更具象，特征更多，汽车更抽象，汽车的属性轿车一定有，但是反过来不一定
// 可以把汽车看作父类，轿车是子类，二者是继承关系，轿车继承了汽车的特征同时还拥有了自己特有的特征
// 从宝马的一辆具体类型到汽车就是越来越抽象的过程就是不断继承
// 在编程里如果我们写了轿车和大卡车的代码，里面的重合部分就可以抽象出来单独作为一个类，成为他们的父类，提高代码复用率
```
### 7.2 语法格式
```java
<修饰符> class <子类名称> extends <父类名称> {
    ···
}
```
```java
class Bus1 {
    public double price;
}

class Bus2 {
    public double price;

    public int type;
}

// 能不能把相同部分不用再写一遍
```
```java
class Bus1 {
    public double price;
}

class Bus2 extends Bus1 {
    // public double price; 不用写了
    // 子类拥有父类的全部属性加上自己可以再加

    public int type;
}
```
* ***一个子类只能继承于一个父类 (单继承)，如果定义类的时候没有什么父类，系统会自动让他继承 Object 类，子类的类型当然是父类***
### 7.3 JVM 里的继承实现
> 这里来讲解一下在Java的虚拟机里面是怎样具体实现对象的构造以及继承的，这一章对于之后的动态绑定十分重要，建议认真理解

> 这里就不对 C 入门里面讲过的在做讲解了，有兴趣的可以看前面的文章，关于堆和栈做了很详细的讲解

* 先让我们看一下JVM里面有哪些部分：
```java
|-------------------------------------------|
|
|   |-------|   |-------|    |-------|
|   | /*栈*/|   | /*堆*/|     // 方法区
|   |       |   |       |
|   |-------|   |-------|
|                         // 本地方法栈
|                         // 程序计数器


// JAVA 栈：
/*
 * 这个空间可以看作是方法的内存模型，JVM自动对栈区压栈出栈
 * 这个空间里面存储的是局部变量、操作数栈、指向运行时常量池的引用、方法返回地址等等
 * 当栈结束，栈里面的局部变量也就自动释放了
*/


// 堆：
/*
 * 堆空间用来存放对象，可以由多个线程共享，这部分随着JVM启动而创建
 * 垃圾回收也发生在此区域
 * 这部分是可以运行时动态分配的
*/


// 方法区：
/*
 * 方法区在JVM中也是一个非常重要的区域，它与堆一样，是被线程共享的区域
 * 在方法区中，存储了每个类的信息 (包括类的名称、方法信息、字段信息) 、静态变量、常量以及编译器编译后的代码等
 * 常量池用来存储编译期间生成的字面量和符号引用也存放于此
*/

// 这只是几个重要的概念，真正的虚拟机肯定不是这样的，这只是方便了解
```
* 下面让我们看一下内存中如何继承对象：
```java
// 测试代码
// 文件名 j.java


class Father {
    public int num = 9;

    void render(){
        System.out.println("Father" + num);
    }
}


class Son extends Father{
    public int m = 10;
}


class Child extends Son{
    public int n = 90;
    
}
public class j {

    public static void main(String[] args) {
        Child c1 = new Child();
        c1.render();
    }
}
```
1. ***包含 main 函数的 j 类字节码会先载入方法区***：
    ```java
    // Stack                        // Heap



    // Method Area
        /*
         * j.class {
         *     main(String[] args);
         * }
        */
    ```
2. main 函数进栈：
    ```java
    // Stack                        // Heap
        /*
         * main(String[] args){
         *  
         * }
        */


    // Method Area
        /*
         * j.class {
         *     main(String[] args);
         * }
        */   
    ```
3. 继续执行发现new了一个新对象，但是Java还不认得这个Child对象，于是准备把 Child 加载进方法区，但是发现 Child 还继承了 Son ，Son 继承了 Father，所以***加载顺序是 Object --> Father --> Son --> Child***
    ```java
    // Stack                        // Heap
        /*
         * main(String[] args){
         *  
         * }
        */


    // Method Area
        /*
         * j.class {                    Object.class {           Father.class {          Son.class {        Child.class {
         *     main(String[] args); -->                    -->       public int num;         int m;               int n;
         *                                                           void render()方法 -->                 --> 
         * }                            }                        }                       }                  }
        */    
    ```
4. 然后就该新建对象初始化了，首先在堆内开辟一块新空间为 Child 类的对象 c1。根据我们之前讲过的，***先初始化父类在初始化子类***，所以先划出一块空间存放 Father 的属性和方法，然后扩充成 Son 的，最后填上自己的
    ```java
    // Heap
    /*
     * Child 类对象 c1
     *  // Father 类内容：
     *      num : 0 // 这里整数默认初始化值是 0 ，如果是String就是 null，这里是无参构造
     *      render() // 这里存储的只是方法区的地址，调用render会根据这个地址在栈内调用
     * 
     * // Son 类内容：
     *      m : 0
     * 
     * // Child 类内容：
     *      n : 0
     * 
    */
    ```
5.  当 main 函数里调用 render 方法时，他会先根据堆中 render 方法留下的地址找到方法区，根据方法区提供的信息在栈内新建一个栈用于执行函数，执行完成后栈被释放
> 这里需要注意的几个点是：字符串保留在方法区中的常量池 (不考虑Java老版本)，堆中的字符串属性保留的只是一个常量池的地址
### 7.4 方法覆盖
> 子类继承了父类的方法，但是发现这个函数不符合要求，想写一个适合自己的
* ***方法覆盖是指子类在继承父类的时候，对父类中的方法进行重新实现的过程***
```java
class Father {
    public void render() {
        System.out.println("HelloWorld!");
    }
}

class Son extends Father {
    public void render() {
        System.out.println("HelloHeaven");
    }
}

// 这里 render 在子类里面和父类是两个方法，在子类里面覆盖了父类给他的方法
```
* ***注意覆盖时必须完全一样 (修饰符先不说) 不然就重载了 (重载可以跨代)，覆盖之后原来的父类并不影响带式子类里面已经是新的方法了***
> 请看以下成立吗？
```java
Father f = new Son();
```
> 小轿车是汽车吗？
* ***一个父类类型的引用变量可以指向任意的子类对象***
```java
f.render();

// 调用的是谁的？

// 指向的子类的
```
* ***通过引用调方法，不看引用看对象。如果子类有就调用，没有就一层一层往上找，Object也没有就编译出错***
> 这是Java的一个重要特性***多态***，也就是当一个**父类类型的对象指向一个子类类型的实例的时候，通过父类调用方法调用的是子类里的方法**

> ***多态跟继承、封装一起称为面向对象的三大特性***，之前两个我们见过
```java
// 问输出多少？

class X {
    public int id;
    public void out() {
        System.out.println(id);
    }
}


class S extends X {
    public int id;
    public void out() {
        System.out.println(id);
    }
}


class C extends S {
    public int id;
    public void out() {
        System.out.println(id);
    }
}


X f1 = new C();

// 这里我们知道这是可以的

f1.id = 12;
f1.out();

// 上面说 "通过引用调方法，不看引用看对象" ，那这里记住了
```
* ***通过引用调属性，不看对象看引用***
> f1 的 id 值是给 X 赋的值，X 的 id 值是 12，没能继承给 C 因为被覆盖了，但是 f1.out 调用的是自己的方法因为***本地优先***，因为没有赋值所以初始化为 0，打印结果也是 0
* 还有一点，***子类继承父类时构造方法不继承***
> 如果不理解可以看下面的动态绑定
* 当然***父类的属性也可以继承给子类***，但是***父类如果没有一个子类的方法还仍然多态指向子类对象也是不行的***
```java
class Fu {
    int num = 10;
}


class Zi extends Fu {
    void render(){
        System.out.println(num);
    }
}


public class n {
    public static void main(String[] args) {
        Zi f1 = new Zi(); // Fu f1 = new Zi(); 不行
        f1.render();        
    }    
}
```
### 7.6 super 关键字
> 之前讲过 this 关键字代表当前对象，这里就讲一个很像的关键字 super 代表父类
```java
class Bus1 {
    public Bus1() {

    }

    public double price;
}

class Bus2 extends Bus1 {
    public Bus2() {

    }

    public int type;
}

Bus1 b = new Bus2();

// 既然 Bus1 的属性 Bus2 也有，那么 Bus2 的对象初始化的时候父类里面的属性由谁来初始化呢？
```
> **Java 认为应该让自己初始化自己**，也即是子类对象初始化时候会调用父类的构造，所以在子类的构造方法里会有这么一句话
```java
class Bus2 extends Bus1 {
    public Bus2() {
        super();
    }

    public int type;
}
```
* ***super表示父类对象***：
    * **super.属性 表示父类对象中的成员变量**
    * **super.方法()表示父类对象中定义的方法**
    * ***super() 表示调用父类构造方法***
        * 可以指定参数，比如super("Tom",23);
        * **任何一个构造方法的第一行默认是super();**
        * 可以写上，如果未写，会隐式调用super();
    * ***super()只能在构造方法的第一行使用***
    * ***this()和super()都只能在构造的第一行出现，所以只能选择其一***
    * **写了this()就不会隐式调用super()**
```java
class Bus1 {
    public Bus1() {
        System.out.println("Bus1");
    }

    public double price;
}

class Bus2 extends Bus1 {
    public Bus2() {
        super();

        // 加不加一样

        System.out.println("Bus2");
    }

    public int type;
}

Bus1 b = new Bus2();
```
> 会先打印 Bus1 就是因为**先调用父类的构造**
```java
class Bus1 {
    public Bus1(int k) {
        System.out.println("Bus1");
    }

    public double price;
}

class Bus2 extends Bus1 {
    public Bus2() {
        super(89);
        // 这里就要加上参数了因为父类的构造需要参数
        System.out.println("Bus2");
    }

    public int type;
}

Bus1 b = new Bus2();
```
* 那我如果**又需要 this 又要 super 怎么办**
```java
class Bus1 {
    public Bus1() {
        System.out.println("Bus1");
    }

    public double price;
}

class Bus2 extends Bus1 {
    public Bus2() {
        this(3);

        System.out.println("Bus2");
    }

    public Bus2(int j) {
        super();

        // 因为这里是构造方法所以也有一个super，所以上面就不需要 super 了
    }

    public int type;
}

Bus1 b = new Bus2();
```
> ***所有的构造方法中都有一个隐形的 super，当 this 和 super 共同出现时不写 super***
### 7.7 父子类的类型转换
* 理论上如下是可行的，因为都是子类对象，但是编译器不知道所以会报错，***只能强制类型转换***
```java
F f1 = new S();
S s1 = f1;

// 应为

S s1 = (S)f1;
```
> 那么是不是另一个类也可以强制类型转换?
```java
Data d = new Data();

S s1 = (S)d;

// 报错，编译器不傻
```
* ***强制类型转换时，被赋值类型的类型和赋值类型的类型如果又父子关系则不编译错误***，但是
```java
F f1 = new F();
S s1 = (S)f1;

// 这里也有父子关系，但是子类引用类型指向父类对象是不对的

// 编译不报错
// 运行时报错
```
### 7.8 动态绑定
#### 7.8.1 变量的就近原则
* 讲过很多遍但是还是说***Java中的变量查找原则时就近原则，局部变量—>成员变量—>父类—>更高的父类—>......—>Object***
```java
class Father {
    public int num = 9;


}


class Son extends Father{
    public int num = 10;
}


class Child extends Son{
    public int num = 90;
    
    void render(){
        System.out.println("num = " + num);
    }    
}
public class j {

    public static void main(String[] args) {
        Child c1 = new Child();
        c1.render();
    }
}

// 分别注释掉 num=90 ，num=10 和 num = 9 自己试试
```
#### 7.8.2 动态绑定机制
> 上文讲过Java的访问原则时就近法则，但是有些时候也可以被打破
* ***绑定就是一个方法的调用与调用这个方法的类连接在一起的过程被称为绑定***，绑定可以发生在编译时也可以发生在运行时
    * ***静态绑定：前期绑定，编译时绑定***
    * ***动态绑定：后期绑定，运行时绑定***
* 在程序运行前，也就是***编译时期JVM就能够确定方法由谁调用，这种机制称为静态绑定***，如果一个方法由***private、Static、final任意一个关键字所修饰***，那么这个方法是前期绑定的，***构造方法也是前期绑定***
> private只能被自己调用，static可以只通过类名加方法名的方式调用，final方法不会被覆写，详情请见下文*类的高级特性*
* 除了由private、final、static 所修饰的方法和构造方法外，***JVM在运行期间决定方法由哪个对象调用的过程称为动态绑定***
```java
class Father {
    private int num = 9;

    void render(){
        System.out.println("Father" + num);
    }
}


class Son extends Father{
    private int num = 10;
    
    void render() {
        System.out.println("Son" + num);        
    }
}


public class j {

    public static void main(String[] args) {
        Father f1 = new Son();
        f1.render();
    }
}
```
* 上文代码编译器不知道当父类类型的对象指向一个子类的实例时候最后会执行哪一个方法，在运行时候才知道，这也是上文提过的多态，所以***多态的三个要素是：继承、重写、父类对象指向子类实例***
* ***当通过对象的形式调用方法时，该方法会和堆内存中真正的该对象——的内存地址绑定，且这种绑定关系会贯穿方法的执行全过程。这就是所谓的动态绑定机制***
```java
class Father {                  /** 父类 */
    //父类的成员变量
    int temp = 5;
 
    //父类temp变量的getter方法
    public int getTemp() {
        return temp;
    }
 
    //父类的两个关于计算temp变量的成员方法
        //方法一
    public int add_temp() {
        return getTemp() + 10;
    }
        //方法二
    public int add_temp_EX() {
        return temp + 10;
    }
}
 
class Son extends Father {      /** 子类 */
    //子类的成员变量（与父类成员变量同名）
    int temp = 11;
 
    //子类temp变量的getter方法
    public int getTemp() {
        return temp;
    }
 
    //子类的两个关于计算temp变量的成员方法
        //方法一
    public int add_temp() {
        return temp + 100;
    }
        //方法二
    public int add_temp_EX() {
        return getTemp() + 1000;
    }
}

// main
Father father = new Son();
System.out.println(father.add_temp());
System.out.println(father.add_temp_EX());
```
1. 请问打印结果如何？
> 父类引用，说明编译类型是父类类型，而父类中定义了这两个方法，因此编译没问题，可调用 (如果父类里面没有这两个方法编译就不通过)；又因为多态关系——父类引用此时指向了子类对象，因此运行类型为子类，子类重写了父类的这两个方法，当然要优先调用子类中的方法

> 111,1011
2. 注释掉子类的add_temp，打印结果如何？
> 访问不到子类的重写就自然去访问父类的add，问题是父类方法里面的get调用的是谁的呢？根据动态绑定机制，在调用add_temp() 方法时，father引用已经和它指向的Son类对象绑定了，并且这种绑定关系会贯穿方法执行的全过程。因此，这里调用的getTemp() 方法是子类的方法，而不是父类的

> 21,1011
3. 再注释掉子类的EX方法，打印结果如何？
> 调用属性时，不存在动态绑定机制，符合继承机制。因此，根据Java中查找属性的原则，这里的temp变量肯定是Father类本类的temp成员变量，也就是5

> 21,15
## 第八章：变量范围和垃圾回收
### 8.1 变量的分类与有效范围
* ***本地变量*** (局部变量) ：
    1. 定义在**参数**中的本地变量，他的有效范围在**函数内有效**
    ```java
    public static App{
        public void render(int count){
            count++;
        }

        public static void main(String args[]){
            count--;

            // 访问不到，因为出了花括号后就失效了
        }
    }
    ```
    2. 定义在**方法体**中的本地变量，有效范围为**变量定义行开始到代码块结束未为止**，**代码块就是一对对花括号**
    ```java
    public static App{
        public void render(int count){
            count++;

        int key = 1;
        key++;
        }
        // 这里就结束了

        public static void main(String args[]){
            
            int num = 9;

            if(num < 10) {
                int m = 20;
            }

            // m在代码块if里面，出了花括号就没有了
        }
    }
    ```
    > **在for里面语句定义的循环变量也是只有在for里面有效，出了循环就无效了**
* ***成员变量 (属性)***
    * **类中的属性的有效范围是整个类范围**
    ```java
    public static App{
        public void render(int count){
            count++;
        }

        public static void main(String args[]){
            id = 90;

            // 即使id的定义在自己后面但是依然能访问到
        }

        public int id;
    }
    ```
### 8.2 两种变量的区别
* ***初始化的值不同***
    1. 成员变量：有默认值
    2. 局部变量：没有默认值，必须先定义，赋值，最后使用
* ***在类中的位置不同***
    1. 成员变量：类中，方法外
    2. 局部变量：方法中或者方法声明上 (形式参数)。
* ***在内存中的位置不同***
    1. 成员变量：堆内存 (这不一定，要看对象本身，包括字符串就在方法区中的常量池而不是堆中)
    2. 局部变量：栈内存
* ***生命周期不同***
    1. 成员变量：随着对象的创建而存在，随着对象的消失而消失
    2. 局部变量：随着方法的调用而存在，随着方法的调用完毕而消失。
* ***作用范围不同***
    1. 成员变量：类中
    2. 局部变量：从定义到花括号结束
### 8.3 垃圾回收
> 什么是垃圾也就是用不上或者已经分配好但是无法访问的内存空间，对于C语言自己申请的内存必须要自己释放，如果野指针或者内存污染可能会让程序崩溃，但是Java虚拟机的强大之处就是如此，他的垃圾回收程序会大大简化流程，但也带来了一些问题
* Java中的垃圾回收机制是***自动***的，当一个变量无法被任何人使用时，也就是***当一个对象没有任何引用指向的时候，这个变量对象就可以被垃圾回收了***，同时***垃圾回收不能被强制调用***
```java
System.gc()

// 这个方法就是告诉程序可以垃圾回收，但是程序不一定执行
```
```java
class Book {
}

public class App {
    public static void main(String args[]) {
        Book b = new Book();
        System.out.println("dsafdfdasf");
        // b = null;
        // 如果加上这句话那么在这一行就被回收掉
        // 所以当你发现一个对象不会再使用的话，可以提前让他指向null就会被提前回收掉
        System.out.println("adfsgsgfds");
        // 在这一行b被回收掉
    }
}
```
> 问App类里面的make方法制造的Book类对象什么时候回收掉？
```java
class Book {
}

public class App {
    public Book make() {
        Book b = new Book();
        return b;
        // 返回b也就是返回Book的地址
    }

    public static void main(String args[]) {
        App app = new App();
        Book tb = app.make();
        System.out.println("fasd fdsaf sa");
        tb = null;
        // 这一行Book就没有指向了，也就是被回收了
        System.out.println("fagfds");
    }
}
```
## 第九章：类的高级特性
### 9.1 static 关键字
* ***被静态修饰属性和方法被类自身与类的所有对象所共享***，这时变量和函数都存储于方法区中，每一个内存对象都引用的是类描述里一份的内存空间
```java
class b {
    public static int count;
    
}

b b1 = new b();
b1.count = 10;

b b2 = new b();
b2.count = 20;

System.out.println(b1.count);
```
* 因此**可以直接用类名去引用属性和方法**，同时***静态方法中不能直接调用非静态属性和方法***
```java
// 上面的修正：
class b {
    public static int count;    
}

b.count = 10;
b.count = 20;

System.out.println(b.count);
```
> 为什么静态方法不能调用非静态函数或变量呢？

> 当Java新建一个对象的时候，不是说直接new一份到堆中，并不是先在堆中为对象开辟内存空间，而是先将类中的静态方法 (带有static修饰的静态函数) 的代码加载到一个叫做方法区的地方，然后再在堆内存中创建对象

> 所以说静态方法会随着类的加载而被加载。当你new一个对象时，该对象存在于堆内存中，this关键字一般指该对象，但是如果没有 new 对象，而是通过类名调用该类的静态方法也可以

> 在类的非静态成员不存在的时候静态成员就已经存在了，访问一个内存中不存在的东西当然会出错

> JVM肯定不会冒这个风险，让你调用一个可能不存在的方法，所以就索性在你调用的时候就报错，避免以后不必要的麻烦

* **每一个Java主文件里都有一个静态main方法**，这个之前一直见过，这个main的格式一定是固定的
```java
// 写法如下：

public static main(String args[]) {
    for(int i = 0 ; i < args.length ; i++) {
        System.out.println(args[i]);
    }
}

// 这个args数组是用来拿命令行参数的
```
* ***static还可以静态导入***
```java
import static java.lang.Math.*;

System.out.println(random());

// 这样就不需要Math.random了

System.out.println
// 这就是System类里面的一个静态属性out指向一个对象里面的方法println
```
### 9.2 final 关键字
* **final修饰变量，则变量为常量不可更改**
* ***final修饰类，则该类不能被其他类继承***
* ***final修饰方法，则该方法不能被覆盖***
### 9.3 权限修饰符
* ***类前面加public，则该类可以被任何包访问，没有加上public就只能和自己在同一个包中的其他类访问，定义为public的类名字必须和源码文件名完全相同***
* **方法或属性**前面的修饰符：private

| 修饰符    | 同一个类 | 同一个包 | 子类 | 整体 |
| --------- | -------- | -------- | ---- | ---- |
| private   | 是       |          |      |      |
| 不写      | 是       | 是       |      |      |
| protected | 是       | 是       | 是   |      |
| public    | 是       | 是       | 是   | 是   |

> 这样善于封装代码，将一些部敏感部分对用户隐藏起来不允许改变
* ***当一个类只能有一个对象引用的时候，这个类叫单例对象***
```java
// 单例模式的写法

class Factory {
    private Factory() {
    }

    // 构造方法private确保new方法只能被该类内部所调用
    
    private static Factory instance;

    // 静态Factory类型的引用对象

    public static Factory getInstance() {
        if (instance == null) {
            // 如果引用对象为空，就新建一个对象
            instance = new Factory();
        }
        // 否则直接返回对象本身，保证类只被创建一次
        return instance;
    }
}
public class i {
    public static void main(String[] args) {
        Factory f1 = Factory.getInstance();
    }
}
```
### 9.4 封装初认识
> 其实我很怀疑老师的课件安排，对于类最重要的多态封装和继承分太分散，中间再加上上字符串和数组这两个大类，这样安排其实是不合理的。其实从一开始就应该先介绍虚拟机的内存运行机制，然后介绍封装再介绍多态，这样子方便去理解继承的内部逻辑
* 当我们学会private之后就要去接触Java的另一大特性——**封装**，封装的好处有
    * 提高代码的安全性
    * 提高代码的复用性
    * 将复杂的事情变得简单化
```java
class Profile {
    int age;
    float height;
    double weight;

    public Profile(){
        
    }

    public Profile(int age, float height , double weight){
        this.age = age;
        this.height = height;
        this.weight = weight;
    }
}

public class j {

    public static void main(String[] args) {
        Profile pr1 = new Profile(12,165,65.7);
        System.out.println(pr1.age);
    }
}
```
> 上面的代码有个问题，如果什么人在哪里任意修改了Profile里的数据怎么办？可以用private保护，但是那样就没有办法访问了，其实Java的一个特性：
* 被 private 修饰的成员只能在本类中访问，其他类无法直接访问本类中被 private 修饰的成员，但是可以访问本类能访问 private 的 public 方法访问，说人话就是：***子类不能继承父类的私有属性，但是如果父类中公有的方法影响到了父类私有属性，那么私有属性是能够被子类使用的***
```java


class Profile {
    private int age;
    private float height;
    private double weight;

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        if (age > 0) {
            this.age = age;            
        } else {
            System.out.println("invalid age");
        }

        // 这样子还能对输入的数据做限制
    }

    public float getHeight() {
        return height;
    }

    public void setHeight(float height) {
        this.height = height;
    }

    public double getWeight() {
        return weight;
    }

    public void setWeight(double weight) {
        this.weight = weight;
    }


    public Profile(){
        
    }


}
public class j {

    public static void main(String[] args) {
        Profile f1 = new Profile();
        f1.setAge(23);
    }
}
```
* 类是属性和行为的集合，是一个抽象概念。而对象是该类事物的具体体现，是一种具体存在。而***当我们需要对某个类中的一些数据进行保护，不想让外界随意修改它们时，或者当我们想调用某个类中的方法，但又不想将该方法的实现细节暴露出来时，就需要这个封装了***
* 这种写法叫做 ***getter 和 setter***，如果你用的是现代IDE一般都有这个自动补全功能，推荐使用 getter 隐藏属性而不是直接公开属性
> 说了怎么多，再回头看一下this，这个最开始只被当作成员变量和局部变量冲突的方案，其实有点东西
* ***所谓 this 和 super ，其实就是 C 里面的指针，分别返回自己对象的地址和父类的地址***
> this是对象的隐藏属性，是一个指向当前对象的引用。而super，则是指向当前对象父类的引用 (即父类内容内存空间的标识)。当new关键字创建子类对象时，子类对象的堆空间中会有一部分用于存放父类的内容，即继承自父类的非私有成员。super就指向这么一部分。可以理解为，super指向的部分是在this指向的部分的范围内。在使用时，***this从本类开始找，super从父类开始找***
* 还是那句话，***理解继承不能理解为覆写而是扩充***，即使重写了父类里的东西但是那些东西还会在，比如下面的例子
```java
class Father {
    int temp1 = 11;
    int temp2 = 12;
    int temp3 = 13;
}


class Son extends Father {
    int temp1 = 99;
    int temp2 = 89;
    int temp3 = 79;

    public void printTemp() {
        int temp1 = 55555;
        int temp2 = 5555;
        int temp3 = 555;
        System.out.println("按照就近原则,直接输出的temp1 = " + temp1);
        System.out.println("按照就近原则,直接输出的temp2 = " + temp2);
        System.out.println("按照就近原则,直接输出的temp3 = " + temp3);
        System.out.println("----------------------------------------------------------");
 
        System.out.println("使用this关键字,temp1 = " + this.temp1);
        System.out.println("使用this关键字,temp2 = " + this.temp2);
        System.out.println("使用this关键字,temp3 = " + this.temp3);
        System.out.println("----------------------------------------------------------");
 
        System.out.println("使用super关键字,输出父类成员变量temp1 = " + super.temp1);
        System.out.println("使用super关键字,输出父类成员变量temp2 = " + super.temp2);
        System.out.println("使用super关键字,输出父类成员变量temp3 = " + super.temp3);
    }
}
public class j {

    public static void main(String[] args) {

        Son s1 = new Son();
        s1.printTemp();
    }
}
```
### 9.5 equals 方法
* ***equals方法是Object类中的方法***，上面再String类里面的equals就是对父类Object的覆盖
```java
class MyData {
    private int month;
    private int year;

    // 这里这两个属性虽然是private的，但是这并不代表新生成的对象实例不包含它们，只是没法直接通过调用属性的方法去修改
    // 这也是为什么底下的this点month和this点year是可以去直接修改，但是调用的却是真真实实的两个隐性的属性
    // 一般private也就是用来干这些，让使用者无法去直接通过方法或属性的去修改，但是可以通过内部函数，也就是写在类定义里面的语句去修改

    public MyData(int month,int year){
        // 构造方法
        this.month = month;
        this.year = year;
    }


    public boolean equals(Object obj) {
        // 方法重载必须完全跟父类的标识符命名一样，所以这里返回值也是布尔值并且接收的参数也得是一个object的类型而不是你自定义的
        if (obj instanceof MyData) {
            // isinstanceof操作符用来去判断是否是一个类型的对象
            MyData tmd = (MyData)obj;
            // 这里为什么要去新建一个mydata类型的对象去转换obj类型，而不是直接去obj访问
            // 这是因为一个很重要的特性就是父类的对象无法访问子类的对象的属性，除非这个父类有他子类所有的东西他都有
            if (tmd.year == year && tmd.month == month) {
                return true;
                // 确定二者相同之后返回true，反之亦然                
            }
        }

        return false;
    }
    
}

MyData md1 = new MyData(12,1994);
MyData md2 = new MyData(3,2003);
System.out.println(md1.equals(md2));

// 重写equals方法非常常见
```
### 9.6 包装类
* Java是一个面向对象的编程语言，但是Java中的八种基本数据类型却是不面向对象的，为了使用方便和解决这个不足，在设计类时为每个基本数据类型设计了一个对应的类进行代表，这样八种基本数据类型对应的类统称为***包装类 (Wrapper Class)***，包装类均位于java.lang包
* 包装类作为和基本数据类型对应的类的类型存在，***方便涉及到对象的操作***，包含每种基本数据类型的相关属性如最大值、最小值等，以及相关的操作方法
```java
boolean —> Boolean
char —> Character
byte —> Byte
short —> Short
long —> Long
int —> Integer
float —> Float
double —> Double
```
* ***装箱指的是基本类型转换为包装类，拆箱指的是包装类转换为基本类型，JDK5以后都是自动封拆箱*** (其实只是让你少写了一句话，编译器补上而已)
## 第十章：Java 内置常用类 (String、StringBuffer 和 Math)
### 10.1 String 字符串
#### 10.1.1 构造
* ***构造 String 类的对象的语法***
```java
String str = new String("HelloWorld");

// 或者

String str = "HelloWorld";

// 这个也叫字符串常量，区别如下
```
* 两种方式区别在于，***一个是使用 new 新建对象位于堆内 (不完全正确)，而直接赋值是在常量池中创建的一个字符串常量，而且两个相同名称的字符串常量指向同一段内存***，这是 Java 自动检查节省内存
```java
public class g {

    public static void main(String[] args) {
        String s1 = "hello";
        String s2 = "hello";

        if (s1 == s2) {
            System.out.println("常量池中的字符串常量指向同一段内存");
        }

        String s3 = new String("hello");
        String s4 = new String("hello");

        if (s3 != s4) {
            System.out.println("位于堆内的字符串对象不指向同一段内存");
        } else {
            System.out.println("位于堆内的字符串对象指向同一段内存");
        }

        if (s1 != s3) {
            System.out.println("常量池中的字符串不等于堆内的字符串");
        }
    }
}
```
* ***String类的对象一经构造，那么保存在对象中的字符串内容就终身不能被修改了***
#### 10.1.2 equals 方法
* ***使用 equals 方法把第二个字符串作为参数传递进去，会比较二者的内容是否相同***
```java
boolean equals(Object anObject) // yufa

// 欸他这个比较的是 Object 的类型呢，是因为他本来是 Object 的方法，在 String 里对他进行了一个覆盖

if (s1.equals(s3)) {
    System.out.println("s1 的内容等于 s3");
}
```
* equalsIgnoreCase 不考虑大小写比较
```java
boolean equalsIgnoreCase(String another)
// 这个是 String 自己的

String str1 = "abcd";
String str2 = "UVWX";

System.out.println(str1.equalsIgnoreCase(str2));

// 大写大于小写
```
#### 10.1.3 charAt 返回指定位的字符
```java
char charAt(int index)
// 返回 char 参数为数字索引从 0 开始

System.out.println(s1.charAt(0));
```
#### 10.1.4 compareTo 比较两个字符串
```java
int compareTo(String anotherString)
// 按照字母顺序比较两个字符串，

String str1 = "abcd";
String str2 = "uvwx";

System.out.println(str1.compareTo(str2));

// 结果为 -20，负数代表在自己的后面，正数反之，0 代表一样
// 返回值类似 C 中的，用处不大
```
* ***compareTolgnoreCase 会忽略大小写***
```java
System.out.println(str1.compareTo(str2));
System.out.println(str1.compareToIgnoreCase(str2));
```
#### 10.1.5 concat 连接字符串
```java
String concat(String str)
// 将字符串连接到此字符串的末尾

String str3 = str1.concat(str2);

// 他不修改字符串本身，你需要那一个新字符串接走
System.out.println(str3);
```
#### 10.1.6 indexOf 返回字符出现位置
```java
int indexOf(int ch,int fromIndex)
// 返回指定字符第一次出现的位置，参数可以直接用编码表示
// 第二个参数代表从第几位开始寻找，默认不写从 0 开始

System.out.println(str1.indexOf('c'));
```
* ***lastIndexOf 返回指定字符最后一次出现的位置***
```java
int lastIndexOf(int ch)
```
#### 10.1.7 length 返回字符串长度
```java
int length()

System.out.println(str1.length());
```
#### 10.1.8 replaca 替换字符
```java
String replace(char oldchar,char newChar)
// 替换字符串中的字符

String str4 = str2.replace('U', 'A');

System.out.println(str4);
```
#### 10.1.9 substring 提取字符串的部分内容作为子字符串
```java
String substring(int beginIndex,int endIndex)
// 第二个参数可以不写默认获取到末尾
// 末尾提取到几位，这个几位是不提取的，要头不要尾

int pos1 = str5.indexOf(',');
int pos2 = str5.indexOf('!',pos1);

String str6 = str5.substring(pos1 + 1, pos2);
System.out.println(str6);
```
#### 10.1.10 字符串连接
* 可以用加号直接连接字符串，***当一个纯加法运算中有一个字符串，那么这个加法运算就变成字符串连接了***
```java
String str7 =  1 + 2 + "hello" + 4 + 5;
System.out.println(str7);

// 从字符产出现位置开始连接，后面是 hello45
// 前面还是加法运算 3，跟后面的 hello45 连接所以结果是 3hello45
```
> 最后说一句话，String 一经创建永远不能改变：
```java
String str8 = "hello";
str8 = str8 + "world";
System.out.println(str8);

// 你看这个 str8 值变了，但其实只是指向了一个新的字符串位置，原来的访问不到了而已
```
### 10.2 String Buffer
* StringBuffer 类和 String 类最大的区别在于**它的内容和长度都是可以改变的。StringBuffer 类似一个字符容器**，当在其中添加或删除字符时，所操作的都是这个字符容器，因此并不会产生新的 StringBuffer 对象
#### 10.2.1 构造方法
* 也是使用 new 方法构造
```java
StringBuffer str_buf = new StringBuffer();
// 这是直接新建

StringBuffer str_buf = new StringBuffer(int capacity);
// 这样是规定一个容量大小，防止运行过慢                

StringBuffer str_buf = new StringBuffer("StringBuffer");
// 也可以直接使用
```
#### 10.2.2 内容扩充 
* **StringBuffer append() 方法扩充到字符串末尾**
```java
StringBuffer str_buf = new StringBuffer("My name is: ");
str_buf.append("Peter");

System.out.println(str_buf);

// 可以不停扩充，内容不断变化
```
#### 10.2.3 返回容量
* int capaticy() 返回当前对象的容量
```java
StringBuffer str_buf = new StringBuffer(1024);
str_buf.append("Peter");

System.out.println(str_buf);
System.out.println(str_buf.capacity());

// 即使容量大小规定出来也不会初始化为零，所以打印的还是你输入的
// 但是打印的大小就是
```
> 跟返回字符串长度不同，这个是返回容量大小
#### 10.2.4 返回指定位置
* char charAt(int index) 返回指定位置字符
```java
StringBuffer str_buf = new StringBuffer(1024);
str_buf.append("Peter");

System.out.println(str_buf.charAt(0));
```
#### 10.2.5 删除指定位置
* **StringBuffer delete(int start,int end) 删除指定位置间的字符**
```java
str_buf.delete(0,2);
System.out.println(str_buf);

// 也是从 0 开始算头不算尾
```
#### 10.2.6 插入
* String Buffer insert() 插入内容到指定的位置
```java
str_buf.insert(2, "none ad");
System.out.println(str_buf);

// 第一个参数为偏移量，第二个是内容
```
#### 10.2.7 顺序反转
* String reverse 让字符串内容反转
```java
str_buf.reverse();
System.out.println(str_buf);
```
#### 10.2.8 提取
* 跟 String 一样提取到子字符
### 10.3 Math
#### 10.3.1 属性
* 比如一些常数可以直接拿来用，静态属性直接拿来用
```java
System.out.println(Math.PI);
System.out.println(Math.E);
```
#### 10.3.2 常用方法
```java
static abs() // 返回参数的绝对值

System.out.println(Math.abs(-98));

// Math.abs(a)：取a的绝对值
// Math.sqrt(a)：取a的平方根
// Math.cbrt(a)：取a的立方根
// Math.max(a,b)：取a、b之间的最大值
// Math.min(a,b)：取a、b之间的最小值
// Math.pow(a,b)：取a的b平方

static double celi(double a) 
static double floor(double a)
static long round(double a)

// 这三个分别是进一法，舍弃法和四舍五入
// 但是注意是以 double 形式返回的

System.out.println(Math.round(10.64));


static double random() // 返回一个大于 0 小于 1 的随机数

for (int i = 0; i < 10; i++) {
    System.out.println(Math.random());
}

// 还可以控制输出范围

for (int i = 0; i < 100; i++) {
    System.out.println(Math.round(Math.random() * 10));
}

// 这是从 0 到 10 的随机数 
```
## 第十一章：包的定义与类路径
### 11.1 包的定义
* ***包 (package) 在 Java 中是为了解决类的命名冲突，方便管理类***，语法如下
```java
package <包名字>;

package com.domin;

public class Book {
    ...;
}
```
* ***包定义语句必须出现在 Java 源代码文件的第一个有效语句行***，一个文件只能定一个包，包定义后面的所有类就属于这个包
> 如果不定义包的类，属于**缺省包**
### 11.2 包的引用
* **当一个包中的类使用到其他包中的类的时候**，有以下解决方法：
    * **把包的名字直接使用**
    ```java
    // 引用 student 包

    package com.book;

    public class Book {
        public static void main(){
            com.domin.student stu1 = new com.domin.student();
        }
    }
    ```
    * ***使用 import 语句引入其他包***
    ```java
    package com.book;

    import com.domin;

    public class Book {
        public static void main(){
            Student stu1 = new Student();
        }
    }
    ```
    * **使用 .* 将这个包里的类全部引入**
    ```java
    import com.domin.*;

    // 这样做的时候想清楚可能会发生的冲突情况
    ```
* ***在 Java 文件里里有三种元素，package、import和类定义，这三种元素一定是先package再 import 最后类定义***
> Java **默认引入 java.lang**
```java
import java.lang.*;

// String 就在这里面
```
### 11.3 编译类时候的CLASSPATH
* ***一个编译好的类目标文件必须存放在与这个类的包一致的目录下***
```java
package com.domin;

public class Book {
    ...
}

// 编译完成后这个class文件必须存放在跟类名相同的目录下，也就是
// .../com/domin/Book.class 是他的存放路径
// 这个文件夹的父文件夹是谁无所谓
```
* 这个时候我们把 com ***这个文件夹的父文件夹称作 CLASSPATH*** (**com本身这个文件夹叫包路径而不是类路径**)
> 比如有一个目录结构如下：
```java
    D:/ -- FolderA -- com -- domin -- Book.class
        |                           |-Book.java
        |
        -- FolderB -- com -- app -- App.class
                                  |-App.java

// Book.java 
package com.domin;

public class Book {
    public void render() {
        System.out.println("Book.....");
    }
}

// App.java

package com.app;

import com.domin.Book;

public class App {
    public static void main(String args[]) {
        Book b = new Book();
        b.render();
    }
}

// cmd 里面在FolderB 里面的app文件夹执行，但是报错
// 因为默认是控制台的文件夹为 CLASSPATH ，但是里面根本就没有com文件夹和Book的class文件，所以编译器不知道你引入的是什么只能报错
// 不能理解的话请看如果想让编译通过的话你的文件结构应该是

    D:/ -- FolderB -- com -- app -- App.java
                                 |- com -- domin -- Book.java
                                                 |- Book.class
```
> 编译器寻找的是编译后的 class 文件而不是源代码
* ***指定编译器 CLASSPATH 的命令格式是***：
```java
javac -d <输出路径> -classpth <类路径> <源代码文件名>

// -classpath 可简写为 -cp

// 输出路径指的是编译后的文件放到哪里，并且你如果定义了包还会自动生成包对应的文件夹结构把class文件放进去
// 类路径指的是你要用到的类的类路径，记住不是包路径
// 比如上面的App的类路径是FolderB，Book的类路径是 D:/FolderB/com/app/

// 有多个类路径用分号隔开
```
> 题外话在前文下载与安装时讲过 CLASSPATH，你确实可以在环境变量里面提前约束类路径，但是官方已经不建议了，还是应该采用命令行 -classpath 参数的方式
### 11.4 运行时的 CLASSPATH
* ***定义了包的类运行时候的命令格式***：
```java
java -cp <类路径> <类全名 (包括包的名字)>

// 这个 -cp 后面的类路径是代码中要用到别的类的类路径，不是自己的
// 有多个用分号隔开来

// 例如在 D:/test 执行：

javac -d D:/test -classpath D:/test Book.java
javac -d D:/test -classpath D:/test App.java

// 会生成如下结构

D:/test
│  App.java
│  Book.java
│
└─com
    ├─app
    │      App.class
    │
    └─domin
            Book.class

// 在 D:/test/com/app 执行 java App 却显示找不到主类是因为 App.java 的全限定类名决定它在 /com/app 里面，但是 D:/test/com/app 里面并没有
// 正确应该在 D:/test 下面执行

java com.app.App
```
> ***全限定类名：包名+类名***，另外，当包名为空时（即代码不包含package语句），称类所在包为默认包，这是编译器确定代码的方式，这便是为何  
> 简而言之，**每个源代码编译时和运行时都要遵守类路径的分类，编译器和虚拟机都按照类路径的定义去寻找类**
## 第十二章：数组
* ***程序就是不断地输入输出数据，为了方便简洁易用，将数据以不同的形态存储在内存中，不同的数据结构读取其中的内容需要配合一定的算法，二者相辅相成***
> 这段话太好了
### 12.1 数组的定义
* ***数组是用于存放相同类型数据的一段连续内存空间***，数组是最简单的数据结构，好处是只要知道数组的首地址就可以遍历任何数据 (因为是连续的相同占用)
* 一维数组的定义与初始化
```java
<数据类型> [] <变量名> = new <数据类型>[数组长度];

// 也可以写成如下

<数据类型> <变量名> [] = new <数据类型>[数组长度];

int [] nums = new int[10];

// 也可以先声明是数组类型的变量，再确定数组长度

int nums [];
nums = new int[10];
```
* ***也可以使用花括号直接写有哪些数据***
```java
int nums [] = {2,3,4,5,6,7};

// 数组长度跟元素数量一致
// 这句话不能分开，也就是

int nums [];
nums = {1,2,3};

// 错误
```
* ***数组元素使用中括号加索引使用或修改***
```java
int nums [] = new int[10];

int[0] = 4;
int[1] = 89;
int[2] = 5;
```
> Java中除了基本类型外，***数组也是一个类，数组对象也是引用类型的对象，你声明一个数组就声明了一个类的对象***，这一点跟 C 里面的数组不一样
* 就因为数组也是类，***数组的初始化根据类型会默认初始化***，比如 int 会放 0，char 放 \0
### 12.2 数组的长度
* 首先，***数组对象一旦构造，其长度将不能改变***，因为连续内存空间是提前分配好的，***可以通过数组的属性length获得数组的长度***
```java
int [] nums;
nums = new int[10];

System.out.println(nums.length);
```
```java
// 利用length遍历数组

int [] nums_1 = {1,2,3,4,5};

for (int i = 0; i < nums_1.length; i++) {
    System.out.println(nums_1[i]);
}
```
* 如果实在想改变数组的长度，可以新建一个长数组，再循环一个一个赋值，这叫***模拟改变数组的长度。Java中提供了一个静态方法叫 Arraycopy***
```java
// 借助循环

int [] nums_1 = {1,2,3,4,5};

System.out.println("原来的数组是：");

for (int i = 0; i < nums_1.length; i++) {
    System.out.println(nums_1[i]);
}

int [] new_nums_1 = new int[10];

for (int i = 0; i < nums_1.length; i++) {
    new_nums_1[i] = nums_1[i];
}

System.out.println("拷贝完成");
System.out.println("新数组是：");

for (int i = 0; i < new_nums_1.length; i++) {
    System.out.println(new_nums_1[i]);
}
```
```java
System.arraycopy(src,srcPos,dest,destPos,length)
```
> 参数很多，**src是源数组对象，srcPos是从源数组第几个位置开始复制，dest是目标数组对象，destPos是从目标数组第几个位置开始赋值，length表示一共拷贝多少个元素**
```java
System.arraycopy(nums_1,0,new_nums_1,0,nums_1.length);

nums_1 = new_nums_1;

// 这里让原数组对象指向一个新地址，其实原来的数组长度并没有变，只是指向了新的数组
```
### 12.3 其他类型的数组
* ***数组也可以由其他数据类型组成***
```java
String [] str = new String[5];

str[0] = new String("abcd");
str[1] = "def";

// str是一个字符串，里面每一个元素都是一个String类的引用对象
```
```java
String ss[] = {new String("qwer"),new String("9896"),new String("dasdas")};
```
### 12.4 多维数组
* 多维数组的定义如下：
```java
int [][] nums = new int[2][3];

// 也就是nums是一个有两个元素，每一个元素都是一个有三个元素的数组的数组
// 当然也可以理解为行列
```
```java
int [][] headers = new int[2][];

headers[0] = new int[3];
headers[1] = new int[5];

// 这里headers其实是一个一维数组，只是每一个数组元素指向一个新的一维数组
// 二维数组每一个数组元素一定是一样大小的
```
* **Java里面的多维数组都是以数组之间互相引用的方式实现的**，有多少维度就有多少的互相引用
```java
int [][] headers = new int[2][];
headers[0] = new int[3];
headers[1] = new int[5];

for (int row = 0; row < headers.length; row++) {
    for (int col = 0; col < headers[row].length; col++) {
        System.out.print(headers[row][col] + ",");
    }
    System.out.println();
}

// 但是从结果上面看确实是像是长度不等的二维数组
```
## 第十三章：抽象类与接口
### 13.1 抽象类的概念与定义
* 当我们需要一个方法却不知道它的具体表现形式，只能知道它的具体实例怎样使用它，我们可以干脆不构造它，这个叫抽象方法
* 抽象类就是一个可以包含抽象方法的类，定义语法如下
```java
// 抽象类

<修饰符> abstract class <类名字> {
    ···
}

// 抽象方法

<修饰符> abstract <返回值类型> <方法名字>(参数列表);
// 没错没有方法体
```
* 抽象类既然不能被构造，所以***抽象类的继承就成了唯一使用途径***，抽象类的特点：
    * ***抽象类不能构造对象***，但是可以有构造方法，问题是只能由子类来构造
    * ***抽象类当中不一定有抽象方法，但是有抽象方法的类必须被申明为抽象类***
    * ***一个类继承抽象类，那么这个类中必须实现抽象类中所有的方法。如果没有，那么这个类也要声明为抽象类***，也就是子类实现了父类的抽象方法，也就是***父类成了规范***，子类必须要实现 (覆写) 父类的全部抽象方法，否则它自己也是抽象的没法实例化
    * ***抽象类不能被申明为 final 类型***的，否则又要继承又不能继承岂不自相矛盾
### 13.2 接口
> 接口就是抽象类的一种特殊表现形式
* ***接口就是一个完全抽象的抽象类***，这个 *类* 中的方法全是抽象方法，语法如下
```java
// 接口当中只能有抽象方法，不像抽象类还可以有方法

<修饰符> interface <接口名字> {
    <修饰符> <返回值类型> <方法名字>(参数列表);
}
```
* 接口的特性：
    * **接口不能构造对象**
    * ***接口可以继承其他接口，而且可以多继承***，你想接口如果继承了多个接口里面有相同的定义，但是他们都没有方法体，有什么冲突吗？
    ```java
    public interface RedBus extends Bus,Color {
        // 用逗号分隔
    }
    ```
    * ***接口中的方法和属性都是 public 的***，不写默认也是 public 的
    * **接口中的方法全是抽象方法**
    * ***接口中的属性全是 static final 的***，因为***接口不能有构造方法*** (抽象类还是类，所以抽象类可以有构造方法，你不写他也会自己加上你) ，所以**变量只能在默认初始化的地方给它初始化**
* 接口的应用：
    * **类可以实现接口** (一个类必须实现接口中所有的方法，如果没有，那么这个类必须是抽象类)，***使用 implements 关键字实现***
    ```java
    interface Bus {
        int id = 12;
        void turnLeft();
    }


    class redBus implements Bus {
        
        public void turnLeft(){
            System.out.println("I'm turning left!");
        }

        // 这里方法必须是 public 的因为接口就是 public 的
    }

    ```
    * ***一个类可以实现多个接口***
    * 一个接口类型的引用变量可以指向一个实现了该接口的类的对象
    ```java
    interface Bus {
        int id = 12;
        void turnLeft();
    }


    class redBus implements Bus {
        
        public void turnLeft(){
            System.out.println("I'm turning left!");
        }
    }


    public class k {
        public static void main(String[] args) {
            Bus b = new redBus();
            b.turnLeft();
        }
    }

    // 就像是一个父类的引用可以指向子类的对象
    // 这也不需要担心报错，因为子类的实现一定全实现了接口，所以调用一定是先调用类的
    ```
> 这一点也是 Java 骄傲的一点，代码可利用性高，不同代码耦合性好，不会出现改了一个类所有接口全挂掉
## 第十四章：内部类和匿名类
* 内部类从 JDK 1.1 后引入的概念，指的是在***类内部定义的类***
* ***内部类的分类*** (类似变量的分类)
### 14.1 成员内部类
* ***成员内部类***，定义在***类的内部与成员变量和方法并列的类***
```java
public class Outer {

    public class Inner {
        ···
    }

    ···
}
```
* 使用方法，***内部类想要制造对象必须拥有外部类的对象才能***，而且权限修饰符也有用，如果是private的也无法访问：
```java
Outer out1 = new Outer();
Outer.Inner inn1 = out1.new Inner();
Outer.Inner inn2 = out1.new Inner();


// 因为不是顶级声明，所以必须先造出外层的对象再造内部的，注意new方法是调用的方法，对象类型带点号但是构造不带，对象类型是类的类型而不是对象的
```
* ***内部类可以访问外部类的属性，包括私有成员 (内部没有同名覆盖的情况下)***
```java
    public class k {

    
    public int id;

    
    public void outerRender(){
        System.out.println("Hi i`m Outer class" + '\t' + id);
    }


    public class Innerk {
        // 这里如果 static 修饰的话也不能访问，因为定位不到外部类的对象
        
        // public int id;
        // 本地优先

        public void innerRender(){
            System.out.println("Hi i`m inner class!" + '\t' + id);
        }        
    }


    public static void main(String[] args) {
        
        k outerk = new k();
        outerk.id = 13;
        k.Innerk inn1 = outerk.new Innerk();

        // inn1.id = 24;
        inn1.innerRender();
    }

}

// 试着注释掉两行代码看看
```
* ***当内部类属性和外部类属性命名冲突时候可以用 类名 + this + 属性名称访问***
```java
public class k {

    
    private int id;
    // 私有属性也能访问
    
    public void outerRender(){
        System.out.println("Hi i`m Outer class" + '\t' + id);
    }


    public class Innerk {
        
        public int id;
        
        public void innerIdRender(int id){
            System.out.println(id); // 函数参数
            System.out.println(this.id); // 内部类属性
            System.out.println(k.this.id); // 外部类属性
        }


        public void innerRender(){
            System.out.println("Hi i`m inner class!" + '\t' + id);
        }        
    }


    public static void main(String[] args) {
        
        k outerk = new k();
        outerk.id = 13;
        k.Innerk inn1 = outerk.new Innerk();

        inn1.id = 24;
        inn1.innerIdRender(45);
    }

}
```
### 14.2 本地内部类
* ***指定义在方法内部的类，方法不运行无法使用类***
```java
public class Outer {
    public void render() {
        class Inner {
            ···

            // 这种类无法使用权限修饰符，因为方法不运行没法使用
        }
    }
}
```
```java
public class k {

    
    private int id;

    
    public void outerRender(){
        System.out.println("Hi i`m Outer class" + '\t' + id);
    }


    public class Innerk {
        
        public int id;
        
        public void innerIdRender(int id){
            System.out.println(id);
            System.out.println(this.id);
            System.out.println(k.this.id);
        }


        public void innerRender(){
            System.out.println("Hi i`m inner class!" + '\t' + id);
        }        
    }





    public static void main(String[] args) {
        
        k outerk = new k();
        outerk.id = 13;
        k.Innerk inn1 = outerk.new Innerk();

        inn1.id = 24;
        inn1.innerIdRender(45);

        App ap1 = new App();
        ap1.setId(90);
        ap1.function();
    }

}


class App {
    private int id;

    public void setId(int id) {
        this.id = id;
    }

    public int getId() {
        return id;
    }

    public void function(){

        class innerFunc {
            int id;
        
            void innerIdRender(int id){
                System.out.println(id);
                System.out.println(this.id);
                System.out.println(App.this.id);
            }
            
        }

        innerFunc inn2 = new innerFunc();
        inn2.id = 67;
        inn2.innerIdRender(89);
    }
}
```
> 这种方法内的内部类使用上面没有区别，也能访问到外部类的属性，内部没有权限修饰符。***只是必须在方法中使用，出栈以后就消失，除非当作 Object 返回值返回出来***，如果一些短小的代码可以用这样完成占内存少
* ***如果想在本地内部类使用本地变量，那么这个本地变量必须是常量***
```java
class App {
    private int id;
    final int iidd = 190;

    public void setId(int id) {
        this.id = id;
    }

    public int getId() {
        return id;
    }

    
    public void function(){
        class innerFunc {
            int id;
        
            void innerIdRender(int id){
                System.out.println(iidd);
                System.out.println(id);
                System.out.println(this.id);
                System.out.println(App.this.id);
            }
            
        }

        innerFunc inn2 = new innerFunc();
        inn2.id = 67;
        inn2.innerIdRender(89);
    }
}
```
### 14.3 静态内部类
* ***静态内部类只针对成员内部类***，只有成员内部类前面加上 static 才是静态内部类，***成员内部类就自动升级为顶级类***
* 这样就没必要需要一个外层的实例，直接用就行
```java
public class OuterClass {
    private static int staticField = 1;
    private int instanceField = 2;

    public static class InnerClass {
        public void print() {
            System.out.println("staticField = " + staticField);
            // System.out.println("instanceField = " + instanceField); 
            // 编译错误，因为不在静态区内
        }
    }

    public static void main(String[] args) {
        OuterClass.InnerClass inner = new OuterClass.InnerClass();
        // 注意静态内部类的创建语法不同于成员内部类，注意 new 和他后面的
        inner.print(); 
        // 输出 staticField = 1
    }
}
```
### 14.4 匿名类
* ***匿名类是一个没有名字的类，匿名类的定义与对象构造同时发生***
```java
IBlock block = new IBlock(){

    // 一般 new 是一个声明语句。而这里还加入了大括号
    // IBlock 是一个接口，这里 new 后面的是父类的调用，小括号里面是父类的构造方法

    public void method(){
        ···

        // 这里面的语句立马执行
    }
}; // 别忘了这个
```

```java
interface Test {
    public void render();
}

public class L {

    public void play(Test t2){
        
        // 参数是一个实现了 test 的类
        t2.render();
    }

    public static void main(String[] args) {
        
        L l1 = new L();
        l1.play(new Test(){
            // 一般匿名类用于这些地方，在参数里构造一个类
            public void render(){
                System.out.println("hello,render!");
            }
        }); // 看清楚哪一个有分号那一个没有

    }
}
```
## 第十五章：异常处理
### 15.1 异常的分类
```java
Throwble
// 所有异常类的父类叫 Throwble
   ↑   ↖
Error   Exception
// 错误和异常，错误是一种无法继续、无能为力的异常 (比如停电了，死机了)，异常是代码仍能够继续运行的异常
         ↗    ↖
        ···    RunTimeException
// Exception 和自己非 RunTime 的子类，都叫 Checked 异常
// RunTime 和自己的子类，都叫 RunTime 异常，运行时
                    ↖
                    ···
```
### 15.2 异常的捕捉
* ***try 语法***：

```java
try {
    可能产生异常的语句;
} catch(异常类型 引用变量名){
    // 将来引用类型的变量会指向一个异常类型
    处理异常的语句;
} catch(){
    ···
} finally {
    语句;
}
```

* ***try 后面，可以只有 catch，只有 finally，也可以都有***
* 如果 try 里面的语句发生了异常，则一个个向下寻找有没有定义相同异常的 catch ，有的话执行对应 catch 里面的语句，然后执行 finally；***如果没有一个 catch 捕捉到异常，则程序中断，但是是先执行 finally 再结束程序***
```java
public class l {
    public static void main(String[] args) {
        try {
        int n = 3;
        int infinity = n / 0;
        } finally {
            System.out.println("finally");
        }

        System.out.println("over");
    }
}

>>>finally
Exception in thread "main" java.lang.ArithmeticException: / by zero
// 这个 ArithmeticException 就是数学异常的类
        at l.main(l.java:8)

// 先打印的 finally ，然后才结束的程序
```
* 所以，***finally 只有两种情况下不会执行，一是错误，二就是如下使用了 exit 退出***
```java
public class l {
    public static void main(String[] args) {
        try {
        int n = 3;
        int infinity = n / 0;
        } catch(ArithmeticException e) {
            System.out.println("cant devide by 0!");
            System.exit(0);
        } finally {
            System.out.println("finally");
        }

        System.out.println("over");
    }
}
```
* java 里面所有异常都是 Exception 的子类，如果先捕捉 Exception 会怎样呢？
```java
public class l {
    public static void main(String[] args) {
        try {
        int n = 3;
        int infinity = n / 0;
        } catch(Exception e) {
            // ArithmeticException 也是 Exception 啊
            System.out.println("Exception");
        } catch(ArithmeticException e) {
            System.out.println("cant devide by 0!");
            System.exit(0);
        } finally {
            System.out.println("finally");
        }

        System.out.println("over");
    }
}

>>>错误: 已捕获到异常错误ArithmeticException
```
* 所以***不要把父类和子类的异常一块写，会导致子类的异常永远无法访问***，当然**反过来是可以的**
### 15.3 异常的抛出
* 抛出异常的语法：
```java
throw <异常类的对象>;
```

* **checked 异常和 runtime 异常的区别**：

```java
class Month {
    private int month;

    public void setMonth(int month) {
        if (month < 1 || month > 12) {
            throw new Exception("month is not correct");

            // 这里的异常，如果你不捕捉，JVM 不会编译，这是 checked 异常
        }
        this.month = month;
    }

    public int getMonth() {
        return month;
    }
    
}
public class l {
    public static void main(String[] args) {
        int n = 3;
        int infinity = n / 0;

        // 这里的异常，只有在运行时才会知道，所以你不捕捉也能编译

        System.out.println("over");
    }
}
```
* ***如果会发生 checkd 异常，要么使用 try 捕捉到 (是真正的拿 catch 捕捉到)，要么在方法定义中对抛出异常的声明***

```java
··· <方法名>(参数) throws <异常类型1>,<异常类型2>··· {
    // throws 有 s
    ···
}
```
* 还**可以在抛出的异常中带上描述**
```java
class Month {
    private int month;

    public void setMonth(int month) throws Exception{
        if (month < 1) {
            throw new Exception("month < 1");
        } else if(month > 12){
            throw new Exception("month > 12");
            // 这里输入的是 message，也就是 exception 的构造方法参数，exception 会把它留下来
        }
        this.month = month;
    }

    public int getMonth() {
        return month;
    }
    
}
public class l {
    public static void main(String[] args) {

        try {
            Month m1 = new Month();
            m1.setMonth(13);
            int n = 3;
            int infinity = n / 0;
        } catch(ArithmeticException e) {
            System.out.println("cant devide by 0!");
            System.exit(0);
        } catch(Exception e) {
            System.out.println(e.getMessage());
            // 调用异常类的getmMessage方法
        } finally {
            System.out.println("finally");
        }

        System.out.println("over");
    }
}
```
### 15.4 自定义异常
```java
class SmallMonthException extends Exception{
    public SmallMonthException(){

    }

    public SmallMonthException(String msg) {
        super(msg);
    }
}


class BigMonthException extends Exception{
    public BigMonthException(){

    }

    public BigMonthException(String msg) {
        super(msg);
    }
}



class Month {
    private int month;

    public void setMonth(int month) throws SmallMonthException,BigMonthException{
        if (month < 1) {
            throw new SmallMonthException("month < 1");
        } else if(month > 12){
            throw new BigMonthException("month > 12");
        }
        this.month = month;
    }

    public int getMonth() {
        return month;
    }
    
}



public class l {
    public static void main(String[] args) {

        try {
            Month m1 = new Month();
            m1.setMonth(798);
            int n = 3;
            int infinity = n / 0;
        } catch(ArithmeticException e) {
            System.out.println("cant devide by 0!");
            System.exit(0);
        } catch(SmallMonthException e){
            System.out.println(e.getMessage());
        } catch (BigMonthException e){
            System.out.println(e.getMessage());
        } catch (Exception e) {
            System.out.println("wrong");
        } finally {
            System.out.println("finally");
        }

        System.out.println("over");
    }
}
```
### 15.5 异常对重载与覆盖的影响
* ***异常对方法重载没有影响***
* 异常对于方法覆盖的影响如下：
    - ***runtime 异常对方法覆盖没有影响***，父类抛出异常，子类想抛抛，不抛也行
    - ***假设父类方法申明抛出了 A 类型的 checked 异常，那么如果子类方法覆盖时想要抛出 checked 异常，只能抛出 A 类型或 A 的子类类型的异常，但是不抛出任何 checkecd 异常是允许的***

    ```java
    class Fu {
    public void out() throws SmallMonthException {

        };
    }


    class Zi extends Fu{

        public void out() throws Exception {
            // 这是 A 的父类型，是不行的
        }
    }
    ```

## 第十六章：集合类
### 16.1 集合
* ***Java 中的集合实际是对常用数据结构的一种规范***
* Java 中的集合的分类与特点如下，集合的规范都是通过接口定义的，位于 java.util 包中
    * ***Collection***：Collection可以看作是父类，**是否有序、是否可以重复取决于实现**
    * ***Set***：**无序集合** (指取出来不一定按顺序的)，**不可以重复**
    * ***List***：**有序集合，可以重复**
    * ***Map***：***存放键值对，键不可以重复***
### 16.2 集合和API
```java
<interface> Collection
    +add(element:Object):Boolean    // 加
    +remove(element:Object):Boolean // 删去
    +size():int // 返回元素数量
    +isEmpty():Boolean  //判断是否为空
    +contains(element:Object):Boolean   // 判断某元素是否位于集合内
    +iterator():Iterator // 返回迭代器
        ↗           ↖
<interface> Set         <interface> List
        ↑                   +add(index:int,element:Object)   // 多了一个序列参数
    HashSet                 +remove(index:int):Object
                            +get(index:int):Object  // 获取第几位的
                            +set(index:int,element Object)  // 设置第几位的
                            +indexOf(element:Object):int    // 获取元素的位置
                            +listlterato():ListIterator // 专门浏览链表的迭代器
                                ↗           ↖
                            ArrayList       LinkedList
                            // 方便查找的数组     // 方便加减的链表
```
### 16.3 Set 的实例
```java
import java.util.*;

public class m {
    public static void main(String[] args) {
        Set set1 = new HashSet();
        set1.add("one");
        set1.add("2nd");
        set1.add(new Integer(3));
        set1.add(new Float(5.0));
        set1.add("2nd");
        // 因为字符串存储在常量池，所以这个不算是重复添加
        set1.add(new Integer(3));
        // 可是这个呢，hashset 判断元素一样不是靠equals方法，而是hashcode 方法，对于 Integer 的 hashcode 会返回整数数值，所以set会认为重复添加
            
        System.out.println(set1);
    }
    
}

// 这里面的东西肯会报警告，具体见后
```
> 更详细的哈希值
```java
// import java.util.*;
// 其实不写这一句话，系统也会自己去找，但是最好写上方便阅读
// 通配符 * 并不代表全部导入，而是仅导入用户需要的

class SetExample {
    int age;
    int num;
}


public class m {
    public static void main(String[] args) {
        SetExample set1 = new SetExample();
        set1.age = 99;
        set1.num = 99;


        SetExample set2 = new SetExample();
        set2.age = 99;
        set2.num = 99;

        System.out.println(set1 == set2);
        System.out.println(set1.hashCode() + "\t" + set2.hashCode());


    }
    
}

// Object类的hashCode.返回对象的内存地址经过处理后的结构，由于每个对象的内存地址都不一样，所以哈希码也不一样
// String 类的 hashcode，只要字符串内容一样，结果也一样
// Integer 类的 hashcode 比较的也是数值而不是类
```
### 16.4 迭代器
* ***迭代就是检索集合中每一个元素的过程***，有没有什么方法无论你是什么数据结构都可以用相同的方法来浏览呢？
* ***Set集合的迭代器 Iterator 是无序的***
* ***List 集合的迭代器 ListIterator 可以顺序或是逆序***
```java
// 迭代器可以记住自己浏览到了第几个

List list1 = new ArrayList();
list1.add("one");
list1.add("second");

Iterator elements = list1.iterator();

while (elements.hasNext()) {
    System.out.println(elements.next());
}
```
* Iterator 主要有三个方法，hasNext()，next()，remove()
> ***创建 Iterator 后，这时的指针其实指向的是第一个元素的上方，即指向一个空***

> 当***调用hasNext方法的时候，只是判断下一个元素的有无***，并不移动指针

> 当***调用next方法的时候，向下移动指针，并且返回指针指向的元素***，如果指针指向的内存中没有元素，会报异常

> ***remove方法删除的元素是指针指向的元素***。如果当前指针指向的内存中没有元素，那么会抛出异常
### 16.5 常用的集合类
* Set:
    * HashSet 使用哈希值算法，对于不同的元素给予下标存储
    * TreeSet 使用树状结构存放
* List:
    * ArrayList
    * LinkedList
    * Stack
    * Vector
* Map：
    * HashMap
    * Hashtable 具体区别见后
    * ***Properties***
* ***Properties类表示一组持久的属性***。 Properties可以保存到流中或从流中加载。 属性列表中的每个键及其对应的值都是一个字符串。
```java
// 读取环境

Properties pro = System.getProperties();

Enumeration ee = pro.propertyNames();

// 这是枚举器，propertyNames() 用来把 pro 中的所有键送出来

while (ee.hasMoreElements()) {  // hasMoreElements() 询问是否还有键
    String name = (String)ee.nextElement(); // 取出 key，同时把 object 变为 string
    String value = pro.getProperty(name);   // 通过 key 获得 value

    System.out.println(name + "\t" + value);
}

// properties 本身就是一个键值对
```
> 有一种思考，while 里面有两个String类型的变量一直被初始化，再声明，会不会影响资源，但是定义在外面就不影响了？
## 第十七章：输入输出
### 17.1 概念
* ***从一个源头上读取信息，将信息输出到一个目标上***
    * 键盘、鼠标、显示器、打印机、网络
* ***流行式的输入输出的特点： 像水流一样，先出来的不能后出来，出来的不能回去，顺序单一不可随意跳转***
### 17.2 File 类
* ***FiIe 类不是一个用于进行输入输出的工具类，它是用来表示文件或文件夹的类***
#### 17.2.1 File 类的构造与方法
* 构造方法：
    * File(File parent,String child)
    * File(String pathname)
    * File(String parent,String child)
* 常用方法：
    * boolean createNewFile()
    * boolean exists()
    * boolean isDirectory()
    * boolean isFile()
    * String [] List()
    * boolean mkdir()

```java
import java.io.*;
// 导入输入输出包


public class u {

    public static void main(String[] args) {
        try {
            File f1 = new File("D:\\test\\com\\test1.txt");
            // 因为反斜杠也代表转义，所以这里用两个
            // 构造完成这个实例并不会干什么，只是构造了

            f1.mkdir();
            // 这下它创建的就不是 txt 而是 test.txt 名称的文件夹了


            File f2 = new File("D:\\test\\com");
            File f3 = new File(f2,"test2.txt");
            File f4 = new File("D:\\test\\com","text3.txt");
            System.out.println("f3 create " + f3.createNewFile());
            System.out.println("f4 create " + f4.createNewFile());
            // 这下就会创建文件了，返回创建成功与否



            if (f1.exists()) {
                if (f1.isDirectory()) {
                    System.out.println("f1 is directory");                    
                } else {
                    System.out.println("f1 is a  file");
                }
            } else {
                System.out.println("f1 is not exists");
            }
            
        } catch(Exception e) {
            e.printStackTrace();
            // 相比 System.out.println(e);，这个会把更详细的信息打印上来

            // 为了防止读写文件时崩溃，所以这里使用异常捕捉
        }
    }
}
```
### 17.3 输入输出 API
||字节流|字符流|
|----|-----|-----|
|低级流|InputStream，OutputStream，FileInputStream，FileOutputStream|Reader，Writer， FileReader，FileWriter，InputStreamReader，OutputStreamWriter|
|高级流|ObjectInputStream，ObjectOutputStream，DataInputStream，DataOutputStream|BufferedReader，BufferedWriter，PrintWriter|
> ***字节流以字节 (byte,1) 为单位，字符流以字符 (char,2) 为单位***
### 17.4 流式输入输出过程
* ***目标 -> 低级流 -> 高级流***
```java
// 打印文件到屏幕上

import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;

public class u {
    public static void main(String[] args) {
        try {
            File f = new File("D:\\test\\App.java");

            FileReader fr = new FileReader(f);
            BufferedReader br = new BufferedReader(fr);

            String line = br.readLine();

            while (line != null) {
                System.out.println(line);

                line = br.readLine();
            }

            br.close();

            // 只需要关掉高级流就行
        } catch(Exception e) {
            System.out.println(e);
        }
    }
    
}
```

```java
// 从键盘上写入文件

try {
    InputStreamReader isr = new InputStreamReader(System.in);
    BufferedReader in = new BufferedReader(isr);

    FileWriter fw = new FileWriter("D:\\test\\com\\test.txt");
    PrintWriter out = new PrintWriter(fw);

    String line1 = in.readLine();
    while (line1 != null) {
        out.println(line1);

        line1 = in.readLine();
    }

    in.close();
    out.close();
} catch (Exception e) {
    System.out.println(e);
}
```
> 更多请见 API
## 第十九章：多线程基础
> 这章以后不会再更新
### 19.1 概念
* ***进程是操作系统中正在运行的的一个任务，现代的操作系统基本都可以多任务并行***，这就像是一个程序，你可以随意切换程序
* ***线程是进程中的一个独立立运行的任务，进程中的线程可以并行***
* ***进程拥有自己独立立的内存地址空间等资源，一个进程中的所有线程共享进程的内存地址空间等资源***
> 注意，不要考虑多核心，现在只假设单核心 CPU ，CPU 通过不断地切换进城同时运行多个任务
* 并行和并发都是同一时间运行多个任务，***并发 (Concurrent) 是逻辑上同时运行，但由于 CPU 的速度快，在感知上像是所有的任务都在同一时间运行着，实际上是依靠调度器切换来切换去的运行***
* ***并行 (Parallel) 是物理上的同时运行，比如多核心 CPU 每一个核心运行着不同的任务***，但是由于这一章只讲述多线程***所以下文语义中的并行可能也指并发***
* ***线程是CPU调度和分配的基本单位，进程是操作系统进行资源分配 (包括cpu、内存、磁盘IO等) 的最小单位***，CPU 是看不到其他的进程的，只有操作系统才能看到
### 19.2 线程的创建与运行
#### 19.2.1 Thread
* 通过继承 Thread 类来定义线程，***当一个类继承 Thread ，它的 run 方法里面就是线程独立时要干的事，通过这个类创建一个实例就创建了一个线程***
```java
class MyThread extends Thread {
    public void run() {
        super.run();

        for (int i = 0; i < 9; i++) {
            System.out.println(i);
        }
    }
}

public class v {
    public static void main(String[] args) {
        MyThread mt1 = new MyThread();
        mt1.run();

        MyThread mt2 = new MyThread();
        mt2.run();
    }
}

// 打印结果并不是我们想的并行运行，只是一个打印完打印另一个
```
* Thraed 的实例***使用 start 方法，就可以让俩个线程同时运行，但是谁先谁后你不能决定***
```java
class MyThread extends Thread {
    public void run() {
        super.run();

        for (int i = 0; i < 9; i++) {
            System.out.println(i);
        }
    }
}

public class v {
    public static void main(String[] args) {
        MyThread mt1 = new MyThread();
        mt1.start();
        // 这条线程启动后，下一个立马就启动了

        MyThread mt2 = new MyThread();
        mt2.start();
    }
}

```
* 使用 sleep 方法，可以选择线程的休息时间
```java
class MyThread extends Thread {
    public void run() {

        for (int i = 0; i < 9; i++) {
            System.out.println(i);
            try {
                Thread.sleep(500);                
            } catch (Exception e) {
            }

            // 注意要使用 try 捕获，sleep 单位为毫秒
        }
    }
}
```
#### 19.2.1 Runnable
* ***通过实现 Runnable 接口***，runnable 就一个方法叫 run，
```java
class MyThread1 implements Runnable {
    public void run() {

        for (int i = 0; i < 9; i++) {
            System.out.println(i);
            try {
                Thread.sleep(500);                
            } catch (Exception e) {
            }
        }
    }
}


public class v {
    public static void main(String[] args) {
        MyThread1 mt1 = new MyThread1();
        // 你只是写了一个实例，但是他不具备线程的特点，它只是一个任务
        Thread t1 = new Thread(mt1);
        // 所以可以通过 Thread 创建一个实例，把 Runnable 的实现实例作为构造传进去

        MyThread1 mt2 = new MyThread1();
        Thread t2 = new Thread(mt1);
        t2.start();

    }
}

```
* 因为一个类可以实现多个接口，但是一个类只能单继承，所以***鼓励使用实现 runnable 接口来实现多线程***
### 19.3 线程的状态
```java
            ←       ←
            ↓        ↑
start() -> 准备 -> 运行 -> 死亡
            ↑        ↓
            ←   ← 等待 .sleep

// 准备时候等的是操作系统的调度，不是虚拟机
// 运行时如果遇到了 sleep，它进入了等待状态，等完后它会回到准备状态，等待调度
// 运行完后，它进入死亡状态，死亡的线程永远不能复活
```
```java
MyThread1 mt1 = new MyThread1();
Thread t1 = new Thread(mt1);
t1.start();


MyThread1 mt2 = new MyThread1();
Thread t2 = new Thread(mt2);
t2.start();

try {
    Thread.sleep(8000);
    // Thread 的 sleep 控制的是自己的睡眠时间，如果在 run 里面那就是每一个类的实例的 Thread 实例，在 main 里面就是主线程的
} catch (Exception e) {
}
// 这里等上 8 秒，等完后肯定 t1 就死了，还能调度吗

t1.start();

// 不行
```
* 常用的线程控制方法：
    * ***start() 开始现场至准备状态***
    * ***sleep() 运行时至等待状态***
    * ***interrupt() 等待时切换至准备时***
        ````java
        class MyThread1 implements Runnable {
            public void run() {

                try {
                    Thread.sleep(8000);                
                } catch (Exception e) {
                }

                for (int i = 0; i < 9; i++) {
                    System.out.println("t1\t" + i);
                    
                }
            }
        }

        class MyThread2 implements Runnable {
            public void run() {

                try {
                    Thread.sleep(8000);                
                } catch (Exception e) {
                }

                for (int i = 0; i < 9; i++) {
                    System.out.println("t2\t" + i);
                    
                }
            }
        }

        MyThread1 mt1 = new MyThread1();
        Thread t1 = new Thread(mt1);
        t1.start();

        
        MyThread2 mt2 = new MyThread2();
        Thread t2 = new Thread(mt2);
        t2.start();


        t2.interrupt();
        ```
* ***join() 等待一条线程结束后才执行自己的***，哪个实例调用的此方法，该实例就优先于 join 语句所在的线程优先执行
* ***yield()，哪个线程执行 yield 后就转换至准备状态，让步***，如果系统还是调用自己那没办法
### 19.4 线程的优先级
* ***操作系统会优先调用优先级高的，等级相同随机调用***
* ***线程的最低优先级为 1 (Thread.MIN_PRIORITY) ，线程的最高优先级是 10 (Thread,MAX_PRIORITY)，默认缺省优先级是 5 (Thread.NORM_PRIORITY)***
* ***通过 setPriority(int) 方法设置线程优先级，通过 getPriority(int) 来获取线程的优先级***
### 19.5 线程同步
#### 19.5.1 概念
* ***两条线程运行时需要互相根据对方的运行进度协调自身速度***
* 线程同步的表现：***一条线程依赖于另一条线程的时候，两者之间能够保持同步***
#### 19.5.2 控制线程同步
##### 19.5.2.1 synchronized
* ***使用 synchronized 修饰的方法，在被多个线程调用该类该方法时，只能有一个线程运行，等待着一个运行完后才能下一个***
> 被 synchronized 修饰的方法被第一个线程调用时，他会加上一个锁标记，这样每一条线程调用该方法时都想加标记，但是锁只能加一次，所以其他线程进入等待状态
```java
public class Test {
    public synchronized void render(){
        System.out.println("test");
    }
}
```
* ***synchronized 还可以对某一个程序段进行控制***
```java
public class Test {
    public void render(){
        System.out.println("test");
        
        synchronized(this) {
        // 括号里面是一个对象，this 表示该对象
        // 1
        // 2
        // 3
        }
    }
}
```
##### 19.5.2.2 wait()，notify()，notifyAll()
* ***这三个都是 Object 类的方法，如果一条线程在执行一个实例的过程中遇到了 wait ，它会释放自己的 synchronized 锁，加入等待队列；当你调用了另一条线程的 notify 方法，它会在所有调用过 wait 方法的线程中随机唤醒一个；当你调用了 notifyAll 方法，所有 wait 的线程统统唤醒***
> 这三个方法用在有 synchronized 的方法里面，不然也没用

> 邮递员和收信员，收信箱只能有一封信
```java
class MailBox {
    private String message;
    private boolean hasMessage = false;

    // 7. 在邮箱类里面，有现在的 message 和邮箱里面是否有信件 (应该叫当前的信件是否被取走了) 两个属性

    public synchronized void setMessage(String message) {

    // 8. 为了防止三位同时调用放信方法，所以加上锁，只有一位线程能够调用

        while (hasMessage) {
    
    // 9. 如果有信 (或者当前的信还没取走) ，则该线程等待其他线程放信

            try {
                wait();
            } catch (Exception e) {

            }
    // 请注意 wait 是需要捕获的
        } 
        
        this.message = message;
        hasMessage = true;
    
    // 10. 如果没有信了，则自己放信，同时叫醒其他人

        try {
            notifyAll();
        } catch (Exception e) {
            
        }
    }

    public synchronized String getMessage() {

        while (!hasMessage) {

    // 11. 同理，只不过判断是否没信，没信就等

            try {
                wait();
            } catch (Exception e) {

            }
        }

        String oldMessage = message;
        hasMessage = false;

    // 12. 因为 return 语句必须在最后一位，所以为了防止在把 hasMessage 设为 false 后 message 被取走，设置一个中转变量
        try {
            notifyAll();
        } catch (Exception e) {

        }

        return oldMessage;
    }
}



class PostMan implements Runnable {
    // 1. Postman 类实现 Runnable 接口，三个私有属性：邮递员姓名、手上的信封、邮箱

    private String name;
    private String [] messages;
    private MailBox mailBox;

    public PostMan(String name,String [] messages,MailBox mailBox) {
        this.name = name;
        this.messages = messages;
        this.mailBox = mailBox;
    }

    // 2. 构造方法

    public void run() {
        for (int i = 0; i < messages.length; i++) {
            mailBox.setMessage(messages[i]);
        }
    }

    // 3. 把自己的信都放入信箱

    public void start() {
        Thread t = new Thread(this);
        t.start();
    }

    // 4. 在这里直接定义 start 方法，其实也是调用的 Thread
}



class Receiver implements Runnable {
    private String name;
    private MailBox mailBox;

    public Receiver(String name,MailBox mailBox) {
        this.name = name;
        this.mailBox = mailBox;
    }

    public void run() {
        while (true) {
            String msg = mailBox.getMessage();
            System.out.println(name + "got <" + msg + ">");
        }        
    }

    // 5. 同理，不停循环拿去信件

    public void start() {
        Thread t = new Thread(this);
        t.setDeamon(true);
        t.start();
    }
}



public class v {

    public static void main(String[] args) {
        MailBox mailBox = new MailBox();

        String [] msg1 = {"111","222","333"};
        String [] msg2 = {"444","555","666"};
        String [] msg3 = {"777","888","999"};

        PostMan ps1 = new PostMan("ps1", msg1, mailBox);
        PostMan ps2 = new PostMan("ps2", msg2, mailBox);
        PostMan ps3 = new PostMan("ps3", msg3, mailBox);

        Receiver rc1 = new Receiver("rs1", mailBox);
        Receiver rc2 = new Receiver("rs2", mailBox);
        Receiver rc3 = new Receiver("rs3", mailBox);


        ps1.start();
        ps2.start();
        ps3.start();

        rc1.start();
        rc2.start();
        rc3.start();

        // 6. main 函数，我们只定义了一个信箱，六位寄信人和收信人拿到的都是同一个信箱在内存中的地址
    }
}
```
* 但是收信员不能随着寄信人的结束而结束，所以需要***一个可以随着其他线程的结束而结束的线程，也就是守护线程***
```java
Thread t = new Thread(this);
t.setDaemon(true);
t.start();
```
* 为了防止两个人同时对一个变量进行修改，这里加上
```java


class MailBox {
    private String message;
    private boolean hasMessage = false;

    public synchronized void setMessage(String message) {

        while (hasMessage) {
            try {
                wait();
            } catch (Exception e) {

            }
        } 
        
        synchronized(this) {
            this.message = message;
            hasMessage = true;
        }

        try {
            notifyAll();
        } catch (Exception e) {
            
        }
    }

    public synchronized String getMessage() {

        while (!hasMessage) {
            try {
                wait();
            } catch (Exception e) {

            }
        }
        
        String oldMessage = message;
        synchronized(this) {
            hasMessage = false;
        }

        try {
            notifyAll();
        } catch (Exception e) {

        }

        return oldMessage;
    }
}



class PostMan implements Runnable {
    private String name;
    private String [] messages;
    private MailBox mailBox;

    public PostMan(String name,String [] messages,MailBox mailBox) {
        this.name = name;
        this.messages = messages;
        this.mailBox = mailBox;
    }

    public void run() {
        for (int i = 0; i < messages.length; i++) {
            mailBox.setMessage(messages[i]);
        }
    }

    public void start() {
        Thread t = new Thread(this);
        t.start();
    }
}



class Receiver implements Runnable {
    private String name;
    private MailBox mailBox;

    public Receiver(String name,MailBox mailBox) {
        this.name = name;
        this.mailBox = mailBox;
    }

    public void run() {
        while (true) {
            String msg = mailBox.getMessage();
            System.out.println(name + "got <" + msg + ">");
        }        
    }

    public void start() {
        Thread t = new Thread(this);
        t.setDaemon(true);
        t.start();
    }
}



public class v {

    public static void main(String[] args) {
        MailBox mailBox = new MailBox();

        String [] msg1 = {"111","222","333"};
        String [] msg2 = {"444","555","666"};
        String [] msg3 = {"777","888","999"};

        PostMan ps1 = new PostMan("ps1", msg1, mailBox);
        PostMan ps2 = new PostMan("ps2", msg2, mailBox);
        PostMan ps3 = new PostMan("ps3", msg3, mailBox);

        Receiver rc1 = new Receiver("rs1", mailBox);
        Receiver rc2 = new Receiver("rs2", mailBox);
        Receiver rc3 = new Receiver("rs3", mailBox);


        ps1.start();
        ps2.start();
        ps3.start();

        rc1.start();
        rc2.start();
        rc3.start();
    }
}
```
##### 19.5.2.3 线程死锁
* ***如果两个线程同时想要别的资源，可是自己锁着别人的资源，自己又不释放，所以同步控制时请杜绝线程死锁***
## 第二十章：断言、枚举和泛型
### 20.1 断言
* 断言语法：
```java
assert <布尔表达式>;

// assert 是判断后面的布尔表达式是 true 还是 false
// 如果布尔表达式的值为 false，将抛出 AssertionError 异常 (这是个错误)
// 但是如果你想要 assert 工作，你必须在运行时加条件

assert <布尔表达式>:<表达式>;

// 这个会把后面表达式的值转为字符串打印出来
```
* 运行带有 assert 的文件时，请在 java 后面加上
```java
java -ea MyClass
java -enableassertions MYyClass
```
* 断言的推荐使用时刻
    * ***内在不变式***：如果这个地方本不能接受其他类型，但是这种情况发生概率极低，所以为了一般运行时的效率可以使用断言，等真的出现了问题再使用断言排查问题
    * ***控制流程不变式***：一般情况下的流程已经确定，但是为了防止流程的突变
    * ***后置条件和类的不变式***：对于条件的结果，可以不检查是否符合条件
    * ***不推荐用于共有方法的前置条件检查***
### 20.2 枚举
* 枚举的定义语法
> 建议看下 C 的枚举
```java
public enum BookType {
    BT_ENGLISH,BT_CHINESE;
}

Book b = new Book();
b.type = BookType.BT_ENGLISH;

// 枚举其实就是一个类，它里面也可以有方法
// 枚举不能构造对象，或者说BT_ENGLISH,BT_CHINESE就是他的对象
// 枚举的对象是作为静态常量存在的，你可以直接调用它

public enum BookType {
    BT_ENGLISH,BT_CHINESE;

    public void render(){
        System.out.print("BT");
    }
}

BookType.BT_ENGLISH.render();
```
* ***枚举的构造方法与重载***
```java
enum BookType {
    BT_ENGLISH(1),BT_CHINESE(4);

    public void render(){
        System.out.print("BT");
    }

    BookType(int i) {
        // 枚举不能构造对象，所以枚举的构造方法不能是 public
        // 枚举的构造参数取决于上面的BT_ENGLISH,BT_CHINESE有没有参数，有的话就有参数
        // 
    }

    Booktype() {
        // 无参构造
    }

    public void render(int i){
        System.out.print("BT" + i);

        // 方法重载
    }
}
```
* ***枚举的方法覆盖***
```java
enum BookType {
    BT_ENGLISH,BT_CHINESE(5) {
        // 基于匿名类的方法覆盖，其实语法就是一样的
        public void render() {
            System.out.println("Chinese");
        }
    };

    public void render(){
        System.out.print("BT");
    }

    BookType() {

    }

    BookType(int i) {
        
    }
}
```
* ***枚举前面只能是 public 或者不写，枚举也可以定义在内部***
### 20.3 泛型
> 如果我有一个数组，但是我不知道我里面要放哪些数据
* ***泛型可以把类型的决定留到运行时***，可以不用写一堆 Object：
```java
public MyClass<T> {
    public void add(T t) {

    }

    public T get(int index) {
        return ;// ···
    }
}

MyClass<String> book = new MyClss<String>();
books.add("str");
books.get(0);
```
* 也可以有***多个泛型***
```java
public MyClass<T,W> {
    public void add(T t) {

    }

    public void put(W w) {

    }
    public T get(int index) {
        return ;// ···
    }
}
```
* 如果你在***使用泛型的时候不指定 (比如前面的集合)，它默认就是 Object 类型***
* jdk 还可以利用泛型对数的包装类自动转换
```java
Integer i = 3;
int k = i;
// int k = i.intValue;

// 自动拆装箱
```

> 感谢收看
