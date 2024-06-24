# Kotlin 入门

> 说在前面：

> 本文是面向零基础用户进行讲解 (但最好看过 Java 或 C 哪怕一点，简单入门后再来看这篇，简单 10 倍)，我也不会以特别简单的语气讲，有些地方是假设你已经知道了类和函数的知识了的

> 有一些在引用块里面 (就像这样) 的小提示可能需要下文的知识，请多多回顾


## 第一章：认识 Kotlin

### 1.1 简介

- Kotlin 是由著名的 ***Jet Brains 公司开发***，融入了他们对于 Java 语言的改进与想法。***Kotlin 继承了 Java 的优点的同时还拥有了一些高级语言的新功能***，最重要的是 Kotlin ***对于安卓开发有着重要的作用***，所以文章后面会专门有一章讲述安卓开发，同时也会有**跨平台图形界面**的内容，笔者与大家一块学习

### 1.2 安装

1. 在 Github 上面的 [Kotlin](https://github.com/JetBrains/kotlin/releases) 编译器仓库下载最新版，Kotlin 基于 Java，所以你必须要有 [JDK](https://learn.microsoft.com/zh-cn/java/openjdk/download) 才行

2. **把 JDK 添加到环境变量** (Windows 打开图形界面，Linux 打开 /etc/profile) ，添加
    - *JAVA_HOME* = jdk/ 到用户变量
    - **%JAVA_HOME%\bin** 到 Path
    - **%JAVA_HOME%\jre\bin** 到 Path

3. **把 kotlin\bin 添加到环境变量**

4. 打开命令行，输入

```kt
java -version

javac -version

kotlic -version

// 是 kotlinc ，有 c 是编译器的意思

kotlinc 

// 这样会进入 Kotlin 的即时命令行编译
```

5. 因为这是 JatBrains 的语言，所以建议使用 [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) (其他的IDE使用体验均不如它) 来开发，或者 [VSCode](https://code.visualstudio.com/) 免费开源，在或是 Notepad++

> 如果使用 VSCode 一定要找一个好用一点的插件，体验还是不如 IntelliJ ，这是我目前用的[插件](https://marketplace.visualstudio.com/items?itemName=mathiasfrohlich.Kotlin)


## 第二章：简述

### 2.1 Hello World！

```kt
fun main() {
    println("Hello World!")
}
```

- 这是 Kotlin 里面 Hello World 的写法，确实***相比 Java 来说简洁很多***，而且像是**函数式编程**

- 首先，***fun 用于声明一个函数，main 函数式程序的入口***，在函数章之前所有的语句都发生在 main 里面，**函数的正文写在大括号里面**

> 见过 def、func 和函数类型开头的，没见过用 fun 声明的

> 在函数章以前，所有的代码都发生在 main 函数里面，所以会省略 main 不写望周知

- ***println 用于打印字符串并换行，还有print 函数打印却不换行***

```kt
fun main() {
    print("Hello ")
    print("World!")
}
```

> 你也看到了，***Kotlin 不需要分号结尾，但是可以使用 `;` 来分割处在同一行的语句，因此请注意代码规范格式***

```kt
val num: Int ; num = 10
```

### 2.2 编译运行

- ***Kotlin 文件以 kt 为结尾***，下面是**编译运行的过程**

```kt
kotlinc hello.kt

// 生成 HelloKt.class ，再使用 jvm 运行

kotlin HelloKt

// 我不知道为啥单词开头就大写了
```

- 也可以包含 Kotlin 的运行时**生成一个 jar 文件**，然后使用 JVM 来运行

```kt
kotlinc hello.kt -include-runtime -d hello.jar

java -jar hello.jar
```

> 如果对 jar 命令不熟，可以参见[这篇文章](https://blog.csdn.net/lcczpp/article/details/130854591)

- 当然你也可以直接使用 JVM 来运行 Kotlin 生成的 class 文件，当前还不会报错，下面会讲，完全不推荐

```
kotlinc hello.kt

java HelloKt
```

### 2.3 注释

- ***注释不会被编译***，因此可以用来编写注解一类的话。与 Java 一样，***Kotlin 支持普通注释和类注释***

```kt
// 这是单行注释


/**
    这是
    多行注释
*/


/**
 * 类注释
 *
 * 每一行开头的 * 不会认作是注释的一部分
 *
 * 块标签以 @ 从新的一行开始
 * 
 * @return 返回 Int
 */
```

> 块标签可以在[官方说明](https://book.kotlincn.net/text/kotlin-doc.html)里看到有哪些

- Kotlin 的***注释甚至可以嵌套***，下面的是=是不会报错的

```kt
/**
 * hhhh
 * /**
 *  fff
 *  /**
 *    ggggg
 *  */
 * */
 *
 * abc
 *
*/
```


## 第三章：变量与*基本类型*

> 与所有的编程语言一样，变量很好基本类型是最重要也是最基础的一章

### 3.1 变量的声明

- Kotlin ***使用 val 和 var 声明一个变量***

```kt
fun main() {
    val greetings = "Hello World"
    println(greetings)

    var greet = "Hello"
    print(greet)
    greet = " World"
    print(greet)
}
```

- ***val (value) 声明的变量不可变，var (variable) 声明的变量可变***，建议优先使用 val 去声明变量，***赋值运算符是 `=` 等号***，表示把右边的值赋给左面的变量

> Kotlin 是一门***一切皆对象*** 的语言，所以 Kotlin 的变量都是对象，它也***没有基本类型***，所以这也是这一章开头基本类型是斜体的原因

> 你甚至可以*对变量调用方法和属性*，见下文

- ***变量的类型写在变量名和冒号的右边***

```kt
val i:Int = 12

// 加上一个空格更美观

val i: Int = 12
```

- 还有一句话，***在 Kotlin 里所有的变量类型都没有默认值，在使用前必须初始化，否则编译器会报错***，无论是成员变量还是本地变量

### 3.2 标识符

- 变量、函数、类的名字叫标识符，Kotlin 的标识符命名规定与 Java 相同：
    1. 标识符可以***由字母、数字、下划线_ 组成***
    2. 标识符***不能以数字开头***
    3. ***区分大小写***，因此 myvar 和 MyVar 是两个不同的标识符
    4. **不可以使用关键字和保留字作为标识符**，但标识符中能包含关键字和保留字
    5. 标识符**不能包含空格**

    > [官网文档](https://book.kotlincn.net/text/keyword-reference.html)上有 Kotlin 的关键字列表，Kotlin 还有一类软关键字可以在特定的位置里面充当标识符，不过你肯定不会用这些名字来当变量名，所以不提
    
### 3.3 类型推断

> 上文可以看到，笔者并没有指定 greeting 和 greet 的类型，这是因为 Kotlin 具有类型推断

```kt
var num: Int = 10

// 等于

var num = 10
```
- 如果你***在声明变量的时候就初始化，那么可以省略变量的类型不写***

- 但是***Kotlin 是一门强类型、静态隐式语言***，所以下面的不可以

```kt
var num = 10
num = 9.2

// 报错
```

> 弱类型语言在运行时会隐式做数据类型转换  
> 强类型语言在运行时会确保不会发生未经明确转换 (显式调用) 的类型转换

> 静态类型检查是基于编译器来分析源码本身来确保类型安全  
> 动态类型语言是在运行时期进行类型标记的检查

> 显式类型语言需要在定义变量时显式给出变量的类型  
> 隐式类型语言可以使用类型推论来确定变量的类型  

- ***如果先声明变量但是没有初始化，就只能手动指定类型了***

> ***初始化是指变量第一次赋值的时候***，变量是可以二次赋值的，即使是常量也可以先声明再赋值 (在当前的情况下，下文中就不会了)

### 3.4 基本数据类型

#### 3.4.1 数字 ( Numbers )

##### 3.4.1.1 整数

- ***Kotlin 的整数有 `Byte`、`Short`、`Int`、`Long` 这四类***，注意他们不是 Java 的小写 int ··· 等基本类，也不是 Java 的 Integer 等包装类，是 Kotlin 自己的

|类型|大小 (比特数)|最小值|最大值|
|---|---|---|---|
|Byte|8|-128|127|
|Short|16|-32768|32767|
|Int|32|-2,147,483,648 (-2^31)|2,147,483,647 (2^31- 1)|
|Long|64|-9,223,372,036,854,775,808 (-2^63)|9,223,372,036,854,775,807 (2^63- 1)|

> 再说一遍，***一字节等于八位，1 byte = 8 bit，1 B = 8 b***

> 这里基本上与 Java 无异，负值到 128 而正值到了 127 是因为有 0

- ***如果你不指定整数的类型，默认是 Int ，超出 Int 则为 Long***，如果要***显式指定 Long 值要在字面量的后面加上 `L`***

> 不能小写 l

> 显式指定类型会触发编译器检测该值是否超出指定类型的表示范围
```kt
val one = 1 // Int
val threeBillion = 3000000000 // Long
val oneLong = 1L // Long
val oneByte: Byte = 1
```

##### 3.4.1.2 无符号整型

- ***Kotlin 还加入了无符号整型***

|类型|大小 (比特数)|最小值|最大值|
|---|---|---|---|
|UByte|8|0|255|
|UShort|16|0|65,535|
|UInt|32|0|4,294,967,295 (2^32-1)|
|ULong|64|0|18,446,744,073,709,551,615 (2^64-1)|

> 为了方便使用，你也可以***在无符号变量的字面量后面加上后缀 `u`、`U` 或 `ul`、`UL`***，这样就不用显示转换了

> 同理，***无符号整型的类型推断也是以 UInt 优先***

```kt
// 手动指定
val b: UByte = 1u
val s: UShort = 1u
val l: ULong = 1u

// 自动推断
val a1 = 42u // UInt
val a2 = 100000000000u // ULong
```

##### 3.4.1.3 浮点数

- Kotlin 提供了基于 IEEE-754 的两种浮点数，***Float(单精度) 和 Double(双精度)***

|类型|大小 (比特数)|有效数字比特数|指数比特数|十进制位数|
|---|---|---|---|---|
|Float|32|24|8|6-7|
|Double|64|53|11|15-16|

- ***使用带有小数部分的字面量来初始化浮点数变量***，小数点后面的部分视为小数位，***默认为 Double 类型，若要指定 Float 请在字面量后加上 `F` 或 `f` 后缀***

```kt
val pi = 3.14 // Double
// val one: Double = 1 // 错误：类型不匹配
val oneDouble = 1.0 // Double

val e = 2.7182818284 // Double
val eFloat = 2.7182818284f // 小数部分包含多于 6～7 位数，那么会将其舍入Float，实际值为 2.7182817
```

##### 3.4.1.4 数字字面量

> 字面量就是变量右边的值部分

- ***Kotlin 只有十进制、十六进制和二进制三种数字字面量***
    - 十进制 (DEC)：123、123L (Long)
    - 十六进制 (HEX)：0x0F
    - 二进制 (BIN)：0010 1101

- 浮点数字面量：
    - 默认 Double：12.3、3.14159
    - Float 用 f 或 F 标记：1.23F、3.14159f

- 无符号整型字面量：
    - u、U：默认UInt
    - uL、UL：ULong

- ***可以使用下划线 `_` 使整数更易读。也可以用科学计数法使浮点数更易读***

```kt
val num: Int = 1_000_000_000    // 好像四个一位也无妨

val d1 = 3.14e-3
println(d1)

val d2 = 3.14e+3
println(d2)
```
##### 3.4.1.5 JVM 的存储方式

- ***在 JVM 平台数字存储为原生类型 int、 double 等。 例外情况是当创建可空数字引用如 Int? 或者使用泛型时， 在这些场景中，数字会装箱为 Java 类 Integer、 Double 等，对相同数字的可为空引用可能会引用不同的对象***

> 引用官网的一句话，具体见下面

```kt
fun main() {
//sampleStart
    val a: Int = 100
    val boxedA: Int? = a
    val anotherBoxedA: Int? = a

    val b: Int = 10000
    val boxedB: Int? = b
    val anotherBoxedB: Int? = b

    println(boxedA === anotherBoxedA) // true
    println(boxedB === anotherBoxedB) // false
//sampleEnd
}

// 由于 JVM 对 -128 到 127 的整数（Integer）应用了内存优化，因此，a 的所有可空引用实际上都是同一对象。但是没有对 b 应用内存优化，所以它们是不同对象。

// 另一方面，它们仍然相等:

fun main() {
//sampleStart
    val b: Int = 10000
    println(b == b) // 输出“true”
    val boxedB: Int? = b
    val anotherBoxedB: Int? = b
    println(boxedB == anotherBoxedB) // 输出“true”
//sampleEnd
}

// 三个等号和可空类型见下文
```

##### 3.4.1.5 隐式类型转换

- 因为 Koltin 里面不同的表示方法，较小类型不是较大类型的子类，***较小类型也不能隐式转换为较大类型***

```kt
val b: Byte = 1 // OK，字面值会静态检测
// val i: Int = b // 错误
val i: Int = b.toInt()
```

> 这里回忆一下 Java 的知识点：***对于 byte short 类型的变量而言，在赋值的时候，如果被赋的值为可预知的常量，即便是高于 byte或 short 的类型，系统也会自动判断其常量值是否能够放置于 byte 或 short 类型的变量中。如果能够则编译正确，否则将会产生编译错误***

> 这个可预知的常量在 Java 里面就是定义和赋值在同一行的变量，但是 Kotlin 的编译器聪明的多，因此下面的是可以正常运行的

```kt
val b: Byte
b = 127
```

- 不过***所有的数字类型都支持转换为其他数字类型***，就是请注意你的数据是否超出，以下是 ***Kotlin 的显式转换方法***
    - toByte(): Byte
    - toShort(): Short
    - toInt(): Int
    - toLong(): Long
    - toFloat(): Float
    - toDouble(): Double

    ```kt
    val i = 15
    val b: Byte = i.toByte()
    ```

- Kotlin 里面***在数字运算时才会隐式转换类型***，具体如下

|数值一|数值二|转换后的类型|
|---|---|---|
|Byte|Byte|Int|
|Byte|Short|Int|
|Byte，Short|Int|Int|
|Byte，Short，Int|Long|Long|
|Byte，Short，Int，Long|Float|Float|
|Byte，Short，Int，Long，Float|Double|Double|

```kt
val b: Byte = 1 // 无需转换
val s: Short = 2 // 无需转换
val i: Int = 3
val l: Long = 4
val f: Float = 5.0f // 因为默认为 Double ，所以必须要转换。而且 Float 也没有 Byte 和 Short 的智能判断
val d: Double = 6.0 // 不能写 6，直接写 6.0 就行，也没有 d 这个后缀

val v1 = b + b // Int
val v2 = b + s // Int
val v3 = b + s + i // Int
val v4 = b + s + i + l // Long
val v5 = b + s + i + l + f // Float
val v6 = b + s + i + l + f + d // Double
```

#### 3.4.2 布尔值 ( Booleans )

- ***表示为布尔类型的值只能有 `true` 和 `false` 两个值***

```kt
var bool: Boolean = true
bool = false
```

> 也有可以为空的布尔变量

#### 3.4.3 字符 ( Charaters )

- ***字符用 char 类型标识，是包括在单括号 `' '`里的单个字符***

> 在 JVM 上，存储为 Char 的字符表示 16 位 Unicode 字符 char

> 在JVM 平台，当需要可空引用时字符会是装箱的 Java 类，类似于数字。 装箱操作不保留同一性

```kt
val c: Char = '永'
println(c)
```
- 如果要打印出特殊字符，可以使用以下的***转义字符***
    - \t：制表符
    - \b：退格符
    - \n：换行（LF）
    - \r：回车（CR）
    - \\'：单引号 (这里不要看 md 原格式，请看渲染完的)
    - \\"：双引号 
    - \\\：反斜杠
    - \\$：美元符 (用于字符串模板)

- 也可以***使用 Unicode 编码***，[这是](https://www.jyshare.com/front-end/3602/)一个在线 Unicode 转码网站

```kt
val c: Char = '\u6c38'
println(c)
```

- ***如果字符变量的值是数字，那么可以使用 `digitToInt()` 函数将其显式转换为数字***

```kt
val c: Char = '1'
val i = c.digitToInt()
println(i)

// 在这之前，我们所有的 kt 文件生成的 class 都可以用 JVM 来运行，但是在这里你可以试一试
// -include-runtime -d hello.jar 不受影响
```

#### 3.4.4 字符串 ( Strings )

##### 3.4.4.1 简介

- ***Kotlin 里面的字符串使用 String 类型表示，字符串字面量使用双引号 `" "` 表示***

- ***字符串是不可变的, 一旦初始化了一个字符串，就不能改变它的值或者给它赋新值, 所有转换字符串的操作都以一个新的 对象来返回结果，而保持原始字符串不变***

```kt
var str: String = "Hello Wrold!"
println(str)
```

- ***字符串中的元素 —— 字符可以轻松的使用索引来遍历***，索引见后文

```kt
var str: String = "Hello Wrold!"

for (i in str) {
    print(i)
}
```

- ***字符串可以使用 `+` 加号运算符自动连接，只要第一个是字符串，那么它也可以跟其他类型连接，结果都是字符串***

```kt
val str: String = "Hello"
println(str + 1 + 3.9 + 4.3f)
```

##### 3.4.4.2 字符串字面值

- Kotiln 里面有两种字符串字面值：
    - ***转义字符串：可以包含转义字符***

    ```kt
    val str: String = "Hello\tWorld\nTom\bAlice"
    println(str)
    ```
    - ***多行字符串：可以包含换行以及任意文本，它使用三个双引号 `""" """` 括起来，内部没有转义并且可以包含换行以及任何其他字符***

    ```kt
    val str: String = """
    This is a message.
         Tab
    
    My name is!@#%^*()))__}{|}
    """"
    println(str)
    ```

    > 如需**删掉多行字符串中的前导空格，请使用 `trimMargin()` 函数**

    ```kt
    val str: String = """
    |This is a message.
    |     Tab
    |
    |My name is!@#%^*()))__}{|}
    """.trimMargin()
    println(str)

    // 默认以竖线 | 作为边界前缀，可以选择其他字符并作为参数传入

    val str: String = """
    \This is a message.
    \     Tab
    \
    \My name is!@#%^*()))__}{|}
    """.trimMargin("\\") // 虽然里面没有了转义字符，但是这里接受的是一个表达式，所以不能单写一个斜线
    ```

##### 3.4.4.3 字符串模板

- 与其他高级语言一样，***Kotlin 也支持字符串模板，允许用美元符号 `$` 把字符串内的一部分解释为标识符***

```kt
val num: Int = 6

// 单变量写法
println("num is $num")

// 表达式写法
println("num add 6 is ${num + 6}")
```

##### 3.4.4.5 字符串格式化

> 这里 Kotlin 基本上跟 Java 一样

- ***字符串格式化使用 `String.format` 方法，参数一是要格式化的字符串，其他参数是传入的值***

```kt
val str1: String = "hello"
val str: String = String.format("%-7sTom",str1)
println(str)
```

- ***`%` 百分号是占位符，若要打印出百分号请使用 `%%`*** ，下面是每种类型占位符 `%` 可接受的标识

    1. 字符、字符串
    ```kt
    %[标识][最小宽度]转换符

    // 这里其实还有一个 index$ ，但是很不好用所以没有写，但是我要说明，感兴趣的可以自己尝试

    val str1: String = "hello"
    val str: String = String.format("%-7sTom",str1)
    println(str)
    ```

    - 标识：
        - `-`： 在最小宽度内左对齐，右边用空格补上
    - 转换符：
        - s: 字符串
        - c：字符
        - b：布尔
        - n：换行符
    
    2. 整数
    ```kt
    %[标识][最小宽度]转换符
    ```

    - 标识：
        - `-`: 在最小宽度内左对齐,不可以与0标识一起使用
        - `0`：若内容长度不足最小宽度，则在左边用0来填充
        - `#` ：对8进制和16进制，8进制前添加一个0,16进制前添加0x (Kotlin 不支持八进制)
        - `+`：整数加正号，负数加负号
        - ` `：正数前面加空格，负数前面加负号
        - `,`：三位数字间用逗号隔开
        - `(`：若结果为负数，则用括号括住，且不显示符号
    - 转换符：
        - b：布尔
        - d：整数 (DEC)
        - x：整数 (HEX)
        - n：换行符

    3. 浮点数
    ```kt
    %[标识][最小宽度][.精度]转换符 
    ```
    - 标识：
        > 与整数一样
    - 转换符：
        - b：布尔
        - n：换行
        - f：浮点数 (十进制) 显示九位有效数字，会四舍五入
        - a：浮点数 (十六进制)
        - e：指数各式的字面量 (9.38e+6)
        - g：浮点数
    
    > 这里的 f 、g 与 Java 里面的并不相同，可以参见参考的[这篇文章](https://blog.csdn.net/android157/article/details/112448721)

    4. 日期

    > 日期相关类会在后文讲解，这里只是先列出来方便查找

    ```kt
    %t转换符

    // import java.time.*

    val dt = LocalDateTime. now()
    println(String.format   ("%tF",dt))
    ```

    - 日期转换符：
        - c：星期六 十月 27 14:21:20 CST 2007
        - F：2007-10-27
        - D：10/27/07
        - r：02:25:51 下午
        - T：14:28:16
        - R：14:28
        - b：月份简称
        - B：月份全称
        - a：星期简称
        - A：星期全称
        - C：年前两位 (不足两位补零)
        - y：年后两位 (不足两位补零)
        - j：当年的第几天
        - m：月份 (不足两位补零)
        - d：日期 (不足两位补零)
        - e：日期 (不足两位不补零)

    - 时间转换符：
        - H：24小时制的小时 (不足两位补零)
        - k：24小时制的小时 (不足两位不补零)
        - I：12小时制的小时 (不足两位补零)
        - i：12小时制的小时 (不足两位不补零)
        - M：分钟 (不足两位补零)
        - S：秒 (不足两位补零)
        - L：毫秒 (不足三位补零)
        - N：毫秒 (不足9位补零)
        - p：小写字母的上午或下午标记：如中文为 "下午"：英文为pm
        - z：相对于GMT的时区偏移量：如+0800
        - Z：时区缩写：如CST
        - s：自1970-1-1 00:00:00起经过的秒数
        - Q：自1970-1-1 00:00:00起经过的豪秒

##### 3.4.4.6 字符串常用方法

> 我不想粘贴复制了，常用的就那些，可以到[这篇文章](https://www.cnblogs.com/weizhxa/p/9982565.html)中看一下

### 3.5 空安全

> 首先回忆一下，在 Java 里面有一个特殊的值，*null*，它是所有引用类型的默认值，你可以把任何一个引用类型的变量的值设为 null，也可以把 null 转化为任何类型的值，我们今天讨论的是 ***`null` 导致的空指针异常***

- 如果对一个空对象访问或调用它的属性和方法，运行时的虚拟机就会抛出 NoPointerException，Kotlin 在编译时就加入了对空指针的规避，所以***在 Kotlin 里面所有的变量默认都不能赋值为 `null`***

```kt
val num: Int
num = null

// error: null cannot be a value of a non-null type
```

- 如果这个对象就是有可能是 null 呢？你可以***在变量类型的右面加上一个 `?` 解除限制，这类可以为空的变量类型，叫可空变量***

```kt
val num: Int? = null
```

- 在 Kotlin 里面，因为没有了基本类型，所以所有的变量、类和函数都是类型，***变量的共同父类叫 `Any` (可以看作是 Java 的 Object)，所有可空变量的父类是 `Any?`***

```kt
val any1 = Any()
println(any1)

// res1: kotlin.Any = java.lang.Object@4397a639
```

- 所以在 Kotlin 里面，可空类和不可空类的区别很大，***可空类不可以调用默认方法，参数类型为不可空类的函数也不能接受可空类的变量***

```kt
fun main() {
    val num: Int? = 2
    test(num)   // error
    println(num.plus(1))    // error
}

fun test(num: Int) {
    println(num)
}
```

- 要想解除限制，可以***使用显式流程控制判断变量和它的属性是否为空***，Kotlin 的编译器会自动判断；也可以***用安全调用操作符 `?.`***

> 如果使用流程判断，结果仍有可能报错，因为多线程情况下可能你判断完还能有一个线程再把它改成空的，所以推荐使用 `?.`
```kt
val num: Int? = 2

println(num?.plus(1))
```

> 如果***变量不为空就返回正常结果，否则返回 null***

- 另外***还有一种 `!!.` 的写法，这叫非空断言，这样的话编译器如果遇到 null 就会抛异常了***

```kt
val num: Int? = 2

println(num!!.plus(1))
```

### 3.6 类型检测与转换

> 前面提过，Kotlin 不会隐式的转换类型，那怎样才能判断变量的类型并且正确的转换呢？

#### 3.6.1 is 和 !is

- ***`is` 和 `!is` 用来判断变量是否是一种类型，返回布尔值***

```kt
if (obj is String) {
    print(obj.length)
}

if (obj !is String) { // 与 !(obj is String) 相同
    print("Not a String")
} else {
    print(obj.length)
}
```

> 判断的是 Number 、Character，不是 Char、Int

#### 3.6.2 智能转换

- ***Kotlin 的编译器足够聪明，它能够跟踪你的条件判断语句，知道这个地方的变量一定是某种类型的，所以可以不用强制类型转换，前提是编译器能保证变量在检测及其使用之间不可改变***

```kt
fun demo(x: Any) {
    if (x is String) {
        print(x.length) // x 自动转换为字符串
    }
}


if (x !is String) return

print(x.length) // x 自动转换为字符串


// || 右侧的 x 自动转换为 String
if (x !is String || x.length == 0) return

// && 右侧的 x 自动转换为 String
if (x is String && x.length > 0) {
    print(x.length) // x 自动转换为 String
}   // 这个 || 的惰性下一章会讲


when (x) {
    is Int -> print(x + 1)
    is String -> print(x.length + 1)
    is IntArray -> print(x.sum())
}
```

#### 3.6.3 as 和 as?

- ***使用 `as` 可以强行转换类型，如果转换失败会抛异常***

> 有些时候***请注意可空类***

> 注意 ***as 不会改变原来变量的类型***，只是返回一个新的值让另一个不同类型的变量接受，***而且一般用不到这个操作符，因为有方法***
```kt
val x: String? = y as String?

// 如果 y 可能空就只能这样写
```

- ***也可以使用安全转换操作符 `as?`，它会在转换失败的时候返回 null***

```kt
val x: String? = y as? String

// 虽然 y 转换的类型是不可空类，但是这个表达式的结果可以为空
```

### 3.7 变量类型与有效范围

#### 3.7.1 本地和成员变量

> 在 Java 里只有两种变量，本地变量和成员变量

- 在 Kotlin 里面也大致相同，***定义在类里面很好方法同一级的叫成员变量 (属性)，定义在方法、函数内部或流程控制语句内部的叫本地变量 (局部变量)，成员变量有效范围是整个类范围 (包括方法内)，本地变量出了所在的花括号就失效了***

- 同样的，***本地优先，函数参数 > 函数内本地变量 > 类属性***

```kt
fun main() {
    val num: Int = 10

    var test1: Test = Test()
    test1.test_func(num)
}


class Test {
    val num: Int = 20

    fun test_func(num: Int) {
        val num: Int = num + 30

        println(num)    //
        println(this.num)
    }
}
```

#### 3.7.2 const 修饰符

- 之前说过 val 修饰的是一个常量，但***其实 val 表示的是你不能直接通过赋值 `=` 办法修改它的引用指向，但是可以通过修改它指向的对象修改它***

```kt
fun main() {
    val test1: Test = Test("Hello")

    test1.str = "World" // 通过属性来修改，虽然 test1 不可变但是 str 可变

    println(test1.get_str())

    val array = intArrayOf(1,2,3)
    array[0] = 100 // 通过修改数组的下标修改
    
    for (i in array) {
        println(i)
    }
}

class Test(var str: String = "") {
    
    fun get_str():String {
        return str
    }
}
```

- 与其相对的，还有一个 ***`const` 修饰符，它表示编译器不变量，也就是在编译过程中不会变化的变量，在运行时直接通过对常量的替换为实际值***，但是限制如下
    - ***只能修饰 val，声明就要初始化***，不能稍后初始化
    - ***位于顶层、object 或伴生对象***
    - ***必须是基本类型或 String***
    - ***不能有自定义 getter***

```kt
// 顶层声明如下，它不属于任何类或函数，直接属于文件，如果其他文件想要使用此常量可以用包名.常量名来使用

const val PI: Double = 3.1415926

fun main() {
    println(PI)
}
```

- 这个***位于顶层的变量可以被所有函数访问，甚至可以修改***，不过出于规范不建议将变量位于顶层

```kt
var num = 10

fun main() {
    println(num)

    func()
    println(num)

    num = 30
    println(num)
}


fun func() {
    num = 20
}

// 10   20  30
```


## 第四章：表达式、语句和操作符

### 4.1 操作符

- 操作符就是符号，用于对变量进行简单快速的操作，这里介绍 Kotlin 里的数字操作符

> 这里没讲 Kotlin 操作符的优先级，因为我觉得没用，你用上几个括号读者也能明白，不过这里
> 这里没讲 Kotlin 操作符的优先级，因为我觉得没用，你用上几个括号读者也能明白，不过[这里](https://www.jianshu.com/p/962a093097d3) 可以看到

#### 4.1.1 加减乘除

- ***`+` 加 `-` 减 `*` 乘 `/` 除  `%` 除法求余***

    > 以下是他们对应的方法，注意***调用 a.plus(b) 不会改变 a 本身的值***，你要把结果接走

    - 加 + ：plus
    - 减 -：minus
    - 乘 *：tiems
    - 除 /：div
    - 取余 %：rem

> Kotlin 没有原生的乘方，但是 math 包里面有

> ***加号和减号也用于字面量的正负值，减号也可以改变数字的正负***

- ***两个整数间的除法结果总会返回整数，对于任何整数都是，若想要返回带有精度的结果请将其中一个除数显性的转换为小数***

```kt
 val x = 5 / 2
//println(x == 2.5) // ERROR: Operator '==' cannot be applied to 'Int' and 'Double'
println(x == 2)

val x = 5L / 2
println(x == 2L)    // true

val x = 5 / 2.toDouble()
println(x == 2.5)   // true
```

- ***Kotlin 对整数提供了一组位运算，它们直接使用数字的比特表示在二进制级别进行操作， 位运算有可以通过中缀形式调用的函数表示，只能应用于 Int 与 Long***

    > 中缀见下文，这里只是记住它的形态即可

    - shl(bits) – 有符号左移
    - shr(bits) – 有符号右移
    - ushr(bits) – 无符号右移
    - and(bits) – 位与
    - or(bits) – 位或
    - xor(bits) – 位异或
    - inv() – 位非

#### 4.1.2 赋值与自增

- ***`=` 等号用于赋值，将右边表达式的结果赋值给左边的变量***

- ***`+=`、 `-=`、 `*=`、 `/=`、 `%=` 是广义赋值操作符***，可以方便的完成如下

```kt
num = num + 1

// 也可以简便的写成

num += 1
```
- ***`++`、 `--` 是递增与递减操作符***，他们的对应方法如下，
    - 加一 ++：inc
    - 减一 --：dec

```kt
num += 1

// 也可以写成

num++
```

- ***`i++` 和 `++i` 的区别在于，`i++` 先返回本身再自增，`++i` 先自增再返回本身***

```kt
fun main() {
    var i: Int = 10
    
    var j: Int = i++ + 10
    var k: Int = ++i + 10

    println("i is $i, j is $j, k is $k")


    var a: Int = 10
    
    var b: Int = --a + 10
    var c: Int = a-- + 10

    println("a is $a, b is $b, c is $c")

}
```

- ***但请注意 Kotlin 里面的使用方法的自增自减不会修改原值，使用 `++i` `i++` 的才能改变原值***

```kt
var i: Int = 10

var j: Int = i.inc() + 10

println(j)
println(i)
println(i.inc())
println(i)
```

> 可能是因为 `i++` 内部的实现就是 `i = i++` 吧

#### 4.1.3 逻辑与比较

- ***`&&`、 `||`、 `!` 逻辑与、或、非操作符，注意`&&` `||` 是惰性的***，也就是如果前面的判断满足了需求则不运行后面的表达式

```kt
var num: Int = 23
println(false && (++num > 0))
println(true || (++num > 0))
println(num)    // 23
```

- ***`==` `!=` 相等不等操作符***，对于非原生类型会调用 `equals()`

> `a == b` 会翻译成 `a?.equals(b) ?: (b === null)`

```kt
val num: Int = 3
val str: String = "abc"

println(num == str.length)
```

- ***`<`、`>`、`<=`、`>=` 比较操作符，对于非原生类型会翻译为调用 `compareTo()`***

- ***`===` 引用相等操作符，用来判断两个变量指向的对象是否相同***

```kt
fun main() {
    var a = "Hello"
    var b = a
    var c = "world"
    var d = "world"

    println(a === b)
    // true，因为把 a 对象的的地址给了 b
    println(a === c)
    // false，不同
    println(c === d)
    // true，因为字符串存储于常量池，使用的时候会优先判断有没有使用过的，这里正好就用上了

}
```

### 4.2 表达式

- 语句和表达式都是最基本的部分，二者都可以执行操作，不同的是***语句没有返回值而表达式一定有返回值*** (在 Kotlin 里语句也没有分号结尾)

- Kotlin 简化了 Java 中的一些语句的语法，并且增加了新的语句和表达式，下面会对基本的语句进行讲解

- ***在 Kotlin 里面的赋值是一个语句而不是表达式***，不是 Java 里面可以返回赋值的值的表达式，这点记住了

### 4.3 流程控制

#### 4.3.1 if

- ***`if` 是一个条件表达式，因此它可以返回一个值，`if` 根据自己后面括号里的表达式的值真假，执行不同的流程，也可以使用 `else if` 创建更多的分支***

```kt
// 语法

if (判断式) {
    // 分支一
} else if () {
    // 分支二
} ··· {
    // ··· 
} else {
    // 最后分支
}
```

```kt
// 官网的文档应该很简单

fun main() {
    val a = 2
    val b = 3

    //sampleStart
    var max = a
    if (a < b) max = b

    // With else
    if (a > b) {
      max = a
    } else {
      max = b
    }

  // 作为表达式
 max = if (a > b) a else b

    // else if 表达式
    val maxLimit = 1
    val maxOrLimit = if (maxLimit > a) maxLimit else if (a > b) a else b


    println("max is $max")
    println("maxOrLimit is $maxOrLimit")
}
```

- ***`if` 表达式的分支可以是代码块，这种情况最后的表达式作为该块的值***，如果你把 `if` 作为表达式则这种写法是必须的

```kt
val max = if (a > b) {
    print("Choose a")
    a
} else {
    print("Choose b")
    b
}
```

- 当有一个可为 `null` 的引用时，进行：***不是 `null`，就用它，否则用一些非空值***的判断时，除了完整的写 `if` 外，还可以***使用 `elvis` `?:` 表达式***

```kt
val l = b?.length ?: -1

// 仅当 b?.length 不为空时才返回 b?.length，否则返回 -1
// 只有 ?: 才是表达式的主体，b?.length 只是因为这有可能是一个空值的引用，elvis 左边的表达式可以返回空也可以返回不空
```

> 仅当左侧为 `null` 时，才会计算右侧的表达式

#### 4.3.2 for

- ***`for` 循环可以对任何提供迭代器的对象进行遍历***，它的语法如下，十分简洁连类型都不用写

```kt
for (item in collection) {
    // 循环体
}

// 单行的语句可以省略花括号

for (item in collection) print(item)
```

- ***Kotlin 还提供了区间操作符 `..` 用于快捷的创建循环，`in` 用来判断元素是否位于区间***

```kt
for (i in 1..5) println(i)
```

```kt
// .. 和 ..< 的区别如下

val num = 9

println(num in 0..num)    // true
println(num in 0..<num)   // false
```

> 相比 Java 的规范写法，这个 `for` 的确简化很多

- ***使用 `downTo` 来实现反向迭代，使用 `step` 自定义步长***

```kt
for (i in 0..8 step 2) print(i)
// 02468

for (i in 0..<8 step 2) print(i)
// 0246

for (i in 8 downTo 0 step 2) print(i)
// 86420
```

> 最后一个元素是根据：  
    > 对于正步长：不大于结束值且满足 (last - first) % step == 0 的最大值  
    > 对于负步长：不小于结束值且满足 (last - first) % step == 0 的最小值

#### 4.3.3 while

- ***`while` 和 `do-while` 当循环条件满足时会持续执行它们的主体***，它们之间的区别在于条件检查的时间
    - ***`while` 先检查条件，如果满足，则执行主体，然后再返回到条件检查***
    - ***`do-while` 先执行主体，然后检查条件。如果满足，则循环重复***，所以 do-while 的主体至少执行一次，不管条件如何

```kt
var x = 0

while (x < 10) {
    println("now x is $x")
    x++
}

var y = 0

do {
    y++
    println("now y is $y")
} while (x < 10)
```

#### 4.3.4 when

- ***`when` 是一个具有多个分支的条件表达式***，它的语法如下

- ***`when` 将它的参数与所有的分支条件顺序比较，直到某个分支满足条件，如果都没有对应的分支则求值 `else`***

```kt
when (x) {
    1 -> print("x == 1")
    2 -> print("x == 2")
    else -> {
        print("x is neither 1 nor 2")
    }
}

// 类似 switch
```

- ***`when` 既可以作为表达式使用也可以作为语句使用，如果它被当做表达式，第一个符合条件的分支的值就是整个表达式的值，如果当做语句使用，则忽略个别分支的值***

- ***类似于 `if`，`when` 也可以当作表达式，每一个分支可以是一个代码块，它的值是块中最后的表达式的值***

- ***如果把 `when` 当作一个表达式来用，则必须有一个 `else` 分支，除非编译器知道已经覆盖了所有的结果*** (比如枚举)
```kt
val num = 5

val str = when (num) {
    5 -> {
        println("num is $num")
        5
    }

    else -> {
        println("num is not 5")
        "null"
    }
}

println(str)
```

- ***使用 `,` 逗号还可以在一行定义多种情况***

```kt
when (x) {
    0, 1 -> print("x == 0 or x == 1")
    else -> print("otherwise")
}
```

- ***可以用任意表达式 (而不只是常量) 作为分支条件***

```kt
when (x) {
    s.toInt() -> print("s encodes x")
    else -> print("s does not encode x")
}
```

- ***也可以使用区间判断***

```kt
when (x) {
    in 1..10 -> print("x is in the range")
    in validNumbers -> print("x is valid")
    !in 10..20 -> print("x is outside the range")
    else -> print("none of the above")
}
```

- ***还可以根据变量的类型进行判断***

```kt
fun main() {
    val num: Short = 10
    type_dectec(num)
}



fun type_dectec(a: Any) {
    
    when (a) {
        is String -> println("this is a String")
        is Byte -> println("this is a Byte")
        is Short -> println("this is a Short")
        is Boolean -> println("this is a Boolean")
        is Number -> println("this is a Number")    // 你不能把 Number 放在前面，否则 Byte 和 Short 永远访问不到
        is Character -> println("this is a Chharater")
        else -> println("i dont what this is")
    }
}
```

- ***`when` 也可以替代分支很多的 `else if`，如果不提供括号里的表达式，所有的分支条件都是简单的布尔表达式，而当一个分支的条件为真时则执行该分支***

```kt
val num = 99

when {
    num in 1..10 -> println("num in 1 .. 10")
    num in 11..20 -> println("num in 11 .. 20")
    num in 21..30 -> println("num in 21 .. 30")
    num in 31..40 -> println("num in 31 .. 40")
    num in 41..50 -> println("num in 41 .. 50")
    else -> println("i dont num is?")
}


// 这种写法比 if 简明概要
```

#### 4.3.5 返回与跳转

- Kotlin 有三种跳转表达式：`break` `continue` `return`，其中
    - ***return 默认从最直接包围它的函数或者匿名函数返回***
    - ***break 终止最直接包围它的循环***
    - ***continue 继续下一次最直接包围它的循环***

    > 什么叫最直接包围，请看下面

    > 目前不会讲解 return，等到内联函数和 lambda 讲完再说，现在记住 break 用于终止循环，continue 用于跳过就行

```kt
fun main() {
    for (i in 1..5) {
        for (j in 1..5) {
            if (i == 3 && j == 3) {
                break
            }

            println("i is $i, j is $j")
        }
    }
}

// 打印结果说明 break 只结束了 j 在 3 的循环
```

- 如果想要精准控制循环，可以使用标签，***在 Kotlin 中任何表达式都可以用标签来标记，标签的格式为标识符后跟 `@` 符号***

```kt
loop@ for (i in 1..5) {
    for (j in 1..5) {
        if (i == 3 && j == 3) {
            break@loop // 注意这里是没有空格，且 @ 在前
        }

        println("i is $i, j is $j")
    }
}

// 打印结果说明当 j 和 i == 3 的时候，整个循环都被终止
```


## 第五章：函数

### 5.1 函数的创建和使用

> 函数用于执行一系列运算，并返回结果，函数最重要的是里面的函数体

- ***Kotlin 使用 `fun` 关键字创建函数，后面是函数名 (遵循标识符命名法则) ，再后面是参数和返回值，和花括号里的函数体***

- ***对于有返回值的函数，你必须要通过 `return` 语句返回一个符合返回值类型的值，`return` 后函数是直接结束的，在 `return` 后面的语句是不会被访问到的***
，具有返回值的函数的返回值就可以被变量或者其他函数接走

```kt
fun add_int(x: Int, y: Int): Int {
    return x + y
}
```

> 如果是这样***只有一行的函数，可以直接省略花括号，使用 `=` 直接把函数体的返回值写在右面***，如果返回值类型是可推断的，你甚至连返回值类型也不用写 (不建议，少几个字的事万一编译器不能自动推断呢？)

```kt
fun add(a: Int, b: Int): Int = a + b
```

- 如果你的函数什么都不返回，那么你可以不写返回值，或者写上 ***`Unit` ，这个类型表示此函数没有返回值***

> 如果有返回值那么必须手动显式指定返回值类型，这一点编译器不会帮你

```kt
fun print_int(n: Int) {
    println(n)

    // 就算你不写 Unit，编译器也会自动加上
}
```

> 这个 `Unit` 跟 Java 的 `void` 不一样的点是，***`Unit` 是一个单例对象，返回 `void` 的函数表示自己真的是什么也不返回，但是返回 `Unit` 的函数是一定要返回 `Unit` 的***

```kt
fun print_int(n: Int) // : Unit 编译器自动加上，这个 Unit 表示类型 {
    println(n)

    // return Unit 自动加上，这个 Unit 表示对象
}
```

> 这也是为什么说 Kotlin 是一门全是对象的语言，这个 ***Unit 就取消了有返回值类型函数和无返回值类型函数的区别***

- 创建完成函数什么都不会发生，你不去调用函数也不会执行，***使用 `函数名()` 的方式调用函数***

```kt
println(add_int(2,3))

// 这里注意到 println 就是一个函数，函数里面再套一个函数，println 接走 add_int 的返回值 5 并打印出来
```

> 理论上函数名应该符合驼峰命名法，如 addInt，但是现在在讲函数式编程，我喜欢蛇形命名法就用蛇形命名法，到了类再说

### 5.2 函数的参数

> 先科普一下，函数的参数可以叫做***实参和形参***，***形参指的是函数参数声明里面的那个参数类型，实参指的是你传进来的那个值***

- Kotlin 里面函数的参数是不可改变的，也就是你没法改变传进来的参数的值，***函数参数是 `val` 的***

```kt
fun main() {
    var n = 10

    my_func(n)
}



fun my_func(n: Int): Int {
    n = 20
    // error: 'val' cannot be reassigned.
    return n
}
```

> 回忆一下，***在 Java 里面，函数参数传递都是值传递的，基本类型把自己值复制一份传进去，引用类型把自己的值 (也就是自己指向内存堆中对象的地址) 复制一份传进去，导致基本类型的变量在函数里面修改不会影响到外面的实参，但是引用类型的变量可以直接修改外部的对象的属性***，如果不明白可以看[这篇文章](https://blog.csdn.net/asd0356/article/details/95747524)

- Kotlin 里面虽然没有了基本类型，但是因为不能在函数里修改参数，所以也只能依靠***传入引用变量的方法修改参数***

```kt
fun main() {
    val fooc = foo()

    println(my_func(fooc))
    println(fooc.n)
}



fun my_func(fooc: foo): Int {
    fooc.n = 40

    return fooc.n
}

class foo {
    var n: Int = 30
}
```

#### 5.1.2 参数的格式

- ***Kotlin 里函数参数的命名规范是 `name: type` ，每一个参数都必须显性指定类型，参数用逗号隔开***，当调用者传入类型不正确的参数或是参数数量不对都会报错

```kt
fun func(l: Int, str: String): Boolean {

    if (str.length == l) {
        return true
    } else {
        return false
    }

}
```

> 也可以***尾部用逗号换行***，当参数很多的时候方便阅读

```kt
fun func(l: Int,
    str: String,
): Boolean {

    if (str.length == l) {
        return true
    } else {
        return false
    }

}
```

#### 5.1.2 缺省参数

- ***函数参数也可以有默认值，只要在参数类型的后面加上 `=` 等号指定缺省值***，如果调用者没有为此参数指定值就使用缺省值

```kt
fun main() {
    println(times(3))
}


fun times(a: Int, b: Int = 2): Int {
    return a * b
}
```

- ***注意缺省参数一定在没有缺省值参数的后面***，不然调用时候传进来的值是没法赋给没有默认值的参数的

#### 5.1.2 具名参数

- ***在调用函数的时候，除了遵守默认参数的顺序传参外，还可以自己手动通过 `参数名 = 实参` 的方式传值，这叫具名参数***

```kt
fun main() {
    val by: Byte = 10

    val resault: Int = add_int_and_byte(byte_arguments = by, int_arguments = 1)

    println(resault)

}


fun add_int_and_byte(int_arguments: Int,
    byte_arguments: Byte,
): Int {
    return int_arguments + byte_arguments.toInt()
}
```

#### 5.1.2 可选参数

> 如果我有一个函数未来可能接受很多的参数，那么我该怎样写出函数的参数？难道是根据参数数量的不同写上几十个？

- ***使用 `vararg` 修饰符修饰的参数，在函数调用时可以接受多个参数，并将他们保存在数组里***，方便调用

```kt
fun main() {
    
    say_hello("Tom", "Alice", "Jack")
}


fun say_hello(vararg names: String) {

    for (i in names) {
        println("hello $i")
    }
}
```

- 既然 `vararg` 的实现原理是保存在数组里，那么我就***不能传入一个数组当可变参数***了吧？对的，不过可以***使用 `*` 星号把数组拆开，一个一个传入***

> 这就是 Kotlin 的语法糖，当你熟悉的时候你就离不开了

```kt
fun main() {
    val names = arrayOf("Peter", "Tomy", "Dog")

    say_hello("Tom", "Alice", "Jack", *names)
}


fun say_hello(vararg names: String) {

    for (i in names) {
        println("hello $i")
    }
}
```

### 5.3 递归函数

- ***递归函数不是什么特殊函数，他就是函数内部又调用了自己，这就叫递归函数***

> 由于 Kotlin 语法上支持面向函数编程，因此写出下面的例子很简单

```kt
fun main() {
    fibonacci(1,1,10000)    // 计算斐波那契数列
}



tailrec fun fibonacci(a: Int, b: Int, limit: Int) {
    println(a)
    println(b)
    println("ratio is ${b/a.toDouble()}")

    if (b < limit) {
        fibonacci(a + b, b + a + b, limit) // 如果没有 limit 那么栈会溢出
    } else {
        
    }
}
```

- 因为递归会消耗栈导致性能下降，Kotlin 还准备了一个 ***`tailrec` 修饰符，可以用于优化递归，但是函数必须将其自身调用作为它执行的最后一个操作***

### 5.4 高级函数

> ***Kotlin 函数都是头等的，这意味着它们可以存储在变量与数据结构中，并可以作为参数传给其他高阶函数以及从其他高阶函数返回。可以像操作任何其他非函数值一样对函数进行操作***

> 这一节涉及到类和对象，如果听不懂可以看完 5.2 再回来看

#### 5.4.1 高阶函数

- ***高阶函数就是指将函数类型用作参数或返回值的函数***，没错在 Kotlin 里面函数是可以作为参数或返回值的

> 指针函数和函数指针的阴影又回来了

- 因为***不同的函数参数类型、参数列表、返回值类型都不一样***，所以声明函数类型的参数或返回值请写全，使用 `(参数) -> 返回值` 的语法声明

> ***Unit 不能省略***

```kt
// 把函数当作参数

fun my_func(func1:(Int) -> String):String {
    // 这是一个接受参数为一个 Int 返回 String 的 func1 函数当作参数并且自己返回 Strirng 的函数

    // my_func() 是函数名，func1 是参数名，(Int) -> String表示 func1 这个参数是一个接受 Int 返回 String 的函数类型，:String 是 my_func 的返回值

    // func1 不是这个函数类型的名字，只是这个参数的名字，它叫 arg 也可以
}


// 把函数当作返回值

fun my_func():Int, Byte, Short -> Unit {
    // 这是一个没有参数，但是返回一个参数为 Int、Byte、Short 返回 Unit 的函数当返回值的函数

    // my_func(): 是函数名，此函数没有参数，但是返回值 Int, Byte, Short -> Unit 是一个函数类型
}
```

> 注意到***函数类型是参数，那么必须有参数名，参数名: 后面才是函数类型；函数名是返回值则没有名字***

- ***还可以有接受函数的函数的函数，使用 `( )` 括号可以区分多个参数和返回值，不过箭头表示法是右结合的***，所以

```kt
(Int) -> ((Int) -> Unit) == (Int) -> (Int) -> Unit != ((Int) -> (Int)) -> Unit
```

> 那怎么传入函数？直接传名字？带不带括号？

- ***若想将一个函数作为参数或者返回值传入，请在函数名左侧加上 `::` 双冒号，这叫函数引用***

```kt
fun main() {
    my_func1(::my_func2)
}


fun my_func1(func: (Unit) -> Int) {
    println(func(Unit)) // 你这里的确传入了 Unit
}


fun my_func2(Unit: Unit): Int {
    // 左边的 Unit 是参数名，右面的是形参
    return 1

}
```
> 这里为什么有这么多 `Unit`？，这是大坑，这方面编译器不会把空的函数参数理解为 Unit，只是认为你没有参数而不是 `Unit`

```kt
fun main() {
    my_func1(::my_func2)
}


fun my_func1(func: (Unit) -> Int) {
    println(func())
}


fun my_func2(): Int {
    return 1

}

// no value passed for parameter 'p1
// inapplicable candidate(s): fun my_func2(): Int

// 这是因为 my_func2 你没有写 Unit 参数，你以为编译器会自动加上，但是他在调用的时候会发现：欸？明明有一个 Unit 参数的啊？为什么你调用的时候什么都没有呢？包括在::my_func2 的时候也会发现明明接受的是一个有 Unit 参数的函数，你这里却是什么都没有的 my_func2
```

> 样还是建议写上 Unit 像上面那样

- 好，回到主题，***`::` 表示为此函数创建一个对象，这也是 Kotlin 能实现高阶函数的原因，他把函数当作对象包装起来传入函数***

```kt
fun main() {
    val func3: (Unit) -> Int = ::my_func2   // 这样也是可以的 func3 是一个指向函数类型的对象的引用变量

    // func3() == my_func2()
    // (::my_func2)() = my_func2()

    my_func1(func3) // 也可以，func3 已经是函数类型的对象了
}


fun my_func1(func: (Unit) -> Int) {
    println(func(Unit))
}


fun my_func2(Unit: Unit): Int {
    return 1

}
```

- 这个***函数类型的对象与普通函数没什么区别，你对它调用 `()`，其实就是在调用它的 `invoke()` 方法***

> 但是你不能对函数调用 `invoke()`，***函数不是函数类型的对象***，函数就是函数

```kt
val func3: (Unit) -> Int = ::my_func2

// func3() == my_func2() == func3.invoke() != my_func2.invoke()

my_func1(func3)
```

> 这样的话看看下面

```kt
val func3: (Unit) -> Int = ::my_func2

func4 = func3   // ok?

// 当然可以，因为 func3 已经是对象了，这下 func4 也是函数类型的对象了
```

- 记住，***函数不是函数类型的对象，但是函数能干的函数类型的对象也能干***

- ***如果高阶函数的参数是一个可能为空的函数类型 (也就是可能是一个函数，可能是 `null`) ，对于这个可空的参数，请用括号 `()` 括起来整个类型并在右面加上 `?`***

```kt
fun my_func1(func: ((Unit) -> Int)?) {
    println(func(Unit))
}
```

> 注意这是***参数可能为空，可能为函数***，不等于***参数是一个包含可空参数或返回值的函数***

```kt
fun my_func1(func: (Int?) -> Int?) {
    println(func(2))
}
```

#### 5.4.2 匿名函数

- 既然可以把函数赋给变量，还有更简易的写法，可以***直接把函数体放在变量赋值的右面，这叫匿名函数***，这样就可以省略函数名了，而且 ***Kotlin 也不允许匿名函数有函数名***

```kt
val func3 = fun (Unit: Unit): Int {
    return 1
}

// 注意参数列表前面没有函数名，val 后面的是变量名
// 支持类型推断
```

> 那么就可以用使用匿名函数用于不想创建一个函数的地方，直接使用匿名函数传入

```kt
fun main() {
    val func1 = fun (func: (Unit) -> Int) {
        println(func(Unit)) // 这是函数声明的函数体
    }

    func1(fun (Unit: Unit): Int {
        return 1    // 调用函数，这里是函数的参数的函数体
    })
}

// 等价于


fun main() {
    val func3 = fun (Unit: Unit): Int {
        return 1
    }

    val func1 = fun (func: (Unit) -> Int) {
        println(func(Unit))
    }

    func1(func3)
}

// 等价于


fun main() {
    val func3 = fun (Unit: Unit): Int {
        return 1
    }

    my_func1(func3)
}


fun my_func1(func: (Unit) -> Int) {
    println(func(Unit))
}

```

- 同理 Kotlin 的***匿名函数也区分可空类***

```kt
val sum_1 = fun (a: Int?, b: Int?): Int? {

    return when {   // when 当作表达式
        a == null -> null   // a is null 不对，因为 null 不是类型，null 是值
        b == null -> null
        else -> a + b
    }
}

println(sum_1(2,null))  // null
```

#### 5.4.3 lambda

- 其实还有一种更简单的语法：***`lambda` 表达式***

> `lambda` 就是匿名函数，不要被这个希腊字母 `λ` 吓到

```kt
val sum: (Int, Int) -> Int = { x: Int, y: Int -> x + y }
```

- `lambda` 的语法如下：
    - ***`lambda` 表达式总是括在花括号中***
    - ***完整语法形式的参数声明放在花括号内，并有可选的类型标注***，没错类型可写可不写，只要你前面声明了
    - ***函数体跟在一个 `->` 之后***
    - ***如果该 `lambda` 的返回类型不是 `Unit`，那么该 `lambda` 主体中的最后一个 (或可能是单个)  表达式会视为返回值***

    > ***`lambda` 不能用 `return` 语句返回，用了 return 会直接把最外面的函数结束掉***，见下文

```kt
fun main() {
    val func1 = fun (func: (Unit) -> Int) {
        println(func(Unit))
    }

    func1({Unit: Unit ->
        1   // 不要加 return ，return 会直接结束外面的函数，至于更详细的见下文
    })
}
```

- ***如果 `lambda` 是函数的最后一个参数，可以把 `lambda` 写在函数参数括号外面，这叫拖尾 `lambda` 表达式***

```kt
val print_resault = fun (a: Int, b: Int, func: (Int, Int) -> Int) {
    println(func(a,b))
}

print_resault(2,4) { a: Int, b: Int -> 
    a.plus(b)
}
```

- ***如果 `lambda` 是函数唯一的参数，你还可以直接把括号去了***

```kt
func1 {Unit: Unit ->
    1
}
```

- ***如果 `lambda` 本身是单参数的，这个参数也可以直接不写，如果想要调用的话直接 `it` 就行***

> 没错，***在 `lambda` 的里面 `it` 也是一个关键字，在外面不是***
```kt
val print_resault = fun (func: (String) -> Int) {
    println(func("asdf"))
}

print_resault() {
    it.length   // Kotlin 里面 length 不是方法，而是属性，请不要加上括号，否则

    // error: expression 'length' of type 'kotlin.Int' cannot be invoked as a function. Function 'invoke()' is not found.

}

```

> 这个 `lambda`这么简洁，不会有什么问题吧？你像它是怎么知道自己的参数类型和返回值类型的

- ***`lambda` 依赖上下文推断，你在声明匿名函数的地方和调用匿名函数的地方，总有一个地方要显式指明参数类型和返回值才可以，都不写也是不行的***

```kt
val print_resault = { func:(String) -> Int ->   // 你这里可能会觉得 Kotlin 会把两种箭头搞混，如果你给 func 加上括号发现报错，所以不用担心
    println(func("asdf"))
}

print_resault() { 
    it.length
}


// 你可以注意到如果在变量类型声明函数类型是不需要参数名的 (你就是参数类型声明参数名称干什么)
// 但是在匿名函数里面声明是需要参数名的，因为你可能会用到他


val print_resault: ((String) -> Int) -> Unit = {
    println(it("asdf"))
}

// 既然你这右面不是匿名函数，那么左面的变量就应该声明类型方便编译器

print_resault() { 
    it.length
}

// 当然下面的不可以，编译器不知道你到底接受什么类型

val print_resault = {
    println(it("asdf"))
}

print_resault() { 
    it.length
}
```

- ***如果 `lambda` 表达式的参数未使用，那么可以用下划线 `_` 取代其名称***

```kt
val sum_2: (Int, Int) -> Int = { _, a ->
    a
}

println(sum_2(3,4))
```

> `lambda` 不要太紧凑以至于自己都读不懂

```kt
val print_resault = { func:(String) -> Int -> println(func("asdf")) }

// 上面是写在一行，下面是缩进写法

val print_resault = { func:(String) -> Int ->
    println(func("asdf"))
}
```
- ***在 Kotlin 里面，有三种函数类型的变量：函数引用、匿名函数和 `lambda`***

> 请看下面的实例

```kt
val sum_1 = fun (a: Int, b: Int) = a + b
val sum_2 = fun (a: Int, b: Int) = { a + b }

println(sum_1(2,3))
println(sum_1(2,3)) // ?
println(sum_2(3,4)())   // ?


// 首先 sum_1 就是一个简单的函数，可以直接写在一行
// 第二个也是，写在一行的依据是该函数只有一个返回值，等号的右面直接就是返回值
// 所以该函数返回什么？返回另一个函数？是返回一个函数类型的 lambda
// 所以先调用 sum_2() ，返回一个函数而不是结果，再调用 sum_2()() 才行
```

> 关于 lambda 其实就是这些，Kotlin 在这方面提供了丰富的语法糖方便使用，但是轻松的时候也不要忘了规范格式。记住***函数名加上括号一定是在使用函数，无论 lambda 还是匿名函数都是函数体，函数体不调用是不会执行的。函数名加上双冒号是创建了一个函数类型的对象，匿名函数和 lambda 都是在创建对象。传递一个函数类型的对象，接收者就可以调用它，记住传值时没有括号也没有冒号***

> 如果还不明白，可以看下 [Google 的文档](https://developer.android.google.cn/codelabs/basic-android-kotlin-compose-function-types-and-lambda?hl=zh-cn#0)，通俗易懂

#### 5.4.4 内联函数

> 乍一听很恐怖的名字，其实很简单

- 如上面所说， Kotlin 能将函数作为参数传递，函数引用的原理是他创建了一个跟函数同样功能的类型，那么你可能会想：***每一次调用函数就生成一个类型，有点耗资源吧***

- Kotlin 也想到了，因此出现了***内联函数修饰符 `inline`，内联函数标记这个函数的函数体在调用处展开，包括如果自己的参数是一个函数类型，也展开到调用处，这样执行起来不用创建一堆函数类型的对象，不太占用性能***

> 这个主要是为了解决函数类型的参数带来的性能消耗，如果函数被放在循环里，函数本身调用带来的栈消耗不算什么，但是函数类型的参数就很恐怖了

```kt
fun main() {
    my_func_1 { println("Hello") }
    
    // 相当于
    // println("Hello")
    // println("world")
}


inline fun my_func_1(func: (Unit) -> Unit) {
    func(Unit)  // 这里会被替换为 println("Hello")
    println("World!")
}
```

> 内联的意思就像是 `编译时常量` 一样，`const` 这个常量的值会被编译器在每个调用的地方复制一份过去，就像 C 的宏一样，这个内联函数也是同理，把函数体复制过去

- 再说一遍，***`inline` 是修饰函数用的，表示这个函数的函数体和函数参数的函数体被展开到调用处***

- 既然这样，那么***就没法再使用函数类型的参数当作对象来操作了，因为他不再是一个函数类型的对象了***

```kt
fun main() {
    val func = my_func_1 { println("Hello") }
    func(Unit)  // 想象中的，但是不行
}


inline fun my_func_1(func: (Unit) -> Unit): (Unit) -> Unit {
    func(Unit)
    println("World!")

    return func   // 这里会报错，因为把代码展开后编译器根本不知道这个 func 是什么
    // 不用 :: ，因为 func 本身已经是对象了
}
```

- 那么我就想要函数类型的参数怎么办？***给一个函数类型的参数加上 `noinline` ，这个函数类型的参数就不会加入内联了，可以用把它当作对象来传递***

> ***`noinline` 是给参数修饰的，`inline` 是给函数修饰的***

```kt

fun main() {

    val func = print_hello({ println("World") ; "World" })

    println("test here")
    
    func(Unit)
}


inline fun print_hello(noinline func: (Unit) -> String): (Unit) -> String {
    println("Hello")

    return func // 可以把函数作为返回值返回而无需内联
}
```

- 但是仔细一想，如果***我的函数类型的参数 (`lambda`) 里面有 `return` 怎么办？不就直接把调用它的函数 (调用它指的是调用内联函数的函数，比如 `main`) 给结束了？***

```kt
fun main() {

    println(print_hello({ println("World") ; return })) // 这里不能返回 String ，因为这个 return 实际上是 main 的 return

    println("test here")    // 不会发生
}


inline fun print_hello(func: (Unit) -> Unit): String {
    println("Hello")

    println(func(Unit))

    return "Wjkasd"
}
```

> 仔细观察下面这个与上面的区别

```kt
fun main() {

    println(print_hello({ println("World") ; "World" }))

    println("test here")
}


inline fun print_hello(func: (Unit) -> String): String {
    println("Hello")

    return "Wjkasd" // 在内联函数本身里面加上 return 是可以的

    println(func(Unit))

}
```

> ***这种 `return` 叫非局部返回，指的就是他直接结束了外面的外面的函数***

- 所以 Kotlin 直接***不允许 `lambda` 里面有 `return` (像上面说的那样)，除非这个 `lambda` 是 `inline` 函数的参数，这样 `lambda` 里面的 `return` 实际上是结束了外面的调用者函数***，相当于利用了这个非局部返回

> ***注意这个限制只是针对 `lambda`*** ，匿名函数没有，当然具名函数也没有

```kt
// 匿名函数

fun main() {

    println(print_hello(fun (Unit): String {
        println("World")

        return "Hi"
    }))

    println("test here")
}


inline fun print_hello(func: (Unit) -> String): String {
    println("Hello")

    println(func(Unit))

    return "Earth"
}
```

```kt
// 具名函数

fun main() {

    println(print_hello(::print_world))

    println("test here")
}


inline fun print_hello(func: (Unit) -> String): String {
    println("Hello")

    println(func(Unit))

    return "Earth"
}


fun print_world(Unit: Unit):String {
    println("World")

    return "World2"
}
```

- ***使用 `crossinline` 可以指示这个函数类型的参数不允许非局部返回，同时 `crossinline` 允许参数内联***

```kt
fun main() {

    println(print_hello({ println("World") ; return }))
    println("test here")
}


inline fun print_hello(crossinline func: (Unit) -> Unit): (Unit) -> Unit {
    println("Hello")

    return func
}

// error: 'return' is prohibited here.
// 告诉你 crossinline 不允许 return

// error: illegal usage of inline parameter 'crossinline func: (Unit) -> Unit'. Add 'noinline' modifier to the parameter declaration.
// 告诉你 crossinline 修饰的参数是内联的，如果不内联请使用 noinline

```

> 最后梳理一下:

| 函数类型的参数 | inline | noinline | crossinline|
|:---:|:---:|:---:|:---:|
|内联吗?|✓|✕|✓|
|能否非局部返回?|✓|✕|✕|
|还是函数类型的对象吗?|✕|✓|✕|

> ***`inline` 修饰的函数，自己本身和自己函数类型的参数都会被打开平铺在调用 `inline` 函数的地方，节省资源。但是这样的参数不能被间接的以一个函数类型的对象来使用 (因为已经铺平了)，支持非局部返回***

> ***`noinline` 是修饰 `inline` 函数的参数，表示该参数不会被拆开，仍然以函数类型的对象来传递，不支持非局部返回***

> ***`crossinline` 不支持非局部返回，支持内联***

- 还有一句，***无论是 `noinline` 还是 `crossinline`，只能在已经声明了 `inline` 的函数的参数里面用***，没有 `inline` 你别想了

### 5.5 局部函数

- ***Kotlin 支持局部函数，即一个函数在另一个函数内部***

```kt
fun main() {
    val num = 10

    fun inner_func(a: Int): String {
        return a.toString()
    }

    println(inner_func(num)) // 局部函数你不调用他也不会执行
}
```

- ***这样的函数就叫局部函数，局部函数可以访问外部函数的局部变量***，如果把这个可以访问外部函数的局部变量的内部函数当作外部函数的返回值返回出去，还能调用吗？

```kt
fun main() {

    val f = func()

    println(f("f")) // 1
    println(f("b")) // 2
    println(f("c")) // 3
}


fun func(): (String) -> String {
    
    var num = 0

    return { str: String ->
        "this time $str is ${++num}"
    }

}
```

> 没错，是可以正常使用的，而且效果像是 num 的每一次调用不像是重新初始化，而是记住了自己上次的值

- 这种特性叫***闭包，指一个局部函数使用自己外部函数中变量的组合，如果将一个闭包的局部函数作为返回值返回出去，那么实际上编译器会把整个函数的上下文环境和局部函数包起来返回出去***，这样外部的变量在调用函数的时候有一些内部的变量他是访问不到的，被很好的封装起来

```kt
// 比如这里我不希望每一个函数的调用者可以用修改工资数量，所以直接返回一个函数回去让他们填上自己的名字，至于金额他们根本摸不到

fun main() {

    val f = func()

    println(f("Bob"))
    println(f("Jack"))
    println(f("Tomy"))
}


fun func(): (String) -> String {
    
    val money = 1_0000

    fun get_money(name: String) = "$name 's money is $money"

    return ::get_money
}
```

- ***局部函数可以还有局部函数***

```kt
fun main() {

    val f = func()

    println(f("Bob")(20000))
    println(f("Jack")(30000))
    println(f("Tomy")(10))
}


fun func(): (String) -> (Int) -> String {   // 箭头表示法是右结合的，最后面的 String 才是他要返回的
    
    val money = 1_0000

    fun get_money(name: String): (Int) -> String {
        var more_money = money

        fun i_want_more(more: Int): String {
            more_money = more

            return "$name 's money is $more_money"
        }

        return ::i_want_more
    }

    return ::get_money
}
```


## 第六章：类和对象

### 6.1 初识面向对象

