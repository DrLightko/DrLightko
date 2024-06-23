# Kotlin 入门

> 说在前面：

> 本文是面向零基础用户进行讲解 (但最好看过 Java 或 C 哪怕一点，简单入门后再来看这篇，简单 10 倍)，因此尽可能的不会遗漏，但若有疏漏错误请联系  

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

5. 因为这是 JatBrains 的语言，所以建议使用 [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) (其他的IDE使用体验均不如它) 来开发，或者 [VSCode](https://code.visualstudio.com/) 免费开源

> 如果使用 VSCode 一定要找一个好用一点的插件，体验还是不如 IntelliJ ，这是我们目前用的[插件](https://marketplace.visualstudio.com/items?itemName=mathiasfrohlich.Kotlin)

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

```kt
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
val num: Int = 1_000_000_000

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
    - ***只能修饰 val***
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

#### 4.1.1 加减乘除

- ***`+` 加 `-` 减 `*` 乘 `/` 除  `%` 除法求余***

    > 以下是他们对应的方法

    - 加 + ：plus
    - 减 -：minus
    - 乘 *：tiems
    - 除 /：div
    - 取余 %：rem

> Kotlin 没有原生的乘方，但是 math 包里面有

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

## 第五章：类和函数

> 这是入门的最后一章，也是内容最多的一章

### 5.1 函数

#### 5.1.1 函数的创建和使用

> 函数用于执行一系列运算，并返回结果，函数最重要的是里面的函数体

- ***Kotlin 使用 `fun` 关键字创建函数，后面是函数名 (遵循标识符命名法则) ，再后面是参数和返回值，和花括号里的函数体***

- ***对于有返回值的函数，你必须要通过 `return` 语句返回一个符合返回值类型的值，`return` 后函数是直接结束的，在 `return` 后面的语句是不会被访问到的***
，具有返回值的函数的返回值就可以被变量或者其他函数接走

```kt
fun add_int(x: Int, y: Int): Int {
    return x + y
}
```

> 如果是这样***只有一行的函数，可以直接省略花括号，使用 `=` 直接把函数体写在右面***，如果返回值类型是可推断的，你甚至连返回值类型也不用写 (不建议，少几个字的事万一编译器不能自动推断呢？)

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

#### 5.1.2 函数的参数

> 先科普一下，函数的参数可以叫做***实参和形参***，***形参指的是函数参数声明里面的那个参数类型，实参指的是你传进来的那个值***

- 

##### 5.1.2.1 参数的格式

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

##### 5.1.2.2 缺省参数

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

##### 5.1.2.3 具名参数

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

##### 5.1.2.4 可选参数

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

#### 5.1.3 递归函数

- ***递归函数不是什么特殊函数，他就是函数内部又调用了自己，这就叫递归函数***

> 由于 Kotlin 语法上支持面向函数编程，因此写出下面的例子很简单

```kt
fun main() {
    fibonacci(1,1,10000)    // 计算斐波那契数列
}



fun fibonacci(a: Int, b: Int, limit: Int) {
    println(a)
    println(b)
    
    if (b < limit) {
        fibonacci(a + b, b + a + b, limit) // 如果没有 limit 那么栈会溢出
    } else {
        
    }
}
```

- 因为递归会消耗栈导致性能下降，Kotlin 还准备了一个 ***`tailrec` 修饰符，可以用于优化递归，但是函数必须将其自身调用作为它执行的最后一个操作***

#### 5.1.4 高级函数

> 高阶函数并不是什么特殊函数，Kotlin 里的函数只不过是功能丰富一些，本质上他们都一样

##### 5.1.4.1 