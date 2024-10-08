# Kotlin 入门
 
> 说在前面：
 
> 本文是面向零基础用户进行讲解，所以尽可能会把细节讲明白，但是还是假设你已经简单了解过 Java 或 C# 这类的语言
 
> 有一些在引用块里面（就像这样）的小提示可能需要下文的知识，请多多回顾



# 第一章：认识 Kotlin
 
## 1.1 简介
 
- Kotlin 是由著名的 ***Jet Brains 公司开发***，是一门***基于 `JVM` 的高级静态强类型语言***（JVM-based, high-level, statically-typed language），融入了他们对于 Java 语言的改进与想法，并且与 Java 无缝兼容。***Kotlin 继承了 Java 的优点的同时还拥有了一些高级语言的新功能***

- 本文为了保证受众面广所以不会只针对安卓开发的 Kotlin 讲解，而是相对全面的介绍 Kotlin 的基础知识和官方库，所以可以放心观看，每一个使用到的 API 都会标明

## 1.2 安装
 
1. 在 Github 上面的 [Kotlin](https://github.com/JetBrains/kotlin/releases) 编译器仓库下载最新版，Kotlin 基于 JVM，所以你必须要有 [JDK](https://learn.microsoft.com/zh-cn/java/opKotlinKotlin enjdk/download) 才行，这个微软打包的版本，你也可以到 OpenJDk 官网下载
 
> 现在也有了 Native 版本，可以自己尝试
 
2. **把 JDK 添加到环境变量** (Windows 打开图形界面，Linux 打开 /etc/profile) ，添加
    - *JAVA_HOME* = jdk/ 到用户变量
    - **%JAVA_HOME%\bin** 到 Path
    - **%JAVA_HOME%\jre\bin** 到 Path
 
3. **把 kotlin\bin 添加到环境变量**
 
4. 打开命令行，输入
 
```
java -version
 
javac -version
 
kotlic -version
 
// 是 kotlinc ，有 c 是编译器的意思
 
kotlinc 
 
// 这样会进入 Kotlin 的命令式终端
```
 
5. 因为这是 JatBrains 的语言，所以建议使用 [IntelliJ IDEA](https://www.jetbrains.com/idea/download/)（其他的IDE使用体验均不如它）来开发，或者 [VSCode](https://code.visualstudio.com/) 免费开源，再或是 Notepad++
 
> 如果使用 VSCode 一定要找一个好用一点的插件，整体体验还是不如 IntelliJ，JetBrains 罪大恶极



# 第二章：简述

## 2.1 Hello World！

```kt
fun main() {
    println("Hello World!")
}
```

> Kotlin 还有 `.kts` 为后缀的脚本文件，可以直接运行

```kts
println("Hello World!")
```

- 这是 Kotlin 里面 Hello World 的写法，确实**相比 Java 来说简洁很多**，而且像是**函数式编程**（functional programming）

- 首先，***`fun` 关键字用于声明一个函数，main 函数是程序的入口***，在函数章之前所有的语句都写在 main 里面，**函数的正文写在大括号里面**

> 见过 def、func、fn 和函数类型开头的，没见过用 fun 声明的

> 在函数章以前，所有的代码都发生在 main 函数里面，所以会省略 main 不写望周知

- ***`println` 用于打印字符串并换行，还有 `print` 函数打印却不换行***

```kt
fun main() {
    print("Hello ")
    print("World!")
}
```

> 你也看到了，***Kotlin 不需要分号结尾***，但是可以***使用 `;` 来分割处在同一行的语句***，因此请**注意代码规范格式**

```kt
val num: Int ; num = 10
```

- ***`readln` 可以从命令行读取用户输入***，具体的输入输出可以见后文

```kt
fun main() {
    println("What's your name?")
    val name = readln()
    println("Hello " + name)
}
```

## 2.2 编译运行

- ***Kotlin 文件以 kt 为结尾***，下面是**编译运行的过程**

```kt
kotlinc hello.kt

// 生成 HelloKt.class ，再使用 jvm 运行

kotlin HelloKt

// 我不知道为啥单词开头就大写了
```

- 也可以包含 Kotlin 的运行时**生成一个 jar 文件**，然后使用 Java 来运行

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

## 2.3 注释

- ***注释（comment）是代码中用来解释代码的文字，不会被编译***，因此可以用来编写注解一类的话。与 Java 一样，***Kotlin 支持普通注释和类注释***

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

- Kotlin 的***注释甚至可以嵌套***，下面的是不会报错的

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

- Kotlin 的***注释支持 `Markdown` 语法***，比如 IDEA 里面可以直接看块级注释的 md 格式，别的 IDE 能不能看不知道

```kt
/**
 *
 * # 一级标题
 * ## 二级标题
 *
 * - 单行
 * > 简单描述
 *
 * ```java
 * // 代码块
 *
 * public class Test {
 *
 *     public static void main(String[] args) {
 *
 *         System.out.println("Hello World!");
 *     }
 * }
 * ```
 *
 * - $x - 9$ `latex` 格式好像不太行
 * 
 * - 表格：
 * 
 * |头标题|头标题|
 * |-|-|
 * |内容|内容|
 */
```



# 第三章：变量与基本类型

> 与所有的编程语言一样，变量很好基本类型是最重要也是最基础的一章

## 3.1 变量的声明

- Kotlin ***使用 `val` 和 `var` 声明一个变量（Variable）***

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

- ***`val` (value) 声明只读变量，`var` (variable) 声明可变变量***，建议**优先使用 `val` 去声明变量**，***赋值运算符是 `=` 等号***，**表示把右边的值赋给左面的变量**

> Kotlin 是一门***一切皆对象*** 的语言，所以 Kotlin 的变量都指向一个对象，它也***没有基本类型***，所以这也是这一章开头基本类型是斜体的原因

> 你甚至可以*对变量调用方法和属性*，见下文

- ***`:` 用于声明变量的类型，变量的类型写在变量名和冒号的右边***

```kt
val i:Int = 12

// 加上一个空格更美观

val i: Int = 12
```

- 还有一句话，***在 Kotlin 里所有的变量类型都没有默认值，在使用前必须初始化，否则编译器会报错***，无论是成员变量还是本地变量

## 3.2 标识符

- **变量、函数、类的名字叫标识符（Identifier）**，Kotlin 的标识符***命名规定与 Java 相同***：
    1. 标识符可以***由字母、数字、下划线 `_` 组成***
    2. 标识符***不能以数字开头***
    3. ***区分大小写***，因此 myvar 和 MyVar 是两个不同的标识符
    4. **不可以使用关键字和保留字作为标识符**，但标识符中能包含关键字和保留字
    5. 标识符**不能包含空格**

    > [官网文档](https://book.kotlincn.net/text/keyword-reference.html)上有 Kotlin 的关键字列表，Kotlin 还有一类软关键字可以在特定的位置里面充当标识符，不过你肯定不会用这些名字来当变量名，所以不提
    
## 3.3 类型推断

> 上文可以看到，笔者并没有指定 greeting 和 greet 的类型

- ***Kotlin 具有类型推断（type inference）的特性***，它会根据变量的赋值来推断它的类型，当然也可以手动指定类型

```kt
var num: Int = 10

// 等于

var num = 10
```
- 如果你***在声明变量的时候就初始化，那么可以省略变量的类型不写***

- 但是***Kotlin 是一门强类型、静态隐式语言***，所以不可以给变量随意赋值

```kt
var num = 10
num = 9.2

// 报错
```

- 强弱类型区别如下：

> 弱类型语言（strongly）在运行时会隐式做数据类型转换  
> 强类型语言（weakly）在运行时会确保不会发生未经明确转换 (显式调用) 的类型转换

> 静态类型检查（statically-typed language）是基于编译器来分析源码本身来确保类型安全  
> 动态类型语言（dynamically-typed language）是在运行时期进行类型标记的检查

> 显式类型语言（explicitly-typed language）需要在定义变量时显式给出变量的类型  
> 隐式类型语言（implicitly-typed language）可以使用类型推论来确定变量的类型  

- ***如果先声明变量但是没有初始化，就只能手动指定类型了***

> ***初始化是指变量第一次赋值的时候***，变量是可以二次赋值的，**即使是 val (局部变量) 也可以先声明再赋值** (在当前的情况下，下文中就不会了)

- 其实下面你就知道了，***只有局部变量才可以先声明再赋值，成员变量是不可以的***

## 3.4 基本数据类型

### 3.4.1 数字 ( Number )

#### 3.4.1.1 整数

- ***Kotlin 的整数有 `Byte`、`Short`、`Int`、`Long` 这四类***，注意他们不是 Java 的小写 int ··· 等基本类，也不是 Java 的 Integer 等包装类，具体怎样实现要看 Kotlin 编译器

> **Kotlin 在编译前都是没有基本类型**的，但是编译后编译器会决定 Int 会变成 int 还是 Integer

|类型|大小 (比特数)|最小值|最大值|
|---|---|---|---|
|Byte|8|-128|127|
|Short|16|-32768|32767|
|Int|32|-2,147,483,648 (-2^31)|2,147,483,647 (2^31- 1)|
|Long|64|-9,223,372,036,854,775,808 (-2^63)|9,223,372,036,854,775,807 (2^63- 1)|

```kt
fun main() {
    println(Int.MAX_VALUE)
    println(Int.MIN_VALUE)
    println(Int.SIZE_BYTES)
    println(Int.SIZE_BITS)
    println()

    println(Byte.MAX_VALUE)
    println(Byte.MIN_VALUE)
    println(Byte.SIZE_BYTES)
    println(Byte.SIZE_BITS)
    println()

    println(Short.MAX_VALUE)
    println(Short.MIN_VALUE)
    println(Short.SIZE_BYTES)
    println(Short.SIZE_BITS)
    println()

    println(Long.MAX_VALUE)
    println(Long.MIN_VALUE)
    println(Long.SIZE_BYTES)
    println(Long.SIZE_BITS)
    println()

    println(Float.MAX_VALUE)
    println(Float.MIN_VALUE)
    println(Float.SIZE_BYTES)
    println(Float.SIZE_BITS)
    println()

    println(Double.MAX_VALUE)
    println(Double.MIN_VALUE)
    println(Double.SIZE_BYTES)
    println(Double.SIZE_BITS)
    println()



    println(Char.MAX_VALUE)
    println(Char.MIN_VALUE)
    println(Char.SIZE_BYTES)
    println(Char.SIZE_BITS)
    println(Char.MAX_HIGH_SURROGATE)
    println(Char.MAX_LOW_SURROGATE)
    println(Char.MIN_HIGH_SURROGATE)
    println(Char.MIN_LOW_SURROGATE)
    println(Char.MIN_SURROGATE)
    println()
}
```

> 再说一遍，***一字节等于八位，1 byte = 8 bit，1 B = 8 b***，数据的存储详情见 C 入门

> 这里基本上与 Java 无异

- ***如果你不指定整数的类型，默认是 Int ，超出 Int 则为 Long***，如果要***显式指定 Long 值要在字面量的后面加上 `L`***

> 不能小写字母 l

> 显式指定类型会触发编译器检测该值是否超出指定类型的表示范围

```kt
val one = 1 // Int
val threeBillion = 3000000000 // Long
val oneLong = 1L // Long
val oneByte: Byte = 1
```

#### 3.4.1.2 无符号整型

- ***Kotlin 还加入了无符号整型***

|类型|大小 (比特数)|最小值|最大值|
|---|---|---|---|
|UByte|8|0|255|
|UShort|16|0|65,535|
|UInt|32|0|4,294,967,295 (2^32-1)|
|ULong|64|0|18,446,744,073,709,551,615 (2^64-1)|

> 为了方便使用，你也可以***在无符号变量的字面量后面加上后缀 `u`、`U` 或 `ul`、`UL`***，这样就不用显示转换了

> 同理，***无符号整型的类型推断也是以 `UInt` 优先***

```kt
// 手动指定
val b: UByte = 1u
val s: UShort = 1u
val l: ULong = 1u

// 自动推断
val a1 = 42u // UInt
val a2 = 100000000000u // ULong
```

> 刚刚接触 Java 的时候很疑惑为什么没有无符号整型，导致出现过一些匪夷所思的问题，没想到 Kotlin 又给加回来了

#### 3.4.1.3 浮点数

- Kotlin 提供了**基于 IEEE-754 的两种浮点数**，***`Float`（单精度小数）和 `Double`（双精度小数）***

|类型|大小 (比特数)|有效数字比特数|指数比特数|十进制位数|
|---|---|---|---|---|
|Float|32|24|8|6-7|
|Double|64|53|11|15-16|

- ***使用带有小数部分的字面量来初始化浮点数变量***，小数点后面的部分视为小数位，***默认为 `Double` 类型，若要指定 `Float` 请在字面量后加上 `F` 或 `f` 后缀***

```kt
val pi = 3.14 // Double
// val one: Double = 1 // 错误：类型不匹配
val oneDouble = 1.0 // Double

val e = 2.7182818284 // Double
val eFloat = 2.7182818284f // 小数部分包含多于 6～7 位数，那么会将其舍入Float，实际值为 2.7182817
```

#### 3.4.1.4 数字字面量

> **字面量（literal）就是变量右边的值部分，这一部分是常量**

- ***Kotlin 只有十进制、十六进制和二进制三种数字字面量***
    - 十进制 (DEC)：123、123L (Long)
    - 十六进制 (HEX)：0x0F
    - 二进制 (BIN)：0010 1101

- 浮点数字面量：
    - **默认 Double**：12.3、3.14159
    - Float 用 f 或 F 标记：1.23F、3.14159f

- 无符号整型字面量：
    - **u、U：默认UInt**
    - uL、UL：ULong

- ***可以使用下划线 `_` 使整数更易读。也可以用科学计数法使浮点数更易读***

```kt
val num: Int = 1_000_000_000
// 好像四个一位也无妨
val numCn: Int = 1_0000_0000

val d1 = 3.14e-3
println(d1)

val d2 = 3.14e+3
println(d2)
```
#### 3.4.1.5 JVM 的存储方式

- ***在 JVM 平台数字存储为原生类型 `int`、 `double` 等。 例外情况是当创建可空数字引用如 `Int?` 或者使用泛型时， 在这些场景中，数字会装箱为 Java 类 Integer、 Double 等，对相同数字的可为空引用可能会引用不同的对象***

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

#### 3.4.1.5 隐式类型转换

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

### 3.4.2 布尔值 ( Boolean )

- ***表示为布尔类型的值只能有 `true` 和 `false` 两个值***

```kt
var bool: Boolean = true
bool = false
```

> ***也有可以为 `null` 的布尔变量 `Boolean?`***

### 3.4.3 字符 ( Character )

- ***字符用 `char` 类型标识，是包括在单括号 `' '`里的单个字符***

> 在 JVM 上，存储为 `Char` 的字符表示 16 位 `Unicode` 字符 `char`

> 在JVM 平台，当需要可空引用时字符会是装箱的 Java 类，类似于数字，装箱操作不保留同一性

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

### 3.4.4 字符串 ( String )

#### 3.4.4.1 简介

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

#### 3.4.4.2 字符串字面值

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

#### 3.4.4.3 字符串模板

- 与其他高级语言一样，***Kotlin 也支持字符串模板，允许用美元符号 `$` 把字符串内的一部分解释为标识符***

```kt
val num: Int = 6

// 单变量写法
println("num is $num")

// 表达式写法
println("num add 6 is ${num + 6}")
```

- 这个字符串模板只是接受标识符并把它解析成字符串添加进字面量里，他***不能做到声明字符串模板之后再更改模板里面变量的值***

```kt
var age: Int = 13  
val str: String = "this guy is $age years old"

age = 20
println(str)
```

#### 3.4.4.5 字符串格式化

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

#### 3.4.4.6 字符串常用方法

> 我不想粘贴复制了，常用的就那些，可以到[这篇文章](https://www.cnblogs.com/weizhxa/p/9982565.html)中看一下，不过那是 Java 里的，有一些方法是过时的请注意

- 唯一需要注意的就是 `str.length` 是属性而不是方法

## 3.5 空安全

> 首先回忆一下，在 Java 里面有一个特殊的值，**`null`，它是所有引用类型的默认值，你可以把任何一个引用类型的变量的值设为 `null`，也可以把 `null` 转化为任何类型的值**，我们今天讨论的是 ***`null` 导致的空指针异常***

- 如果对一个空对象访问或调用它的属性和方法，运行时的虚拟机就会抛出 `NoPointerException`，Kotlin 在编译时就加入了对空指针的规避，所以***在 Kotlin 里面所有的变量默认都不能赋值为 `null`***

```kt
val num: Int
num = null

// error: null cannot be a value of a non-null type
```

- 如果这个对象就是有可能是 `null` 呢？你可以***在变量类型的右面加上一个 `?` 解除限制，这类可以为空的变量类型，叫可空变量***

```kt
val num: Int? = null

// Java 里 int 是基本类型，是不能赋值为引用类型的值 null 的，但是 Kotlin 可以这样写
```

- 在 Kotlin 里面，因为没有了基本类型，所以所有的变量、类和函数都是类型，***变量的共同父类叫 `Any`（可以看作是 Java 的 `Object`），所有可空变量的父类是 `Any?`***

> 实际上只有一个 `Any` 类，这个 `Any?` 只是说你在声明类型的时候使用问号说明这个引用变量可能为空，看起来这个 `Any?` 像是一个新类

> `?` 只是标记引用变量是否可为空，而不代表类型本身

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

> 如果使用流程判断，结果仍有可能报错，因为多线程情况下可能你判断完还能有一个线程再把它改成空的，所以**推荐使用 `?.`**
```kt
val num: Int? = 2

println(num?.plus(1))
```

- 使用 ***`?.` 如果结果变量不为空就返回正常结果，否则返回 `null`***

> `a?.b?.c` 这样的链式调用，如果 `a`、`b`、`c` 有一个为空，那么整个链式调用都会返回 `null`

- 另外***还有一种 `!!.` 的写法，这叫非空断言，这样的话编译器如果遇到 null 空引用就会抛空指针异常了***

```kt
val num: Int? = 2

println(num!!.plus(1))

// 我保证这个变量不为空，如果真的是空编译器也不会帮你了
```

> 也跟 Java 没什么区别了

## 3.6 类型检测与转换

> 前面提过，Kotlin 不会隐式的转换类型，那怎样才能判断变量的类型并且正确的转换呢？

### 3.6.1 is 和 !is

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

### 3.6.2 智能转换

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

### 3.6.3 as 和 as?

- ***使用 `as` 可以强行转换类型，如果转换失败会抛异常***

> 有些时候***请注意可空类***

> 注意 ***as 不会改变原来变量的类型***，只是返回一个新的值让另一个不同类型的变量接受，***而且一般用不到这个操作符，因为有方法***
```kt
val x: String? = y as String?

// 如果 y 可能空就只能这样写
```

- ***也可以使用安全转换操作符 `as?`，它会在转换失败的时候返回 `null`***

```kt
val x: String? = y as? String

// 虽然 y 转换的类型是不可空类，但是这个表达式的结果可以为空
```

## 3.7 变量类型与有效范围

### 3.7.1 本地和成员变量

> 在 Java 里只有两种变量，本地变量（local variable）和成员变量（member variable）

- 在 Kotlin 里面也大致相同，***定义在类里面很好方法同一级的叫成员变量 (属性)，定义在方法、函数内部或流程控制语句内部的叫本地变量 (局部变量)，成员变量有效范围是整个类范围 (包括方法内)，本地变量出了所在的花括号就失效了***

- 同样的，如果变量名相同，则***本地优先，函数参数 > 函数内本地变量 > 类属性***

```kt
fun main() {
    val test = Test(10)
    test.print(20)
}

class Test (var i: Int = 0) {
    fun print(i: Int) {
        for (i in 1..1) {
            println("i in for is $i")
            // for 内部的本地变量 i
        }
        
        println("i in function before val is $i")
        // 函数参数

        val i = 40

        println("i in function after val is $i")
        // 函数本地变量，覆盖了函数参数
        func()
    }

    fun func() {
        i--
        println("i in class is $i")
        // 类属性
    }
}
```

> Java 的垃圾分类就略过了，想必你也了解

### 3.7.2 const 修饰符和顶层声明

- 之前说过 `val` 修饰的是一个常量，但***其实 `val`  表示的是你只能让它初始化一次 (只能指向一次对象)，但是可以通过修改它指向的对象修改它，或是自定义 getter***，并不代表 `val` 就是常量

```kt
fun main() {
    val user = User(10)

    println(user.num)
}


class User (num: Int) {
    val num: Int = num
        get() {
            return field + 10
        }
        
}
```

- 与其相对的，还有一个 ***`const` 修饰符，它表示编译器不变量，也就是在编译过程中不会变化的变量，在运行时直接通过对常量的替换为实际值***，但是限制如下
    - ***只能修饰 val，声明就要初始化***，**不能稍后初始化**
    - ***位于顶层、object 或伴生对象***
    - ***必须是基本类型或 String***
    - ***不能有自定义 getter***

    > **`const` 是把所有用到他的地方使用值内联替换掉**，请记住这个概念
```kt
// 顶层声明如下，它不属于任何类或函数，直接属于文件，如果其他文件想要使用此常量可以用包名.常量名来使用

const val PI: Double = 3.1415926

fun main() {
    println(PI)
}
```

- 这个***位于顶层声明的变量可以被所有函数访问，如果是 `var` 甚至可以修改***

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



# 第四章：表达式、语句和操作符

## 4.1 操作符

- 操作符（oprator）就是符号，用于对变量进行简单快速的操作，这里介绍 Kotlin 里的数字操作符

- 这里 ***Kotlin 操作符的优先级***，不用记因为我觉得没用，你用上几个括号读者也能明白


|类型|符号|
|---|---|
|后置|`++` `--` `.` `?.` `?`|
|前置|`-` `+` `++` `--` `!` `labelDefinition@`|
|类型转换|`:` `as` `as?`|
|乘除余|`*` `/` `%`|
|加减|`+` `-`|
|范围运算符|`..`|
|中缀函数|`infix`|
|Elvis 运算符|`?:`|
|类型判断和区间判断|`in` `!in` `is` `!is`|
|比较|`<` `>` `<=` `>=`|
|相等判断|`==` `!==`|
|逻辑与|`&&`|
|逻辑或|`\|\|`|
|赋值|`=` `+=` `-=` `*=` `/=` `%=`|

> 从上至下优先级变低，***括号 `()` 永远是最优先的***

### 4.1.1 加减乘除

- ***`+` 加 `-` 减 `*` 乘 `/` 除  `%` 除法求余***

    > 以下是他们对应的方法，注意***调用 a.plus(b) 不会改变 a 本身的值***，你要把结果接走

    - 加 + ：`plus`
    - 减 -：`minus`
    - 乘 *：`tiems`
    - 除 /：`div`
    - 取余 %：`rem`

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

- ***Kotlin 对整数提供了一组位运算，它们直接使用数字的比特表示在二进制级别进行操作， 位运算有可以通过中缀形式调用的函数表示，只能应用于 `Int` 与 `Long`***

    > 中缀见下文，这里只是记住它的形态即可

    - shl(bits) – 有符号左移
    - shr(bits) – 有符号右移
    - ushr(bits) – 无符号右移
    - and(bits) – 位与
    - or(bits) – 位或
    - xor(bits) – 位异或
    - inv() – 位非

### 4.1.2 赋值与自增

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

### 4.1.3 逻辑与比较

- ***`&&` 与、 `||` 或、 `!` 非操作符，注意`&&` `||` 是惰性的，也就是如果前面的判断满足了需求则不运行后面的表达式***

- ***`&&` 接受的表达式都为真才返回真，否则为假：`||` 接受的表达式只要有一个为真就返回真，一个都没有返回假***

```kt
var num: Int = 23
println(false && (++num > 0))
println(true || (++num > 0))
println(num)    // 23
```

- ***`==` `!=` 相等不等操作符，对于非原生类型会调用 `equals()`***

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

- 注意，Kotlin 的*基本类型*虽然是一个类，可是编译器会尽量把它当作一个值，因此下面

```kt
fun main() {
    val a: Int? = 10
    val b = 20
    val c: Int? = a
    val d = 20
    println(a == b)
    println(a == c)
    println(a === c)
    println(b === d)

    // Identity equality for arguments of types 'kotlin.Int' and 'kotlin.Int' is prohibited.
    // Identity equality for arguments of types 'kotlin.Int?' and 'kotlin.Int?' is prohibited.
}
```

- 在使用的时候把它当作基本类型就行，不具备引用类型的特性，这一点我们会在内联类中再讲解

## 4.2 表达式

- 语句（statement）和表达式（expression）都是一门语言最基本的组成，二者都可以执行操作，不同的是***语句没有返回值而表达式一定有返回值*** (在 Kotlin 里语句也没有分号结尾)

- Kotlin 简化了 Java 中的一些语句的语法，并且增加了新的语句和表达式，下面会对基本的语句进行讲解

- ***在 Kotlin 里面的赋值是一个语句而不是表达式***，不是 Java 里面可以返回赋值的值的表达式，这点记住了

## 4.3 流程控制

### 4.3.1 if

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

> 因为 `if` 是一个表达式，因此可以写出简便写法

```kt
// 官网的文档应该很简单

fun main() {
    val a = 2
    val b = 3

    var max = a
    if (a < b) max = b // 单行语句无需花括号

    // 常规写法，else 分支
    if (a > b) {
      max = a
    } else {
      max = b
    }

    // 作为表达式
    max = if (a > b) a else b

    // else if 用于表达式
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

### 4.3.2 for

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
// .. 和 ..< 的区别如下，`..` 含首含尾，`..<` 含首不含尾

val str = "Hello"

println(str.length in 0..(str.length))  // true
println(str.length in 0..<(str.length)) // false
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

// 在所有的编程语言中，默认都是以 0 为基准
```

> 最后一个元素是根据：  
    > 对于正步长：不大于结束值且满足 (last - first) % step == 0 的最大值  
    > 对于负步长：不小于结束值且满足 (last - first) % step == 0 的最小值

### 4.3.3 while

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

### 4.3.4 when

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
        is Int -> println("is int")
        is Byte -> println("is byte")
        is Short -> println("is short")
        is Long -> println("is long")
        is UInt -> println("is unsigned int")
        is Number -> println("is num")  // 你不能把 Number 放在 Int 前面，否则永远访问不到
        is Boolean -> println("is bool")
        is Character -> println("is char")
        is String -> println("is string")
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

### 4.3.5 返回与跳转

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

> `for` 不是一个表达式

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



# 第五章：函数

> 这里的函数章就是类的方法篇，只不过为了内容不要太挤放在了单独的一章，本质上方法就是函数

## 5.1 函数的创建和使用

> 函数用于执行一系列运算，并返回结果，函数最重要的是里面的函数体

- ***Kotlin 使用 `fun` 关键字创建函数（Function），后面是函数名 (遵循标识符命名法则) ，再后面是参数和返回值，和花括号里的函数体***

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

> 对于无返回值但是也只有一行的函数也可以把函数体写在一行

```kt
fun add_int(x: Int, y: Int) { println(x + y) }

// 注意这里不是等号连接，等号表示返回值，而这里没有返回值
```

- 如果你的函数什么都不返回，那么你可以不写返回值，或者写上 ***`Unit` ，这个类型表示此函数没有返回值***

> 如果**有返回值那么必须手动显式指定返回值类型**，这一点编译器不会帮你

```kt
fun print_int(n: Int) {
    println(n)

    // 就算你不写 Unit，编译器也会自动加上
}
```

> 这个 `Unit` 跟 Java 的 `void` 不一样的点是，***`Unit` 是一个单例对象，返回 `void` 的函数表示自己真的是什么也不返回，但是返回 `Unit` 的函数是一定要返回 `Unit` 的***

```kt
public object Unit {
    override fun toString(): String {
        return "kottlin.Unit"
    }
}

// 因为默认继承自 Any ，所以以下不会报错

val unit: Any = Unit
```

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

## 5.2 函数的参数

- 我们可以定义拥有参数的函数，**参数是特殊变量，是函数签名的一部分。当函数拥有参数（形参，Parameters）时，可以为这些参数提供具体的值（实参，Arguments）**

- Kotlin 里面函数的参数是不可改变的，也就是你没法改变传进来的参数的值，***函数参数是 `val` 的***

> Kotlin 一刀斩掉了在函数里面修改引用变量的能力，不过这不代表函数接受的引用类型的变量无法在函数里面对它进行操作，只是不能修改它的指向

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

> 按值传递是函数把实参的值复制一份拿给自己，按引用传递是说函数拿到了指向实参的引用，**在 Java 里虽然都是按值传递**，但是可以通过传入引用类型的变量，通过把对象的地址传入从而实现*修改参数*，如果不明白可以看[这篇文章](https://blog.csdn.net/asd0356/article/details/95747524)

- ***Kotlin 里函数参数也都是按值传递的***

> 你说既然他没有基本类型，是不是代表我可以通过传入的基本类型的引用变量去修改它，放心吧不行的。Kotlin 的基本类型在实现上仍然是 Java 的基本类型

```kt
fun main() {

    val number = Num(-90)

    println(abs(number))

    println(number.num)
}


fun abs(num: Num) {
    // return if (num < 0) -num else num

    if (num.num < 0) {
        num.num = -(num.num)
    }
}


class Num (var num: Int = 10)
```

- 不要搞混了引用传递和值传递，比如下面，**Java 里面把以一个引用类型的变量传值传入和引用传递是两个概念**

```kt
/*

    User 对象，存储在堆中
    ^           ^
    |           |
    |           |
实参 user -> 值传递给函数参数，因为拿到了 user 的拷贝值，也指向 User


    User 对象
    ^
    |
    |
实参 user <-- 如果是引用传递，那么函数应该是拿到的 user 的地址而不是 User 的地址

*/
```

### 5.2.1 参数的格式

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

### 5.2.2 缺省参数

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

### 5.2.3 具名参数

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

### 5.2.4 可选参数

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

- 既然 `vararg` 的实现原理是保存在数组里，那么我就***不能传入一个数组当可变参数***了吧？对的，不过可以***使用 `*` 展开操作符把数组拆开，一个一个传入***

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

## 5.3 递归函数

- ***递归函数（recursive function）不是什么特殊函数，他就是函数内部又调用了自己，这就叫递归函数***

> 由于 Kotlin 语法上支持面向函数编程，因此写出下面的例子很简单

```kt
fun main() {
    println(fibonacci(1,1,10000))
}



tailrec fun fibonacci(a: Int, b: Int, limit: Int): Double {

    if (b >= limit) {   // 这个 limit 就是精度限制
        return b / a.toDouble() // 除法显性指定返回值类型
    }

    return fibonacci(a + b, a + b + b, limit) 
}
```

- 因为递归会消耗栈导致性能下降，Kotlin 还准备了一个 ***`tailrec` 修饰符，可以用于优化递归，但是函数必须将其自身调用作为它执行的最后一个操作***

```kt
fun main() {
    println(factorial(12UL))
}


tailrec fun factorial(num: ULong): ULong {

    if (num < 2UL) {
        return 1UL
    } else {
        return num * factorial(num - 1UL)
    }
}
```

> 上面的编译器会**警告说尾递归的函数必须将递归作为函数的最后一步执行，而上面的阶乘其实是把乘法当作了函数的最后一步**

## 5.4 高级函数

> ***Kotlin 函数都是头等的，这意味着它们可以存储在变量与数据结构中，并可以作为参数传给其他高阶函数以及从其他高阶函数返回。可以像操作任何其他非函数值一样对函数进行操作***

> 这一节涉及到类和对象，如果听不懂可以看完 5.2 再回来看

### 5.4.1 高阶函数

- ***高阶函数（High Order Function）就是指将函数类型用作参数或返回值的函数***，没错在 Kotlin 里面函数是可以作为参数或返回值的

> 指针函数和函数指针的阴影又回来了

> 注意是把函数当作参数，而不是函数的返回值当作参数

```kt
fun func(func1())   // 先调用 func1 ，拿到 func1 的返回值后传给 func

fun func(/*func1*/) {
    func1()

    // 把函数当作参数，可以在函数体内根据传入函数的不同动态调用
}
```

- 因为***不同的函数参数类型、参数列表、返回值类型都不一样***，所以声明函数类型的参数或返回值请写全，***使用 `(参数) -> 返回值` 的语法声明一个函数类型***

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


fun my_func1(func: () -> Int) {
    println(func())
}


fun my_func2(): Int {
    return 1

}
```

> 还可以把所有的 `Unit` 都写上，不过注意，这方面编译器不会把空的函数参数理解为 Unit，只是认为你没有参数而不是 `Unit`

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

- 好，回到主题，***`::` 表示为此函数创建一个引用对象（function reference），这也是 Kotlin 能实现高阶函数的原因，他把函数当作对象包装起来传入函数***

>  具体的原理会在后面反射的时候讲到，现在只简单的理解成这是个引用对象就行，可能不太准确

```kt
fun main() {
    val func3: () -> Int = ::my_func2   // 这样也是可以的 func3 是一个指向函数类型的对象的引用变量

    // func3() == my_func2()
    // (::my_func2)() = my_func2()

    my_func1(func3) // 也可以，func3 已经是函数类型的对象了
}


fun my_func1(func: () -> Int) {
    println(func())
}


fun my_func2(): Int {
    return 1

}
```

- 这个***函数类型的引用对象与普通函数没什么区别，你对它调用 `()`，其实就是在调用它的 `invoke()` 方法***

> 但是你不能对函数调用 `invoke()`，***函数不是函数类型的对象***，函数就是函数，具体 `invoke()` 会在后面讲

```kt
val func3: () -> Int = ::my_func2

// func3() == my_func2() == func3.invoke() != my_func2.invoke()

my_func1(func3)
```

> 这样的话看看下面

```kt
val func3: () -> Int = ::my_func2

func4 = func3   // ok?

// 赋值的意义是把右面的值赋左面，右面的 func3 存的是什么
// 存的是一个函数类型的对象的地址，把这个地址的值赋给左面的当然可以
// 这下左面的变量也指向函数对象了
```

- ***如果高阶函数的参数是一个可能为空的函数类型（也就是可能是一个函数，可能是 `null`） ，对于这个可空的参数，请用括号 `()` 括起来整个类型并在右面加上 `?`***

```kt
fun my_func1(func: ((Unit) -> Int)?) {
    println(func(Unit))
}
```

> 注意这是***参数可能为空，可能为函数***，**不等于*****参数是一个包含可空参数或返回值的函数***

```kt
fun my_func1(func: (Int?) -> Int?) {
    println(func(2))
}
```

### 5.4.2 匿名函数

- 既然可以把函数赋给变量，还有更简易的写法，可以***直接把函数体放在变量赋值的右面，这叫匿名函数（Anonymous function）***，这样就可以省略函数名了，而且 ***Kotlin 也不允许匿名函数有函数名***

```kt
val func3 = fun (Unit: Unit): Int {
    return 1
}

// 注意参数列表前面没有函数名，val 后面的是变量名
// 支持类型推断
```

> 那么就**可以用使用匿名函数用于不想创建一个函数的地方，直接使用匿名函数传入**

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

### 5.4.3 lambda

- 其实还有一种更简单的语法：***`lambda` 表达式***

> `lambda` 就是匿名函数，不要被这个希腊字母 `λ` 吓到

```kt
val sum: (Int, Int) -> Int = { x: Int, y: Int -> x + y }
```

- `lambda` 的语法如下：
    - ***`lambda` 表达式总是括在花括号中***
    - ***完整语法形式的参数声明放在花括号内，并有可选的类型标注***，没错类型可写可不写，只要你前面声明了
    - ***函数体跟在一个 `->` 之后***
    - ***如果该 `lambda` 的返回类型不是 `Unit`，那么该 `lambda` 主体中的最后一个（或可能是单个）表达式会视为返回值***

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
- ***在 Kotlin 里面，有三种方式创建一个函数类型的实例：函数引用、匿名函数和 `lambda`***

> 请看下面的实例

```kt
val sum_1 = fun (a: Int, b: Int) = a + b
val sum_2 = fun (a: Int, b: Int) = { a + b }

println(sum_1(2,3))
println(sum_2(2,3)) // ?
// HelloKt$$Lambda$12/0x00000231b000cc18@4c98385c 这个就是 Kotlin lambda 的本质东西
println(sum_2(3,4)())   // ?


// 首先 sum_1 就是一个简单的函数，可以直接写在一行
// 第二个也是，写在一行的依据是该函数只有一个返回值，等号的右面直接就是返回值
// 所以该函数返回什么？返回另一个函数？是返回一个函数类型的 lambda
// 所以先调用 sum_2() ，返回一个函数而不是结果，再调用 sum_2()() 才行
```

> **`lambda` 也可以有缺省参数**

```kt
fun func(n: Int = 1, fn: () -> Unit = { println("Hello") }) {
    println(n)
    fn()
}

fun main() {
    func(2) { println("World") }
}
```

> 关于 lambda 其实就是这些，Kotlin 在这方面提供了丰富的语法糖方便使用，但是轻松的时候也不要忘了规范格式。记住***函数名加上括号一定是在使用函数，无论 lambda 还是匿名函数都是函数体，函数体不调用是不会执行的。函数名加上双冒号是创建了一个函数类型的对象，匿名函数和 lambda 都是在创建对象。传递一个函数类型的对象，接收者就可以调用它，记住传值时没有括号也没有冒号***

> 如果还不明白，可以看下 [Google 的文档](https://developer.android.google.cn/codelabs/basic-android-kotlin-compose-function-types-and-lambda?hl=zh-cn#0)，通俗易懂

### 5.4.4 内联函数

> 乍一听很恐怖的名字，其实很简单

- 如上面所说， Kotlin 能将函数作为参数传递，函数引用的原理是他创建了一个跟函数同样功能的类型，那么你可能会想：***每一次调用函数就生成一个类型，有点耗资源吧***

- Kotlin 也想到了，因此出现了***内联函数修饰符 `inline`，内联函数标记这个函数的函数体在调用处展开，包括如果自己的参数是一个函数类型，也展开到调用处，这样执行起来不用创建一堆函数类型的对象，不太占用性能***

> 这个主要是为了解决函数类型的参数带来的性能消耗，***如果接受函数的函数被放在循环里，函数本身调用带来的栈消耗不算什么，但是函数类型的参数就很恐怖了***

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

> 内联的意思就像是 `编译时常量` 一样，`const` 这个常量的值会被编译器在每个调用的地方复制一份过去，就像 C 的宏一样，这个***内联函数也是同理，把函数体复制过去***

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

> ***`noinline` 是给参数修饰的，`inline` 是给函数修饰的***，当然只有 `inline` 存在 `noinline` 才能修饰参数

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

- 但是仔细一想，如果***我的函数类型的参数 (`lambda`) 里面有 `return` 怎么办？不就直接把调用它的函数（调用它指的是调用内联函数的函数，比如 `main`）给结束了？***

```kt
fun main() {

    println(print_hello({ println("World") ; return })) // 这里不能返回 String ，因为这个 return 实际上是 main 的 return，main 函数的返回值是 Unit

    println("test here")    // 不会发生
}

// 其实上面的内联 printhello 是发生在 println 里面的，理论上应该结束的是 println 而不是 main a
// 因为 println 也是一个内联函数，它的本质就是调用了 System.out.println ，因为它的内联，它的参数 (print_hello) 也会被展开


inline fun print_hello(func: (Unit) -> Unit): String {
    println("Hello")

    println(func(Unit))

    return "Wjkasd"
}

```

> 仔细观察下面这个与上面的区别

```kt
fun main() {

    print_hello(fun (Unit: Unit): Unit {
        println("World")

        return Unit // 如果匿名函数也支持非局部返回的话，这里结束的应该是 main 函数
    })

    println("test here")
}


inline fun print_hello(func: (Unit) -> Unit): String {
    println("Hello")
    func(Unit)

    return "Wjkasd"
}
```

> ***这种 `return` 叫非局部返回，指的就是他直接结束了外面的外面的函数***

- 所以 Kotlin 直接***不允许 `lambda` 里面有 `return`（像上面说的那样），除非这个 `lambda` 是 `inline` 函数的参数，这样 `lambda` 里面的 `return` 实际上是结束了外面的调用者函数***，相当于利用了这个非局部返回

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

> 最后梳理一下，被 `inline` 修饰的函数里的参数

| 函数类型的参数 | 默认 | noinline | crossinline|
|:---:|:---:|:---:|:---:|
|内联吗?|✓|✕|✓|
|能否非局部返回?|✓|✕|✕|
|还是函数类型的对象吗?|✕|✓|✕|

> ***`inline` 修饰的函数，自己本身和自己函数类型的参数都会被打开平铺在调用 `inline` 函数的地方，节省资源。但是这样的参数不能被间接的以一个函数类型的对象来使用 (因为已经铺平了)，支持非局部返回***

> ***`noinline` 是修饰 `inline` 函数的参数，表示该参数不会被拆开，仍然以函数类型的对象来传递，不支持非局部返回***

> ***`crossinline` 不支持非局部返回，支持内联***

>> `crossinline` 还有一种用法我们在协程的时候再讲

- 还有一句，***无论是 `noinline` 还是 `crossinline`，只能在已经声明了 `inline` 的函数的参数里面用***，没有 `inline` 你别想了

- 还有一件事，如果***想要 `lambda` 即使用 `return`，又不要非局部返回，可以使用标签***，就是我们之前在流程控制里讲过的标签

```kt
fun main() {

    println(print_hello lamb@ { 
        println("World")
        return@lamb "Earth" // 再说一遍这里的格式是 @ 在前且不能有空格
    })

    println("test here")
}


inline fun print_hello(func: (Unit) -> String): String{
    println("Hello")

    println(func(Unit))

    return "Hi"
}

// 你去观察打印结果发现所有的函数都执行了，没有中断 main
// 这就是带标签返回的作用，他结束了 lambda 而不是调用 lambda 参数的函数
```

- 如果使用标签返回可以使用隐式标签，***隐式标签的名称和接受 lambda 参数的函数名同名***

```kt
fun main() {

    println(print_hello { 
        println("World")
        return@print_hello "Earth"
    })

    println("test here")
}


inline fun print_hello(func: (Unit) -> String): String{
    println("Hello")

    println(func(Unit))

    return "Hi"
}
```

## 5.5 局部函数

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

    println(f("a")) // 1
    println(f("b")) // 2
    println(f("c")) // 3

    val g = func()

    println(g("x")) // 1
    println(g("y")) // 2
    println(g("z")) // 3

}


fun func(): (String) -> String {
    
    var num = 0

    return { str: String ->
        "this time $str is ${++num}"
    }

}
```

> 没错，是可以正常使用的，而且效果像是 num 的每一次调用不像是重新初始化，而是记住了自己上次的值

> ***不同的闭包对象之间互不干扰，因为是存了各自的一个环境***

- 这种特性叫***闭包，指一个局部函数使用自己外部函数中变量的组合，如果将一个闭包的局部函数作为返回值返回出去，那么实际上编译器会把整个函数的上下文环境和局部函数包起来返回出去***，这样外部的变量在调用函数的时候有一些内部的变量他是访问不到的，被很好的封装起来

> 什么叫函数的上下文被包装起来，请看下面的例子

```kt


fun main() {

    val func = fun (): (Unit) -> Int {
        var count = 0

        return {
            ++count
        }
    }

    val addCount = func()
    // 闭包发生，func 变量把自己的上下文都返回了出去

    for (i in 1..10) {
        println(addCount(Unit))

        // 可以看到 count 在变化，说明 count 没有重新赋值，而是一直使用一块区域内 count 的值
    }
}

```

> 利用闭包可以实现很多方便的操作

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

    fun get_money(name: String) = "${name}'s money is $money"   // 这样即使是单标识符也可以加上花括号以达到名称连贯的效果

    return ::get_money
}
```

- ***局部函数可以还有局部函数***

```kt
fun main() {

    val f = func()

    println(f("Bob")(20000))    // 这个双括号代表函数再调函数
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

> 上面的写法在数学里面有一个专有的名词叫**柯里化**，指的是$f(x,y,z)$ 转化为  $f(x)(y)(z)$ 的形式，个人觉得没用

## 5.6 函数重载

> 这里其实是下一章的内容，奈何 Kotlin 的方法也可以拿到顶层叫函数，所以放在这里，记住类里面的方法也可以重载，重载不等于重写

> 假设我有一个函数，它可以接受很多种类型的形参并且返回值回去，难道我需要写上一百个接受不同类型的函数，同时函数名还要自己去绞尽脑汁的想上一百个吗？

- ***方法重载（Overloading）的目的就是让类似的方法具有相同的名字，简化对方法的调用***
- ***在方法重载时，任意两个重载的方法之间在方法参数的个数上或是一一对应的参数类型上，至少有一项存在差别，方法的返回值类型不作任何限制***

```kt
fun main() {
    println(add(1,2))
    println(add(1L,2L))
    println(add(1.0,2.0))
}

fun add(a: Int, b: Int) = a + b + 1
fun add(a: Long, b: Long) = a + b + 100
fun add(a: Double, b: Double) = a + b + 0.001
```

- 如果***要引用一个重载的函数，则必须要知道匹配这个具体参数的重载函数***，如果无法知道的话会报错

```kt
fun func(str: String) { println(str) }

fun func() { println("Hello, World!") }

fun funcNeedFunc(func: () -> Unit) { func() }

fun funcNeedFunc(func: (String) -> Unit) { func("Hello, Kotlin!") }

fun main() {
    // val fn = ::func 报错
    // funcNeedFunc(::func) 报错
    funcNeedFunc { it: String -> println("Hello, $it!") }
    funcNeedFunc(fun () { println("Hello Java!") })
    // funcNeedFunc { println("Hello, Kotlin!") } 报错
}
```

> 说实话，Java 不支持具名参数和参数默认值所以有了方法重载，Kotlin 都有的话其实方法重载用的很少，但是也还能用，



# 第六章：包和导入

> 上一章和下一章很难，讲一点轻松的

- 为了方便代码的管理和复用，Java 里使用了包管理，Kotlin 里面的基本一样

- ***使用 `package` 声明该文件位于的包，`package` 必须位于顶层***，对于位于同一包下面的文件可以有如下的方式导入

    1. ***直接使用包名.文件名的方式导入***
    ```kt
    // User.kt

    package com.domin

    const val PI = 3.14f

    class User(name: String) {

        val name = name

        fun printName() {
            println("name is $name")
        }
    }

    fun func() {
        println("Hello World!")
    }
    ```
    ```kt
    // Hello.kt

    package com

    fun main() {
        func1()
        func2()
    }

    fun func1() {
        println(com.domin.PI)
        com.domin.func()

        val user = com.domin.User("Jordan")

        user.printName()
    }



    fun func2() {
        com.domin.func()

        println(com.domin.PI)
    }
    ```

    - ***编译器多文件编译的语法***：

    ```kt
    // 在编译时需把所有的文件引入，在运行时只需要执行带有 main 的就行

    kotlinc Hello.kt User.kt

    kotlin com/HelloKt.class
    ```

    2. ***使用 `import` 可以使包下面的类、变量和函数不需要界定符就能访问，对于命名冲突的可以使用 `as` 重命名***

    ```kt
    import com.User // 导入单个类，这个类就不需要 com.User 才能访问了
    import com.*    // 导入这个包下面的所有类、函数等顶层
    import com.User as Person   // 可能会有命名空间冲突，使用 as 重命名
    ```

    ```kt
    // Hello.kt

    package com

    import com.domin.User
    import com.domin.PI     // 这里一定注意
    import com.domin.func   // 顶层声明是属于包的
    // import com.domin.User.printName 这跟这个是不一样的
    // 不过你要是真的这么干了，你会得到
    // error: cannot import 'printName'. Functions and properties can only be imported from packages or objects.



    fun main() {
        func1()
        func2()
    }

    fun func1() {
        println(PI)
        func()

        val user = User("Jordan")

        user.printName()
    }



    fun func2() {
        func()

        println(PI)
    }
    ```

- 一定注意，***所有的顶层声明都直接属于包***，所以上面的 `import` 导入的常量和函数不需要加上 User 的界定

- 能看出，Kotlin ***不仅能导入其他文件的类，还可以导入其他文件中的函数、顶层变量***，但是这些***直接属于包而不是其他文件***

> 根据它生成的文件也能知道，上面的 User 文件编译后生成了 User.class UserKt.class 两个文件，其实 **Kotlin 是帮你把单独的这些东西放在了一个独立的文件里**，符合Java 命名规范的就放在文件名同名 class 下面，使用了顶层声明的放在带有 Kt 后缀的里面

> ***所有的顶层声明都是静态的***，位于 `文件名Kt.class` 的类中

- **Kotlin 会默认导入如下的包**：
```kt
kotlin.*
kotlin.annotation.*
kotlin.collections.*
kotlin.comparisons.*
kotlin.io.*
kotlin.ranges.*
kotlin.sequences.*
kotlin.text.*

// 根据平台也会导入以下的包

JVM:
    java.lang.*
    kotlin.jvm.*
JS:
    kotlin.js.*
```

- 还有一点，**Kotlin 里面的包名和文件名是没有关系的**，没有 Java 类名必须跟文件名一致并且同意文件下只能有一个 `public` 的类的限制，你只需要保证包名唯一就行，文件名可以随便取，但是建议文件名和类名保持一致



# 第七章：类和对象

> 这是第一部分最难也最多知识点的部分，笔者真的很幸苦不妨点个赞再走

- ***面向对象编程 (Object-Oriented Programming，OOP) 是一种重要的思想，对于代码的可复用性和维护性有着重要的作用***，虽然 Kotlin 基于 Java (后者是一门强制面向对象语法的语言) ，但是在之前的文章里我们并没有使用面向对象的概念 (倒是简单使用了方法和对象) ，所以在本章会系统的对面向对象的概念和使用进行讲解。同时，Kotlin 是一门一切皆对象的语言，因此一些操作可能跟 Java 不太一样，详见下文

## 7.1 初识面向对象

- 什么是面向对象？这里也不跟大家讲什么复杂的，**类就是一个把在逻辑上互相关的变量和函数包装起来的抽象的代码块，你要使用的话需要创建出来一个*****类的实例：对象***，这个对象里面包含着***自己的变量（成员变量、属性、Properties）和能够操作成员变量的函数（成员函数、方法、Methods、Member Functions）***

> **方法和函数基本上已经没有区别**了，你就按照一个概念理解就行

- 如此一来一系列有关的函数和变量就不需要用户手动的在 main 里面创建，只需要一个该类的对象，而且在方法里面也可以约束用户的操作，同时类还有一些更高级的操作

## 7.2 对象的初始化

- Kotlin 里***使用 `class` 关键字创建一个类，使用 `类名()` 的方式创建一个类的对象，使用 `.` 点号引用对象的属性和方法***

> ***Kotlin 里面没有 `new`***

- ***类中的属性就是正常变量的声明格式，有 `val` 和 `var` 区分，也有 `non-null` 和可空变量区分***

- ***类中的方法就是函数的声明格式***

```kt
class User {
    // User 是类名，一般首字母大写

    var age: Int
    val height: Double

    // 这就是成员变量，也叫属性
    // 就是变量的声明格式

    fun printUser() {
        println("this guy is $age years old, and $height m tall")
    }

    // 这就是成员方法，就是函数的声明格式
}



fun main() {
    
    val user_1 = User() // 创建 User 的对象
    user_1.age = 30
    user_1.height = 182.43

    // 使用属性还是方法，都是使用 . 号引用

    user_1.printUser()
}
```

- ***对象是通过对象引用变量来访问的，该变量包含了对对象的引用。该类类型的变量都可以引用该类的一个实例 从表面上看，对象引用变量种似乎存放
了一个对象；但是事实上，它只是存放了对该对象的引用，对象实际存放在堆中，对象的引用在栈中***

```kt
fun main() {
    
    val user_1 = User()
    var user_2 = User()
    // 每当你使用括号，你就是创建了一个新的对象

    println(user_1 === user_2)  // false
    // 三个等号判断的是这两个引用类型的变量是否指向的是同一个对象
    // 因为 Kotlin 里面万物皆对象，所以所有的变量也都是引用类型的变量

    user_2 = user_1 
    // 这里是干什么，是把 User 的值赋给了 user_2
    // 是把 user_1 的值赋给了 user_2，user_1 存了什么值？自己的 User 对象的地址
    // 所以现在二者指向同一个对象

    println(user_1 === user_2)  // true
}


class User // 如果一个类没有类体，可以省略花括号
```

> 不过你要是按照我上面的写时会报错的，Kotlin 在这方面是很严格的

- Kotlin 规定：***属性声明为非空的类型必须在声明后就初始化或在构造方法中初始化***，什么是***构造方法，就是你在创建对象时那个类名后面的括号***

```kt
val user_1 = User()

// 这个括号里面是可以传值的，类里面的初始化函数 (方法，我下文想说成什么就说成什么，避讳太麻烦了) 就可以接走这些参数，并使用他们
```

### 7.2.1 主构造方法

- Kotlin 里面的***主构造方法使用 `constructor` 声明，位于类头而不是类体***里面，他只有一个功能就是***接受创建对象时括号里的参数，不能有函数体***

- ***属性可以接受主构造里面的参数并为自己赋值***

```kt
fun main() {

    val user_1: User = User(54)
    user_1.print_age()
}


// class 类名 constructor(参数列表) {}
class User constructor(age: Int) {
    val age: Int = age

    fun print_age() {
        println(age)
    }
}
```

- ***如果主构造方法没有可见性修饰符或注解，可以省略该关键字，类名后面直接跟上构造方法的参数列表***

> ***但如果如果构造方法有注解或可见性修饰符，这个 `constructor` 关键字是必需的***，并且这些修饰符在它前面，详情见下文

```kt
class Customer public @Inject constructor(name: String) { /*……*/ }
```

```kt
fun main() {

    val user_1: User = User(54)
    user_1.print_age()
}


class User (age: Int) { // 这就像是函数参数一样
    val age: Int = age

    fun print_age() {
        println(age)
    }
}
```

- ***也可以直接在主构造方法里面声明属性***

```kt
fun main() {

    val user_1: User = User(54, "Dog")
    println("${user_1.name} is ${user_1.age} years old")
}


class User (val age: Int, val name: String)

// 如果这后面没有方法或者属性了，直接去掉花括号
```

> **主构造方法也支持尾部逗号换行**

```kt
class User (val age: Int,
            val name: String,
            val height: Double
)
```

- ***如果你不写主构造方法，Kotlin 默认也会加上一个无参的构造***

- ***属性的默认值使用 `=` 也可以在主构造里面声明***

```kt
fun main() {
    val user = User()

    println("${user.age}\t${user.name}\t${user.height}")
}

class User (val age: Int = 30,
            val name: String = "Peter",
            val height: Double = 180.0
)
```

### 7.2.2 init 代码块

- 因为主构造方法不能有函数体，无法执行一些更复杂的操作，所以 ***`init` 代码块出现了，它的作用就是帮助著构造方法执行其他语句***

```kt
class User (age: Int, name: String) {
    val age: Int
    val name: String

    init {
        println("age is $age, name is $name")
        this.age = age
        this.name = name
    }
}
```

- ***可以定义多个 `init` 代码块，执行顺序就是声明的顺序从上往下***

```kt
class User (age: Int, name: String) {
    val age: Int
    val name: String

    init {
        println("age is $age, name is $name")
        this.age = age
        this.name = name
    }

    init {
        println("second")
    }
}
```

### 7.2.3 次级构造方法

> 本质上**次级构造方法就是为了方法重载而诞生的**，谁让他的主构造只能声明在类头呢

> ***构造方法也可以重载***，重载方式与函数重载完全相同

- ***次级构造方法在类体里面声明，同样使用 `constructor` 加上参数列表。花括号里面是他的函数体***

```kt
class User {
    val age: Int
    val name: String

    constructor (age: Int, name: String) {
        this.name = name
        this.age = age
    }
}
```

- ***主构造方法可以不写，此时次级构造方法就会负责主构造的任务***

- ***主构造方法要么不写，写了也只能有一个；次级构造方法可以有多个，每一个构造方法以参数列表不同来进行构造方法的重载，符合参数列表的会被调用***

```kt
fun main() {

    val user_1 = User()
    val user_2 = User("Jack")
    val user_3 = User("Tomy", 24)
    val user_4 = User("Handson", 24, 170)

}


class User {
    val name: String
    val age: Int
    val height: Int
    
    constructor () : this("Peter") {}

    constructor (name: String) : this(name, 30) {}

    constructor (name: String, age: Int) : this(name, age, 180) {}

    constructor (name: String, age: Int, height: Int) {
        this.name = name
        this.age = age
        this.height = height

        println("name is $name, age is $age, height is $height")
    }

}
```

> ***请注意在类名后面加上括号表示这是一个空的主构造，而不是没有主构造***

### 7.2.4 构造顺序

> 这一节十分重要，如果你了解 Java 的话上面的不看也可以，但是这里必须要知道

- ***Kotlin 里面对象初始化的流程是***：
    1. ***执行主构造方法，初始化成员变量和执行 init 代码块***
    2. ***再执行次级构造方法***

- **如果主构造方法和次级构造同时存在，则*****每一个次级构造方法都必须调用主构造方法，无论是直接好还是间接的***

> 如果你的属性是不可变的，那么请注意***在每一个构造方法里面不要重定义属性***

- ***使用 `constructor(次级构造参数) : this(主构造或间接构造参数)` 的格式调用主构造方法***

```kt
fun main() {

    val user_1 = User()

}


class User (val name: String, val age: Int, val height: Int) {

    constructor () : this("Peter") {
        println("this is constructor()")
    }

    constructor (name: String) : this(name, 30) {
        println("this is constructor(name)")
    }

    constructor (name: String, age: Int) : this(name, age, 180) {
        println("this is constructor(name, age)")
    }

    // 在这里，无参的构造并不是直接调用了主构造，而是调用了单参数构造，单参数再调用双参数，双参数才调用的主构造
    // 这就叫间接调用
    // 看起来像是单参数先执行，但其实是 init 先执行并且拿到了属性的值，因为属性已经在最早的主构造里面初始化了

    init {
        println("name is $name, age is $age, height is $height")
    }

}

// 打印结果符合上文
```

- 请注意，***没有主构造 (也就是类名后面直接就是花括号) 和主构造方法没有参数是两码事***

### 7.2.5 this

- ***`this` 就表示自己的类，使用 `this.属性 或 this.方法()` 就可以访问到自己类里面的属性和方法，`this()` 其实跟创建对象时类名后面的括号是一个意思，所以上面的 `constructor` 调用的 `this()` 其实就是在调用自己的构造方法，但是因为方法重载的存在，只有符合参数数量和参数类型的 `this()` 才能调用到主构造***

- ***创建对象时的构造参数，只有类属性初始化赋值和 init 代码块里可以直接访问到 ( 指以变量名的方式 )***

```kt
fun main() {

    val user_1 = User(10, "some")

    user_1.printNum(40)
}


class User (num: Int) {

    var num = num   // 这个 num 就代表上面的构造参数

    constructor (num: Int, some: String) : this(num) {
        println("before the constructor, num is $num, this.num is ${this.num}")
        this.num = 30
        println("constructor set num is ${this.num}")

        // 这段话一定时最后才执行的
    }

    init {
        println("before the init, num is $num, this.num is ${this.num}")
        this.num = 20
        println("init set this.num is ${this.num}")

        // 这段话在属性初始化之后执行
    }

    fun printNum(num: Int) {
        println("now this.num is ${this.num}, num is $num")

        // 因为本地优先，所以这个方法拿到的默认的 num 是它的参数而不是类的属性，要想拿到类的属性需要 this.num
    }
}
```

- ***Kotlin 里面是本地优先，所以使用 `this` 关键字可以避免函数参数和类属性名称的冲突问题，对于同名函数也是如此***

```kt


fun main() {

    val user_1 = User( {
        "10"
    }, "some")

    user_1.printFunc( { "40" } )
}


class User (func: (Unit) -> String) {

    var func = func

    constructor (func: (Unit) -> String, some: String) : this(func) {
        println("before the constructor, func is ${func(Unit)}, this.func is ${this.func(Unit)}")
        this.func = { "30" }
        println("constructor set func is ${this.func(Unit)}")
    }

    init {
        println("before the init, func is ${func(Unit)}, this.func is ${this.func(Unit)}")
        this.func = { "20" }
        println("init set this.func is ${this.func(Unit)}")
    }

    fun printFunc(func: (Unit) -> String) {
        println("now this.func is ${this.func(Unit)}, func is ${func(Unit)}")
    }
}
```

### 7.2.5 总结

1. ***构造方法使用 `constructor` 关键字修饰，主构造方法要没有要么没有，构造方法可以有可以有很多个，每一个之间以重载来区别***
2. ***如果同时存在主构造和次级构造，则每一个次级构造都要去直接或者间接的调用主构造***
3. ***可以没有主构造，都是次级构造；如果你不写构造方法，会有一个默认的无参构造***

> ***这个默认的无参构造也会被隐式的调用，只是不用写罢了***

```kt
fun main() {
    val user_1 = User("No name", 0, 0.0)
}



class User {

    val name: String
    val age: Int
    val height: Double


    init {
        println("init")
    }

    constructor (name: String, age: Int, height: Double) {
        this.name = name
        this.age = age
        this.height = height

        println("over")
    }

}

// 先是 init 说明有一个无参的主构造被执行了
```

4. ***`init` 代码块和属性初始化都是主构造方法的一部分，执行顺序是从上往下按照声明顺序执行***

> **Kotlin 里面属性和 init 是同级初始化的**，这点和 Java 不一样，**Java 里面是 属性初始化 -> 初始化模块 -> 构造方法**

```kt
fun main() {

    val user_1 = User("No name", 0, 0.0)

    println("name is ${user_1.name}, age is ${user_1.age}, height is ${user_1.height}")
}



class User (name: String, age: Int, height: Double) {

    var name = name
    var age = age
    var height = height


    init {
        println("init_1:\nname is $name, age is $age, height is $height")
        println("this.name is ${this.name}, this.age is ${this.age}, this.height is ${this.height}")
        println()

        this.name = "Peter"
        // name = "Peter" 是不可以的，这个 name 默认是构造参数的 name ，函数参数不可变
    }



    init {
        println("init_2:\nname is $name, age is $age, height is $height")
        println("this.name is ${this.name}, this.age is ${this.age}, this.height is ${this.height}")
        println()


        this.age = 30
    }


    init {
        println("init_3:\nname is $name, age is $age, height is $height")
        println("this.name is ${this.name}, this.age is ${this.age}, this.height is ${this.height}")
        println()


        this.height = 180.0
    }

}    
```

5. ***主构造方法的参数可以在 `constructor` 构造方法、 `init` 代码块和属性初始化中通过参数名直接访问到，如果接受的参数名和属性相同，可以使用`this` 来访问属性***

## 7.3 属性

- 属性有 `val` `var` 之分，这是之前讲过的，***声明为 `var` 的变量可以后期再重新赋值， 声明为 `val` 的变量只能赋值一次***。但无论如何，***所有的成员变量，在声明的时候就要初始化***

> 有一种属性可以也不能初始化，是什么我们下面看~~没有幕后字段的属性~~

- 这个声明之后就要初始化，是指**在类体里面声明的属性，如果同时存在主构造和次级构造的情况下，即使你在次级构造里面定义了初始化，但是主构造里面没有，也时会报错的**

> 所以***主构造参数一定大于次级构造参数***

```kt
class foo(num: Int, age: Int) {
    
    val num: Int
    val age: Int

    constructor (num: Int) : this(num, num) {
        this.num = num
        this.age = num
    }
}

// 你说我在调用的时候一定是次级构造，编译器不管
// 你说我在主构造里面也定义一个行不行


class foo(val num: Int,val age: Int) {

    constructor (num: Int) : this(num, num) {
        this.num = num
        this.age = num
    }
}

// val cant be resigned
```

> 在 Java 里面，我们经常会设置 `get` `set` 方法约束变量的取值和赋值，其实在 Kotlin 里面其实也支持

### 7.3.1 getter 和 setter

> 在 Java 里面，我们一般将成员变量设置为 `private`，然后设置两个公开的 set get 方法以限制使用者对于成员变量的读写访问，在 Kotlin 里面进一步完善了这个支持

- 在 Kotlin 里面**声明一个属性，默认就会生成一个 `getter` 和 `setter`**，***调用对象的属性的时候，其实是在调用这个属性的 `getter` 和 `setter`***
```kt
fun main() {
    val user = User("Peter", 78)
}

class User (val name: String, var age: Int)

// 查看编译后的字节码可以看出来
```

> 因为 `val` 的属性只能赋值一次，所以 **`val` 的属性不会生成 `setter`，只有 `getter`，`var` 两个都有**

- `getter` `setter` 只是名称的区别，实际作用和 Java 的 `XXXget()` `XXXset()` 是一样的，***`getter` 叫读访问器，`setter` 叫写访问器***

> 因为在编译后 Kotlin 会自动给属性加上访问器，并且这个访问器的名称都是 getXXX，所以***不能自己定义一个 getXXX 方法了，会导致编译时命名冲突***

- ***自定义 `getter` `setter` 的语法如下***：

```kt
var <propertyName>[: <PropertyType>] [= <property_initializer>]
    [<getter>]
    [<setter>]

// 中括号里的均为可选
// 类型也可以从 getter 里面推断出来
// 如果已经在构造里面初始化过了，则初始化器也可以不写
```

- 因为 Kotlin 里面***调用属性的本质就是在调用属性的 `getter` 方法***，因此我们可以如下

```kt
fun main() {
    val user = User(78)

    println("age is ${user.age}")
    println("age is ${user.get_age()}")
}


class User (age: Int) {

    var age: Int = age
        get() {
            return 10
        }
    
    fun get_age(): Int {
        return this.age // 通过 this 调用也是调用 getter
    }

    init {
        println("age is $age")
    }
}

// 打印结果可以说明，虽然我们确实对 age 属性进行了赋值，但是因为自定义 getter 的存在，我们是取不到 age 真正的值的
```

> 属性既然是通过 `getter` 方法获取的，那**属性可能仅仅是存在于 ` getter` 方法中**，而不会存储在属性的字段中，我怎么才能获取真正的字段值呢？

### 7.3.2 幕后字段

- ***幕后字段（Backing Field）允许我们访问属性中真正的字段值，它只在 `getter` `setter` 中以 `field` 关键字的形式调用***

> 在 Kotlin 中，字段仅作为属性的一部分在内存中保存其值时使用。字段不能直接声明。 然而，当一个属性需要一个幕后字段时，Kotlin 会自动提供。这个幕后字段可以使用 field 标识符在访问器中引用

- ***属性初始化的时候修改的值就是幕后字段的值***

> 字段和属性的区别，可以简单的理解成字段就是 Java 里面的单一一个成员变量，而属性就是包括了 set 和 get 的成员变量

```kt
fun main() {
    val user = User(78)

    println("age is ${user.age}")

    user.age = 20

    println("age is ${user.age}")

}



class User (age: Int) {

    var age: Int = age  // 初始化器是可以修改幕后字段的
        set(value) {    // 这里的 value 不用加类型是因为 setter 方法的参数必须跟属性的类型一样，不一样是报错的
                        // 这个 value 不是关键字，你把他改成什么都可以
            field = value
        }

        get() {
            return field
            // field 和 lambda 里面的 it 一样，在 getter 和 setter 里面代表属性的幕后字段，在其他的环境下可以用作标识符
        }

        // 以上这个就是默认生成的 getter 和 setter，也就是你只声明一个 var 的变量生成的
        // val 不会生成也不允许定义 setter
}
```

- 你说不就是一个 `get` `set`  吗，为啥需要 `field`，我不能自己写？

```kt
class User (name: String){
    var name: String = name
        get() = this.name
}

fun main() {
    val user = User("John")
    println(user.name)
}

// java.lang.StackOverflowError
```

> 没错，在 Kotlin 里面 ***`this` 也是在调用自动生成的 `getter` `setter` 方法***，所以会导致上面无限递归导致栈溢出，这也是为什么需要 `field` 关键字的原因，只有它才是真正访问属性幕后的真正值的

- 还要注意，***不是所有的属性都有幕后字段，在下面的情况以外是不会生成幕后字段的***
    1. ***使用默认 `getter` `setter` 的属性，一定有幕后字段***，对于 `var` 属性来说，只要 `getter` `setter` 中有一个使用默认实现，就会生成幕后字段
    2. ***在自定义 `getter` `setter` 里面使用了 field 的属性***
    3. *不能初始化*
    > 因为初始化过的属性一定会有幕后字段，你对一个没有幕后字段的属性初始化也会得到报错，所以说***初始化过的属性不能没有上方的两个限制***

- 反过来说，***要声明一个没有幕后字段的属性***，必须：
    1. **`val` 类型的变量自定义 getter ，并在 getter 里面不使用 field**
    2. **`var` 类型的变量自定义 getter 和 setter，在两个里面都不使用 filed**
    3. ***显示声明属性的类型，并且没有初始化***

> 下文中这个属性是不会生成幕后字段的，可以通过 class 反编译看到

```kt
fun main() {
    val user_1 = User(78)
    println(user_1.age)
    
    user_1.noBackupField = 12   // 这就是在调用 set 方法，也就是给 age 加一
    println(user_1.age)
    println(user_1.noBackupField)   // 这就是在调用 get 方法，也就是返回 age
}



class User (age: Int) {

    var age = age   // 有幕后字段的属性转换成Java代码一定有一个对应的 Java 变量

    var noBackupField: Int  // 这个属性虽然看着像属性，但是通过字节码可以看到只生成了两个在名字上有关的方法，并没有生成这个属性本身
        set(value) {
            age++
        }

        get() {
            return age
        }
}
```

- 根据这个，我们如果需要***一个变量在内部表现为可读可写，在外部表现为只读***，可以使用如下的语法，这叫***幕后属性***

```kt
private var _table: Map<String, Int>? = null
public val table: Map<String, Int>
    get() {
        if (_table == null) {
            _table = HashMap() // 类型参数已推断出
        }
        return _table ?: throw AssertionError("Set to null by another thread")
    }
```

## 7.4 继承

### 7.4.1 概念

```kt
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
// 这就叫继承
```
- **继承中的父类（Parent Class）也叫基类（Base Class）、超类（Super Class）**
- **子类（Subclass）也叫派生类（Derived Class）**，子类可以通过继承获得来自父类的方法和属性而不需要自己创建

> 继承是一种 is-a 关系，即子类是父类的一种，而不是子类是父类的实例，也不是父类是子类的子集

- 为了避免混淆，**继承只能是单继承，即一个子类只能有一个父类，但是一个类可以有多个子类**

- 在 Kotlin 中***所有类都有一个共同的父类 Any***，对于没有父类型声明的类它是***默认 Any 的子类***

```kt
class Example // 从 Any 隐式继承
```

- ***Any 有三个方法：equals()、 hashCode() 与 toString()***。因此，为所有 Kotlin 类都定义了这些方法

- ***默认情况下，Kotlin 类是最终 `final` 的不能被继承，使用 open 关键字标记类使其开放继承***

> Kotlin 里面 **`final` 唯一的作用就是标记该类或者方法、属性不能被继承**

```kt
open class Base // 该类开放继承
```

- ***显式声明一个类的父类型，请在类头中把父类名称放到冒号之后***

```kt
open class Fu

class Zi : Fu() // 这表示在调用父类的无参构造
```

### 7.4.2 覆盖

> 子类通过继承，拿到了父类的属性和方法，遇到了不适合自己的怎么办？

- 子类可以***使用 `override` 关键字覆盖父类的属性或方法***，你不写就声明一个同名的属性和方法是不行的

> *强制要求覆盖方法有 `override` 方便辨认*

- 父类的***属性和方法默认是 `final` 不能被覆盖的，使用 `open` 关键字使其可被覆盖***

> 下面的 fill 方法**没有 open 修饰，子类里面不允许定义一个同名的函数，无论加不加 override**

```kt
open class Shape {
    open fun draw() { /*……*/ }
    fun fill() { /*……*/ }
}

class Circle() : Shape() {
    override fun draw() { /*……*/ }
}
```
- ***`override` 本身也是开放的，使用 `final` 使其不能再被继承***

```kt
class Circle() : Shape() {
    final override fun draw() { /*……*/ }
}
```

- 属性也是可以被覆盖的，唯一注意的一点就是 ***`var` 可以覆盖原来 `val` 的属性，反之则不行***

    1. `val` 属性是可以被 `val` 的属性所`override` 的
    2. `var` 属性是可以被 `val` 属性 `override` 的
    3. `val` 属性是不能被 `var` 属性所 `override` 的

> 因为 `val` 只有一个 getter 访问器，而 `var` 有 getter 和 setter

```kt
open class Rectangle {
    val vertexCount: Int = 4    // 长方形总是有四个顶点
    open val width: Int = 10    // 不仅这个类是 open 的，里面的也要是 open 的
    open val height: Int = 20   // 假设长宽
}


class Square : Rectangle() {    // 注意实际上有一个默认的无参构造
    override var width: Int = 5
    override var height: Int = 5
}
```

- **`override` 也可以写在主构造里面作为属性声明的一部分**，见下文

> **构造方法不继承**，注意这跟构造时子类调用父类的构造是两码事

- 请注意，***覆盖方法总是使用与父类相同的缺省参数，当覆盖一个有默认实参值的方法时，必须从参数列表中省略默认实参值***

```kt
open class A {
    open fun foo(i: Int = 10) { /*……*/ }
}

class B : A() {
    override fun foo(i: Int) { /*……*/ }  // 不能有默认值，否则会报错
    // 可能是因为 Kotlin 本质实现还是 Java 里的重载吧
}
```

- ***注意覆盖时必须完全一样 不然就重载了（重载可以跨代），覆盖之后原来的父类并不影响但是子类里面已经是新的方法了***

> 还有一点，理解覆盖不要用字面上的 "覆盖" 来理解，比如一个子类覆盖了父类的属性，不要以为是父类的这个属性字段就变了，而是子类新建了一个同名属性，父类的属性永远可以通过 super 来访问

- Kotlin 里面因为 ***`Unit` 是个类型，也是 `Any` 的子类***，所以***如果父类的返回值是 `Any`，那么子类是可以有返回值也可以是没有返回值的***

> Java 是不可以的，因为 `void` 是真的不返回

```kt
open class Fu (open val name: String) {
    open fun sayHello(): Any {
        println("Hello, my name is $name")
        return "Hello, my name is $name"
    }
}

class Son (override val name: String) : Fu(name) {
    override fun sayHello(): String {
        return "Hello, my name is $name, and I'm a Son"
    }
}

class Zi (override val name: String) : Fu(name) {
    override fun sayHello(): Unit {
        println("Hello, my name is $name, and I'm a Zi")
    }
}
```

### 7.4.3 super

- 如果子类继承了父类，子类里面的属性由子类的构造初始化，那么对于那些从父类继承而来的呢？JVM 认为应该是自己初始化自己。所以所有***子类在初始化对象的时候，都要显性或隐性的调用父类的构造***

- ***使用 `super` 关键字去指向父类***，这里的用法跟 `this` 基本一样，有 ***`super.属性` `super.方法()` `super(父类的构造参数)`***
```kt
fun main() {

    val son = Zi(2,3)
    println("number is ${son.number}, num is ${son.num}")

    val child = Zi(5)
    println("number is ${child.number}, num is ${child.num}")

}

open class Fu (val num: Int)

class Zi : Fu {

    val number: Int

    constructor (x: Int, y: Int) : super(y) {   
        number = x
        
    }

    constructor (x: Int) : super(x) {
        number = x
    }
}
```

- ***如果子类有主构造，可以也必须在主构造的右面生命父类的构造 (即便父类没有)；如果子类没有主构造，则在每一个次级构造方法里面都要使用 `super()` 调用父类的构造，或者使用间接调用的方式调用一个有 `super` 的主或次构造***

> ***因为 `this` 和 `super`没法放在一起***，所以**推荐子类拥有主构造，只需在主构造调用一次 `super` ，自己的次级构造就不用了** (反正每一个次级构造都要调用主构造)

> **派生类 (子类) 不同的次构造函数可以调用基类 (父类) 的不同的构造函数**，请看下面

```kt
fun main() {
    val son = Zi("Peter", 12)
    val child = Zi("Peter", 12, 190.0f)

    son.print_Fu()
    println("Zi:\n\tname = ${son.name}, age = ${son.age}, height = ${son.height}")
    println()

    child.print_Fu()
    println("Zi:\n\tname = ${child.name}, age = ${child.age}, height = ${child.height}")
}

open class Fu(open var name: String, open var age: Int) {

    constructor (name: String) : this(name, 30) {
        this.name = name
        this.age = name.length
    }
}


class Zi(override var name: String, override var age: Int, var height: Float) : Fu("$age", height.toInt()) {

    constructor (name: String, age: Int) : this(name, age, 180.0f) {
        this.name = name
        this.age = age
        this.height = age.toFloat()
    }

    fun print_Fu() {
        println("Fu:\n\tname = ${super.name}, age = ${super.age}")
    }
}

// 仔细看打印的结果
// 子类拥有构造重载，父类也有构造重载
// 但无论如何，子类的每一个构造方法是一定会去调用父类的构造的
```

- ***理解继承不能理解为覆写而是扩充***，即使重写了父类里的东西但是那些东西还会在，使用 `super` 仍然可以访问到

```kt
fun main(){
    val son = Zi(10)
    son.printNum()
}


open class Fu(open val num: Int)

class Zi(num: Int) : Fu(num * 3) {
    override val num = num

    fun printNum() {
        println("Zi num is $num")
        println("Fu num is ${super.num}")

    }
}
```

- 注意一下**继承的初始化顺序，子类先去初始化父类的构造，init，然后才是自己的**

```kt
fun main() {
    val son = Zi("Peter", 12)

    son.print_Fu()
    println("Zi:\n\tname = ${son.name}, age = ${son.age}, height = ${son.height}")
    println()
}

open class Fu(open var name: String, open var age: Int) {

    constructor (name: String) : this(name, 30) {
        this.name = name
        this.age = name.length
        println("父类次级构造")
    }

    init {
        println("父类 init")
    }
}


class Zi(override var name: String, override var age: Int, var height: Float) : Fu("$age") {

    constructor (name: String, age: Int) : this(name, age, 180.0f) {
        this.name = name
        this.age = age
        this.height = age.toFloat()
        println("子类次级构造")

    }

    init {
        println("子类 init")

    }

    fun print_Fu() {
        println("Fu:\n\tname = ${super.name}, age = ${super.age}")
    }
}
```

## 7.5 封装

> 本来这一章是叫权限的，看在封装是三大特性之一特此列出以表示封装的重要性

### 7.5.1 权限修饰符

- **类、对象、接口、构造函数、方法与属性及其 setter 都可以有可见性修饰符**，Kotlin 里面有四种***权限修饰符，`private` `protected` `internal` `public`***

- 前面说过，Kotlin 里面变量、函数可以直接在文件内的顶层声明，你***不作说明的话顶层声明默认为 `public` 随处可见***，如果你声明为 ***`private` ，它只会在声明它的文件内可见***。如果你声明为 ***`internal`，它会在相同模块内随处可见***

> `protected` 修饰符不适用于顶层声明

```kt
// 文件名：example.kt
package foo

private fun foo() { …… } // 在 example.kt 内可见

public var bar: Int = 5 // 该属性随处可见
    private set         // setter 只在 example.kt 内可见

internal val baz = 6    // 相同模块内可见

public open class Fu(open var name: String, open var age: Int) // 该类随处可见

// 有一点，权限修饰符总是最前面，比如上面的 public 比 open 前
```

- 而对于***类内部声明的成员***：
    1. ***`private` 意味着只该成员在这个类内部 (包含其所有成员)可见***
    2. ***`protected` 意味着该成员具有与 `private` 一样的可见性，但也在子类中可见***
    3. ***`internal` 意味着能见到类声明的本模块内的任何客户端都可见其成员***

    > 模块可以理解为就是一个项目，比如 IntelliJ 生成的一个···

    4. ***`public` 意味着能见到类声明的任何地方都可见其成员***，默认为它

> **`getter` 总是与属性共享权限**，***不意味着 `setter` 不能跟属性有一样的修饰符***，记住***一个 `public` 的 `var` 是可以有 `private set` 但是不能有 `private get` 的***

```kt
fun main() {
    someVariable = 20
    println(someVariable)
    // 顶层变量位于 `文件名kt` 的类中，main 也是，所以可以访问
}


var someVariable = 10
    private set(value) {
        println("Setting value to $value")
        field = value
    }
    public get() {
        println("Getting value")
        return field
    }

```

- 如果你***覆盖一个 `protected` 或 `internal` 成员并且没有显式指定其可见性，该成员还会具有与原始成员相同的可见性***

```kt
open class Outer {
    private val a = 1
    protected open val b = 2
    internal open val c = 3
    val d = 4  // 默认 public

    protected class Nested {
        public val e: Int = 5
    }
}

class Subclass : Outer() {
    // a 不可见
    // b、c、d 可见
    // Nested 和 e 可见

    override val b = 5   // b 为 protected
    override val c = 7   // c is internal
}

class Unrelated(o: Outer) {
    // o.a、o.b 不可见
    // o.c 和 o.d 可见 (相同模块)
    // Outer.Nested 不可见，Nested::e 也不可见
}
```

- ***构造方法也可以有权限修饰符***，下面的这个例子让调用者没法生成该类的对象 (不用单例，Kotlin 有更方便的)

```kt
class C private constructor(a: Int) { …… }

// 构造为 private 导致没办法生成类的对象
```

### 7.5.3 反引号的妙用

- 这个 `internal` ，其实没什么用，而且在跟 Java 互操作时***Java 会把 `internal` 理解成 `public`***，本来限制模块的作用也没起到，不过有一种方式可以限制 Java 无法使用

- Kotlin 里面有一个反引号（键盘左上角跟波浪在一块的符号），使用***反引号可以把不合法的标识符变为合法***，它的出现本是为了与 Java 互操作时避免关键字的冲突

> 这个 ` 无法打出来，因为在 markdown 里面这也是一个标识


```kt
fun main() {
    `fun`()
    ` `()
    `  `()
    `   `()
}


fun `fun`() {
    println("i'm `fun`")
}

fun ` `() {
    println("! !")
}

fun `  `() {
    println("!  !")
}

fun `   `() {
    println("!   !")
}
```

>比如 Java 没有 fun 关键字，可以调用一个叫 fun 的函数，但是 Kotlin 不行

- 可是**可以使用这个反引号创造出一些 Java 根本识别不了的标识符，从而避免这个 `internal` 被外部的 Java 调用**

```kt
// app/Hello.kt

package app

internal fun `class`(num: Int) {
    println("num is $num")
}

// app/Hello.java

package app;

public class Hello {
    
    public static void main(String[] args) {
        app.HelloKt.class(213);     // 报错
        app.HelloKt.`class`(213);   // 报错
    }
}
```

### 7.5.2 语法习惯

> 对于 Java 转来 Kotlin 的人 (包括我)，经常会写出这样的代码

```kt
fun main(args: Array<String>) {
    
    val son = Zi(10)
    son.printNum()
}


open class Fu(num: Int) {
    private var num: Int = num
    
    fun getNum(): Int {
        return num
    }

    fun setNum(num: Int) {
        this.num = num
    }
}


class Zi(num: Int) : Fu(num) {
    
    init {
        setNum(num)
    }

    fun printNum() {
        println(getNum())
    }
}
```

- 上面也讲过，**Kotlin 已经把属性的字段隐藏起来了**，使用 getter 和 setter 也能达到效果而且**大幅省略字数**

## 7.6 多态

> 对于从 Java 过来的人来说其实不用讲，但是为了知识的完整性还是补全了面向对象的最后一章

### 7.6.1 概念

>  以下成立吗？

```kt
val dad: Father = Son()

// 小汽车是汽车吗？
```

- ***一个父类类型的引用类型的变量，允许把一个子类的对象赋值给它***

> 那么如果父类里面和子类里面都有相同名称的属性和方法（覆盖），通过这个父类的引用类型调用时调用的是谁的？

```kt
fun main() {
    val dad: Father = Son()

    dad.num = 40
    dad.printNum()
}


open class Father (open var num: Int = 10) {

    open fun printNum() {
        println("Father $num")
    }
}

open class Son (override var num: Int = 20) : Father() {

    override fun printNum() {
        println("Son $num")
    }
}
```

> 在 Java 里面，上面的代码不会跟 Kotlin 获得一样的结果

```java
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

// main
X f1 = new C();

f1.id = 12; // 实际上是给 X 的 id 赋值
f1.out();   // int 属性默认值是 0
```

> 不像 Java 的属性是看引用，Kotlin 里**因为不允许直接对字段读写，所有的赋值语句都会包装成 getter 和 setter 两个方法**，在这两个方法里面都是**调用的属性名称**，而根据***变量本地优先的法则，`局部变量 > 成员变量 > 父类的成员变量 > ··· > Any` ，所以会优先获取对象的属性***

> 所以 ***Kotlin 里面：通过引用调方法和属性，都是看对象而不是引用***

> 这是一个很有意思的特性

- ***在把一个父类的引用指向一个子类的对象的时候，通过属性和方法优先获得的是子类的同名覆盖属性和方法，这种特性叫做多态（Polymorphism）***

> 记住是**父类和子类必须同时具有覆写方法和属性才行**，对于一个子类里面多了方法和属性的对象，你把他赋给父类引用是不行的

```kt
fun main() {
    val dad: Father = Son()

    dad.num = 40
    dad.printNum()
    dad.doSomething()   // 如果你不使用这个子类独有的方法的话也是可以编译运行的
}


open class Father (open var num: Int = 10) {

    open fun printNum() {
        println("Father $num")
    }
}

open class Son (override var num: Int = 20) : Father() {

    override fun printNum() {
        println("Son $num")
    }

    fun doSomething() {
        println("Haha")
    }
}

```

### 7.6.2 动态绑定

> 在 Java 入门这篇文章里的 7.8 动态绑定一章，我详细介绍了 Java 里面的动态绑定机制，建议没有看过的朋友先看过那一章再过来，因为懒所以我就直接搬过来了

```md
- ***绑定就是一个方法的调用与调用这个方法的类连接在一起的过程被称为绑定***，绑定可以发生在编译时也可以发生在运行时
    - ***静态绑定：前期绑定，编译时绑定***
    - ***动态绑定：后期绑定，运行时绑定***
- 在程序运行前，也就是***编译时期 JVM 就能够确定方法由谁调用，这种机制称为静态绑定***，如果一个方法由***private、static、final任意一个关键字所修饰***，那么这个方法是前期绑定的，***构造方法也是前期绑定***
> private只能被自己调用，static可以只通过类名加方法名的方式调用，final方法不会被覆写，详情请见下文*类的高级特性*
- 除了由private、final、static 所修饰的方法和构造方法外，***JVM在运行期间决定方法由哪个对象调用的过程称为动态绑定***
```

- 简单来说，***对于多态当中的同名覆写方法，在编译之后并不知道最终在使用的时候会去调用谁，而在运行时这个方法会跟真正的对象的地址绑定，这种现象就叫动态绑定***

> 下面的程序，注释掉 1 和 2 处的代码会发生什么？

```kt
fun main() {
    val dad: Father = Son()

    dad.num = 40
    println(dad.addNum())
    println(dad.addNumber())
}


open class Father (open var num: Int = 10) {

    open fun printNum() {
        println("Father $num")
    }

    open fun getNumber(): Int = num + 500 // 不能是 getNum，因为 Kotlin 默认就有了，这里会有命名冲突

    open fun addNum(): Int = num + 100
    open fun addNumber(): Int = getNumber() + 200
}

open class Son (override var num: Int = 20) : Father() {

    override fun printNum() {
        println("Son $num")
    }

    override fun getNumber(): Int = num + 50

    override fun addNum(): Int = num + 1000 // 1
    override fun addNumber(): Int = getNumber() + 2000 // 2

}
```

> 注释掉 Son 的 addNum 方法，会去找父类的 addNum ，问题是 addNum 里面的 num 是谁？记住 num 其实是 getNum 这个自动加上的访问器，因为动态绑定的存在这个方法会去调用子类里面的 getNum ，而因为变量本地优先，子类里面的方法肯定优先访问到子类里面的属性，所以这里访问的是子类的属性而不是父类的

> 注释掉 Son 的 addNumber 方法，父类里面的 addNumber 的 getNumber 调用的谁的，因为动态绑定的存在会去调用子类的，结果就是 290

> 动态绑定就是这样，有点绕，不过一定牢记 **Kotlin 里属性都是在调用方法而不是访问真正的字段**，动态绑定我们还会再见

- 多态是一个非常好用的特性，他可以大大简化代码的抽象程度，比如下面

```kt
fun main() {

    val pet_1: Animal = Cat("Lily")
    val pet_2: Animal = Dog("Talen")
    val pet_3: Animal = Cat("Octavia")
    val pet_4: Animal = Dog("Kaladin")

    val petsList = listOf(pet_1, pet_2, pet_3, pet_4)
    for (pet in petsList) {
        printPetsName(pet)
    }

}


fun printPetsName(animal: Animal) {
    
    println(animal.myNameIs())
}

open class Animal (open val name: String) {

    open fun myNameIs() = "Animal name is $name"
}

class Cat (override val name: String) : Animal(name) {

    override fun myNameIs() = "Cat's name is $name"
}

class Dog (override val name: String) : Animal(name) {

    override fun myNameIs() = "Dog's name is $name"
}
```

### 7.6.3 调用优先级

> 请看如下的例子，注意这是一个子类的引用指向子类的对象，父类里面的同名函数调用的是谁的？

```kt
fun main() {

    val son: Zi = Zi()
    son.render()
}


open class Fu {
    
    open fun render() {
        println("Fu render")
        render2()
        // 按照正常逻辑应该本地优先
    }

    open fun render2() {
        println("Fu render2")
    }
}


class Zi : Fu() {

    override fun render() {
        println("Zi render")
        super.render()
    }

    override fun render2() {
        println("Zi render2")
    }
}
```

- 没错，***父类的函数体里面如果调用了一个被继承的方法或属性，那么这个同名方法和属性调用的是子类的而不是父类的***，即便这个情况发生在子类的引用子类的对象中

> 当然父类自己的对象是会调用自己的方法的

> 为什么这个动态绑定也会发生在属性上？还是那句话，**所有的属性都是一个访问的方法，因为方法会多态指定为子类的访问器，所以结果就是子类里面的属性被拿到了**

```kt
fun main() {

    val son = Zi("Joeth")
    son.render()

    println()
    
    val dad = Fu("Tang")
    dad.render()
}


open class Fu (open val name: String) {
    
    open fun render() {
        println("Fu render")
        render2()
        println("Fu $name")
    }

    open fun render2() {
        println("Fu render2 $name")
    }

    init {
        render2()
    }
}


class Zi (override val name: String) : Fu(name + "Fu") {

    override fun render() {
        println("Zi render")
        super.render()
    }

    override fun render2() {
        println("Zi render2 $name")
    }
}
```

- 所以，***父类的构造器里面最好不要去调用 `open` 的方法，因为很可能此时这一个属性或方法还没有被子类初始化***

```kt
fun main() {

    val son = Zi("Joeth")
    son.render()
}


open class Fu (open val name: String) {
    
    open fun render() {
        println("Fu render")
        render2()
    }

    open fun render2() {
        println("Fu render2 $name")
    }

    init {
        render2()
    }
}


class Zi (override val name: String) : Fu(name) {

    override fun render() {
        println("Zi render")
        super.render()
    }

    override fun render2() {
        println("Zi render2 $name")
    }
}
```

> 没想到竟然是 null ，Kotlin 花了大功夫的空安全设计在这里失效了

- 这个问题在 Java 里面也存在，***如果父类构造器调用了被子类重写的方法，且通过子类构造函数创建子类对象，调用了这个父类构造器（无论显示还是隐式），就会导致父类在构造时实际上调用的是子类覆盖的方法***

- **优点就是实现了多态**，继承于同一父类下面的不同子类在父类的构造里面调用的是子类的方法，而缺点就是***如果这个被覆写的方法，在子类里面的实现涉及了子类的成员变量，恰恰这个时候子类的成员变量还没有被初始化，那么就会得到空指针异常***

```kt
fun main() {
    val son = Zi()
}



open class Fu  {

    open val name = "Fu"

    val id = getID()    // 这也是构造器的一部分。这个 getID 调用了子类的 getID
    
    init {
        println("Fu: id is $id, name is $name")
    }

    open fun getID(): Int {
        return 1000
    }
}


class Zi : Fu() {

    override val name = "Zi"

    init {
        println("Zi: id is $id, name is $name")
    }

    override fun getID(): Int {
        return name.length  // 这个 name 哪里来？
        // return super.name.length
        // return 1
        // 这两者均可以
    }

}
```

- 所以请注意，***父类的构造器不要调用可被继承的方法***，你不知道你的子类会不会访问一个自己无法初始化的属性

> 这还是一个运行时问题，编译时 Kotlin 不会指出你的问题，当然智能的 IDE 可以，但如果不注意这会是一个相当难找的问题

- 即便加上了显式的 `this` ，他仍会去调用子类的 `getter`，至于为啥见上文幕后字段

```kt
open class Fu(open val name: String) {
    init {
        println("Fu name is $name, this name is ${this.name}")

        // 你以为 this 获得的就是自己的？之前在幕后字段讲过，this 获得的也是 getName，所以一定小心
    }
}


class Zi(override val name: String) : Fu("Jackson") {
    init {
        println("Zi name is $name, this name is ${this.name}, super name is ${super.name}")
    }
}


fun main() {
val zi = Zi("Johnson")
}
```

### 7.6.4 父子类的转换

> 在上文我们看到一个父类的引用可以指向子类的对象，并且可以调用那些父子类共享的方法和属性，如果我想使用那些子类独有的呢？直接使用会报错，所以要进行类型转换

- ***指向子类对象的父类引用类型变量是可以转换为子类的引用的，前提是二者是父子关系***

- **这叫向下转型，相反的多态就是向上转型**

```kt
fun main() {
    val dad: Father = Son()

    dad.num = 40
    dad.printNum()
    
    val child: Son = dad as Son
    child.doSomething()
}


open class Father (open var num: Int = 10) {

    open fun printNum() {
        println("Father $num")
    }
}

open class Son (override var num: Int = 20) : Father() {

    override fun printNum() {
        println("Son $num")
    }

    fun doSomething() {
        println("Haha")
    }
}
```

- 但是，***子类的引用类型是不能接受一个父类的对象的***

> 就像汽车不一定都是小轿车一样，在逻辑上行不通

## 7.7 抽象

### 7.7.1 抽象类

- 当我们**需要一个方法却不知道它的具体表现形式，只能知道它的具体实例怎样使用它，我们可以干脆不构造它，这个叫抽象方法**

```kt
abstract fun func(num: Int): String

// 我只知道这个函数参数为 Int 返回值为 String，但是我不知道他怎样实现
```

- ***抽象类就是一个可以包含抽象方法和抽象属性的类，定义语法如下***

```kt
<修饰符> abstract class <类名字> {
    ···

    abstract fun func1() // 抽象方法

    fun func2() {
        // 方法
    }
}
```

- ***抽象类不能被构造***，所以***抽象类的继承就成了唯一使用途径***，抽象类的特点有：
    - ***抽象类不能构造对象***，但是**可以有构造方法**，问题是只能由子类来构造
    - ***抽象类当中不一定有抽象方法或属性，但是有抽象方法或属性的类必须被申明为抽象类***
    - ***一个类继承抽象类，那么这个类中必须实现抽象类中所有的方法。如果没有，那么这个类也要声明为抽象类***，也就是子类实现了父类的抽象方法，也就是***父类成了规范***，子类必须要实现（覆写）父类的全部抽象方法，否则它自己也是抽象的没法实例化
    - ***抽象类不能被申明为 final 类型***的，否则又要继承又不能继承岂不自相矛盾

- ***抽象的类、属性和方法默认都是 `open`*** 的，可以直接被继承

```kt
open abstract class myClass {
    oprn abstract fun func(num: Int): String
}

>>>warning: modifier 'open' is redundant in presence of 'abstract'.

// 他只是 warning ，不会拒绝编译
```

- **抽象类中可以定义正常的属性和方法**，使用上跟正常的类完全一样

- ***抽象方法不能有函数体，抽象属性可以为 `var` 和 `val`，不可以有 `getter` `setter` ，不能有初始值***

```kt
abstract class myClass {

    abstract fun abstractFunc(num: Int): String

    fun figurativeFunc(num: Int): String {
        return "num is $num in figurative func"
    }

    abstract var varNum: Int
    abstract val valNum: Int    // 因为没有初始值所以必须显示指定类型

    var num: Int = 21
        get() {
            return field + 100
        }
        set(value) {
            field = value + 200
        }
}
```

- ***抽象类可以继承抽象类，也可以继承正常类，抽象方法可以覆盖具象方法也可以覆盖抽象方法***

```kt
open class myClass {

    open var varNum = 10
    open val valNum = 30

    open fun abstractFunc(num: Int): String {
        return "func"
    }
}


abstract class abstractClass : myClass() {

    override abstract var varNum: Int
    override abstract val valNum: Int

    var num: Int = 21
        get() {
            return field + 100
        }
        set(value) {
            field = value + 200
        }

    override abstract fun abstractFunc(num: Int): String

    fun figurativeFunc(num: Int): String = "num is $num in figurative func"

}
```

```kt
fun main() {
    
    val kt = Kotlin()
    kt.sayHello()

    val coffee = Java()
    coffee.sayHello()
}


abstract class Language {
    
    abstract val name: String

    abstract fun sayHello()

}


class Kotlin : Language() {

    override val name = "Kotlin"

    override fun sayHello() {
        println("I'm $name, hello world!")
    }
}

class Java: Language() {

    override val name = "Java"

    override fun sayHello() {
        println("I'm Java, hello world!")
    }
}
```

> 因为抽象类本身也是个类，所以不支持多继承，简言之一个子类不能同时继承类和抽象类

### 7.7.2 接口

- ***接口就是一个完全抽象的抽象类，使用 `interface` 声明，默认 `open` 修饰***，可以直接被继承

> 接口本质上也是类，所以以一个引用类型的变量需要一个接口类型，如果你用这个接口的实现类传给他是可以的，如果是新手可能有点困惑

```kt
<修饰符> interface <类名字> {
    ···
}

// 默认 open
```

- ***接口中不允许定义属性，除非它没有幕后字段，或者是抽象的***（没错 Kotlin 支持抽象属性），属性默认 `open`

- ***接口中的方法的方法体也是可选的***，你可以写上然后在继承的时候就不用写了，方法默认 `open`，没有方法体的方法默认 `abstract open`

> 这种接口中的普通方法，本质上是创建了一个 $DefaultImpls.class ，在这个类里面实现了你在 Kotlin 接口里面的方法体

- ***接口不允许有构造方法***，所以在继承的时候***不能在接口名后面写括号***

> 抽象类是允许有构造函数的，只不过要交给子类去构造

```kt
fun main() {

    val myclass = MyClass()
    myclass.printNum()
    println(myclass.age)
}

interface User {
    abstract val num: Int

    // 抽象属性，不允许有初始值
    // 不用写这个 abstract 也行，因为属性默认就是 abstract 的

    val age: String
        get() = "age"

    // 这样就没有幕后字段了，也不能使用 field 了

    fun printNum() {
        println(num)

        // 方法体也是可选的，这样子其实这就是一个正常函数
        // 如果写成 abstract fun printNum 就不能有函数体了
    }
}


class MyClass : User {

    override val num = 20
    override val age = "48"

    /*
    override fun printNum() {
        println(num)
    }
    */

    // 因为接口中的这个方法不是抽象的，那么不覆盖也可以
}
```

- ***接口也可以继承接口，还可以实现覆写其他接口的实现，那么继承这个接口的类就不用覆写了***

> 接口中的覆写仅限于方法覆写，接口中还是不能定义属性

```kt

fun main() {
    val guy = Employee("Peter", "Benny", 40)

    println(guy.name)
}


interface Named {
    val name: String
}

interface Person : Named {
    val firstName: String
    val lastName: String

    override val name: String
        get() = "$firstName $lastName"

        // 对于这个 name ，它仍然是抽象的，只不过 get 被覆写了
}

class Employee(
    // 不必实现“name”
    override val firstName: String,
    override val lastName: String,
    val age: Int
) : Person
```

- 类和抽象类不支持多继承，因为无法避免冲突问题，但是接口里面都是抽象的方法和属性，所以***接口支持多继承***，**使用逗号 `,` 分隔不同的父类**

> Kotlin 只支持单继承的意思是一个**子类的超类列表里只能有一个有实例的父类**，也就是**抽象类和类只能二选一且唯一**，但是**可有无限多的接口**

```kt
fun main() {

    val myclass = MyClass()

    println(myclass.func(12))
    println(myclass.func(120L))
}

interface A {
    fun func(a: Int): String
}


interface B {
    fun func(b: Int): String

    fun func(c: Long): String
}


class MyClass : A , B { // 同时继承 A 和 B
    
    override fun func(num: Int): String = "$num in func(Int)"

    // 这个是两个里面共有的同名方法，一同覆盖掉

    override fun func(num: Long): String = "$num in func(Long)"

    // 加上这个后成了重载
}
```

- 上文中的方法都是抽象的，但如果两个方法是已经实现的，那么在调用的时候是分不清楚的，所以***使用 `super<接口名>.方法名(参数)` 的形式区分每个接口中已经实现的同名方法***

> 这个格式只能调用方法，不能覆写了，它的本质是：因为两个方法已经实现了，所以必须同时覆盖这两个，在覆写的方法体中去分别调用两个方法（不调用也行），就可以避免命名冲突

- Kotlin 里的继承规则是：***如果一个类从它的直接超类继承相同成员的多个实现， 它必须覆盖这个成员并提供其自己的实现（也许用继承来的其中之一）***

```kt
fun main() {

    val myclass = MyClass()

    println(myclass.func(12))
}

interface A {
    fun func(a: Int): String  = "$a in A.func(Int)"
}


interface B {
    fun func(b: Int): String = "$b in B.func(Int)"
}


class MyClass : A , B {

    override fun func(num: Int): String {
        val str1 = super<A>.func(num - 10)
        val str2 = super<B>.func(num + 10)

        println("override")

        return "$str1\n$str2"
    }
}
```

> 有没有多重继承的意思

- ***这种方法适用于任何实现了方法的接口***，都可以指定接口中方法的实现

> 比如我的类里面就想使用接口里面的方法体，我不想覆盖，但又想添加一些东西，就可以这样调用

```kt
fun main() {

    val myclass = MyClass()

    println(myclass.func(12))
    println()

    myclass.function()
}

interface A {
    fun func(a: Int): String  = "$a in A.func(Int)"
}


interface B {
    fun func(b: Int): String = "$b in B.func(Int)"

    fun function() {
        println("interface")
    }
}


class MyClass : A , B {

    override fun func(num: Int): String {
        val str1 = super<A>.func(num - 10)
        val str2 = super<B>.func(num + 10)

        println("override")

        return "$str1\n$str2"
    }

    override fun function() {
        super<B>.function()

        println("class")
    }
}
```

### 7.7.3 函数式接口

- Kotlin 也支持函数式接口（SAM，Simple Abstract Method），***使用 `fun interface` 声明函数式接口***，这种接口可以有多个实现的函数，但是***只能有一样个抽象方法***

> Java 里面使用 `SAM` 是因为没有高阶函数，Kotlin 多数情况下推荐使用 `lambda` 表达式，当然与 Java 互操作的时候下面会讲

```kt
fun interface MyInterface {
    fun doSomething()
}
```

- 在实现 `SAM` 的时候可以***使用 `SAM` 转换简化代码***

```kt
fun interface IntPredicate {
   fun accept(i: Int): Boolean
}

// 一般情况下
val isEven = object : IntPredicate {
   override fun accept(i: Int): Boolean {
       return i % 2 == 0
   }
}

// 使用 lambda 简化后
val isEven = IntPredicate { it % 2 == 0 }

fun main() {
   println("Is 7 even? - ${isEven.accept(7)}")
}

```

## 7.8 内部

### 7.8.1 嵌套类

- ***类可以定义在另一个类的内部，这个时候这个类叫做嵌套类***

> 嵌套类本质上***就是 Java 里的静态内部类***，因为 Kotlin 没有 `static` 关键字，所以把它改名叫做了嵌套类

- ***因为嵌套类是静态的，所以无需构造外部类的对象即可使用，嵌套类不能访问外部类的方法和属性，但是是可以访问其他嵌套类的***

```kt
fun main() {
    val nes1 = Outer.Nested1(99)
    val nes2 = Outer.Nested2(nes1, 88)

    // 记住这里外部类不需要构造

    nes2.printNum()
}


class Outer (val int: Int = 10) {
    
    fun printInt() {
        println(int)
    }


    open class Nested1 (open val num: Int = 20) {

        open fun printNum() {
            println(num)
            // printInt(int) 是不行的，因为它在静态区域，它不能保证自己被创建的时候外部类已经被创建了
        }
    }

    // 嵌套类当然可以继承嵌套类
    class Nested2 (val clas: Nested1, override val num: Int) : Nested1(num - 11) {
        override fun printNum() {
            clas.printNum()
            println(num)
            println(super.num)
        }
    }
}
```

- ***还可以使用带有嵌套的接，所有类与接口的组合都是可能的***：可以将接口嵌套在类中、将类嵌套在接口中、将接口嵌套在接口中


```kt
fun main() {
    
    val outer = OuterClass()
    val inner = OuterClass.InnerClass()

    outer.printMessage()
    inner.printMessage()
}


interface OuterInterface {

    class InnerClass {

        fun printMessage() {
            println("OuterInterface.InnerClass")
        }
    }

    interface InnerInterface {

        fun printMessage() {
            println("OuterInterface.InnerInterface")
        }
    }

    open fun printMessage() {
        println("OuterInterface")
    }
}


class OuterClass : OuterInterface {
    class InnerClass : OuterInterface , InnerInterface { // 可以不加 OuterClass 的前缀，因为它可以访问到

        override fun printMessage() {
            super<OuterInterface>.printMessage() // 注意 OuterInterface 会被打印两边，因为他同时被 OuterClass 和 InnerClass 调用
            super<InnerInterface>.printMessage()
            println("OuterClass.InnerClass")
        }
    }

    interface InnerInterface {

        fun printMessage() {
            println("OuterClass.InnerInterface")
        }
    }

    override fun printMessage() {
        super<OuterInterface>.printMessage()
        println("OuterClass")
    }
}
```

### 7.8.2 内部类

> 内部类才是真正 Java 里的成员内部类

- ***内部类需要使用 `inner` 修饰，定义在类的内部与属性和方法同级***，本质上内部类会带有一个对外部类的对象的引用，***作为外部类的成员是可以访问外部类的 `private` 属性和方法，使用他之前必须先构造外部类的对象***

> 外部类不能访问内部类，因为它不能保证自己被创建的时候内部类也被创建了，但是它可以声明一个内部类的对象

> 内部类能访问外部类的私有成员，是因为它本身也是外部类的成员

```kt
fun main() {
    println(Outer().Inner().foo())
    // 外部类必须有构造
}


class Outer (private val bar: Int = 1) {
    
    inner class Inner {
        fun foo() = bar
    }
}
```

- 那**如果内部类的属性和外部类的属性同名该怎样区分？** Kotlin 里的 `this` 功能很强大，**默认指的是最内层的包含它的作用域**，要引用其他作用域中的 `this`，***在 `this` 后面加上隐性的标签就可以指定作用域访问***

```kt
fun main() {
    Outer().Inner().foo(3)
    Outer().inn.foo(4)
    Outer().useInner()

    // 其实不建议写成这样，但是这里方便演示写成了表达式的样子
}


// 可以在这里加上自定义的标签
// 类名就是默认隐式的 @Outer
class Outer (private val bar: Int = 1) {
    
    val inn = Inner()


    inner class Inner { // @Inner
        private val bar = 2

        fun foo(bar: Int) {
            val a = this@Outer.bar  // 指定外部类的this，所以调用的是外部类的私有属性
            val b = this@Inner.bar  // 指定 this 为Inner
            val c = bar             // 不指定本地优先，选择函数的本地变量，也就是参数

            println("a is $a\nb is $b\nc is $c\n")
        }
    }

    fun useInner() {
        inn.foo(5)
        // println(inn.bar)
        // 内部类可以访问外部类的私有属性，可是反过来不行
    }
}
```

### 7.8.3 局部内部类

- 除此以外，还可以***把类定义在方法（函数）内***，这样的类***叫做局部内部类***，他***只能在函数内部定义和创建***，因此也***不能有权限修饰符***，出了函数后就访问不到了

```kt
fun main() {

    abstract class LocalInnerClass {
        // 可以有局部抽象类，但是不能有局部接口
        abstract fun printMsg()
        // 抽象类可不会自动给方法加上抽象前缀 
    }

    class LocalInnerClassDerive : LocalInnerClass() {

        override fun printMsg() {
            println("LocalInnerClass")
        }
    }


    val lic = LocalInnerClassDerive()
    lic.printMsg()
}
```

- **当对 `this` 调用成员函数时，可以省略 `this.` 部分，这叫隐式的接收者**，但是如果有一个同名的非成员函数时，请谨慎使用，因为**在某些情况下会调用同名的非成员**

```kt
fun main() {
    fun printLine() { println("Top Level function") }

    class A {
        fun printLine() { println("Member function") }

        fun invokePrintLine(omitThis: Int)  {
            when {
                omitThis == 0 -> printLine()
                omitThis == 1 -> this.printLine()
                omitThis == 2 -> this@A.printLine()
            }
        }
    }

    A().invokePrintLine(0)
    A().invokePrintLine(1)
    A().invokePrintLine(2)
}
```

## 7.9 object 对象

### 7.9.1 匿名类

> 我们经常会遇到一种情况，有一个函数需要一个接口的实现，那么难道我们还要声明一个只使用一次的类？可以使用匿名类

- Kotlin ***使用 `object` 对象表达式（Object expression）创建一个匿名类的对象***，在后面的花括号里面写上类体，注意***不能有构造***

> 这个 `object` 是关键字不是 Java 里面那个 `Object`，Kotlin 里面叫 `Any`

```kt
fun main() {
    val helloWorld = object {
        val hello = "Hello"
        val world = "World"

        override fun toString() = "$hello $world"

        // 因为任何没有显式声明超类的类默认继承 Any，所以对于 toString 方法需要覆盖
    }

    print(helloWorld)
    
    // 一样，打印一个东西是在调用 toString 方法
}
```

- 也**可以声明匿名类的父类**，声明方法跟类的继承一样，多继承接口用逗号隔开，类的构造在括号里写明

```kt
fun main() {
    val helloWorld = object : Message,  Printer("Printer") {

        override val hello: String = "Hello"
        override val world: String = "World"


        override fun printSomething() {
            println(super.hello)
            
            // 这个 super 拿到的是父类 Printer 的，接口根本没有实例不会有冲突
            // 对于同时继承接口和抽象类或类的子类，使用 super 拿到的一定是非接口的那个
            println(hello)
        }
    }

    helloWorld.printSomething()
}


open class Printer(open val hello: String) {

    open fun printSomething() {
        println(hello)
    }
}


interface Message {

    val hello: String
    val world: String
}
```

- 当***匿名对象用作本地或私有但不是内联（函数或属性）的类型时，其所有成员都可以通过该函数或属性进行访问***

```kt
class C {
    private fun getObject() = object {
        val x: String = "x"
    }

    fun printX() {
        println(getObject().x)
    }
}
```

- 但如果该***函数或属性是公开或私有内联***的，则它实际的类型是：
    1. ***`Any` 如果匿名对象没有声明的超类型***
    2. ***匿名对象的声明超类型***（如果正好有一个这样的类型）
    3. ***显式声明的类型***（如果有多个已声明的超类型）

- 在所有这些情况下，***匿名对象中添加的成员都无法访问***，但是**可以访问被覆盖的成员**

```kt
interface A {

    fun funcFromA() {
        println("funcFromA")
    }
}


interface B {

    fun funcFromB() {
        println("funcFromB")
    }
}


class C {
    
    // 实际类型为 Any ，x 无法访问
    fun getObject() = object {
        val x = "x"
    }

    
    // 实际类型是 A 的子类，所以没有在 A 中出现的 x 访问不到    
    fun getObjectA() = object : A {
        override fun funcFromA() {
            println("get object A ${super<A>.funcFromA()}")
        }

        val x = "x"
    }

    // 实际类型是 B ，所以 funcFromA 和 x 都访问不到
    fun getObjectB(): B = object : A, B{
        override fun funcFromA() {
            println("get object B ${super<A>.funcFromA()}")
        }

        override fun funcFromB() {
            println("get object B ${super<B>.funcFromB()}")
        }
        
        val x = "x"
    }
}
```

- 还有一点，**对象表达式中的代码可以访问并修改来自包含它的作用域的变量**

```kt
fun countClicks(window: JComponent) {
    var clickCount = 0
    var enterCount = 0

    window.addMouseListener(object : MouseAdapter() {
        override fun mouseClicked(e: MouseEvent) {
            clickCount++
        }

        override fun mouseEntered(e: MouseEvent) {
            enterCount++
        }
    })
    // ……
}
```

### 7.9.2 单例类对象声明

> 有的时候我们想限制一个类只能产生一个实例对象，那么在 Java 里面我们可能会使用什么懒汉式或是饿汉式的写法创建单例，构造私有导致无法外部 new，一个静态属性指向对象（饿汉式直接 new ，懒汉式先是 null），静态的 getInstance 方法获取静态属性的指向

> Kotlin 里面很简单

- ***使用 `object` 后面接上类名，就创建了一个只能创建一个对象的单例类***，这种写法也叫***对象声明***（Object declaration）

- 如果使用的话*直接类名加属性或方法名*，就**跟静态写法一样**，无需创建对象

> 这个 `object` 可不是对象表达式里面的那个，那个没有类名是匿名类，这个是单例类，这个因为是语句所以不能放在赋值语句的右面

- 这种写法**不会立即初始化**，直到你第一次访问的时候，但是缺点就是***不能有构造方法***，可以把需要初始执行的语句放在 `init` 里面简单代替下

```kt
fun main() {
    println("not initialized yet")

    Singleton.name = "Peter"
    // 在你第一次访问的时候初始化，可以看到 init 先被打印出来，然后是 set 里面的 print
    Singleton.printName()
}

object Singleton {

    var name: String = "name"
        set(value) {
            field = value
            println("name set")
        }

    fun printName() {
        println("$this name is $name")
    }

    init {
        println("$this is initialize")
    }
}
```

> 通过反编译的源码可以看到，实际上这是一个我们所谓饿汉式的写法，并且里面的成员已经成了静态的，并且**线程安全**


```java
public final class Singleton {
   @NotNull
   public static final Singleton INSTANCE = new Singleton();
   @NotNull
   private static String name = "name";

   private Singleton() {
   }

   @NotNull
   public final String getName() {
      return name;
   }

   public final void setName(@NotNull String value) {
      Intrinsics.checkNotNullParameter(value, "value");
      name = value;
   }

   public final void printName() {
      System.out.println(this + " name is " + name);
   }

   static {
      System.out.println(INSTANCE + " is initialize");
   }
}

```

- ***对象声明不能在局部作用域***（即不能直接嵌套在函数内部），但是它们可以嵌套到其他对象声明或非内部类中

- ***`object` 也是可以继承的***，无论是接口还是类

```kt

interface A {
    fun interfaceFunc()
}

open class B() {
    open fun classFunc() {
        println("classFunc")
    }
}

object Singleton : A, B(){

    override fun classFunc() {
        println("classFunc impl")
    }

    override fun interfaceFunc() {
        println("interfaceFunc impl")
    }
}

```

### 7.9.3 伴生对象

> 因为有顶层函数，顶层变量（常量），对象声明，所以 Kotlin 取消了 ststic 关键字，可是有些时候我们还是需要 static，比如在一个类的里面既有非静态的方法和属性，又有静态方法和属性，这个时候使用对象声明就不够用了

- 我们可以***把对象声明在一个类里面，那么这个对象声明里面的所有成员都可以看作是这个类的静态成员***

```kt
fun main() {

    val sing = SingletonClass("Hanson")
    sing.name

    val single = SingletonClass("Douglas")
    single.name

    println("Singleton class is loaded ${SingletonClass.Static.times} times total")
    // 可以直接通过类名的方式访问，这不就是静态成员？
}


class SingletonClass(name: String) {

    val name: String = name
        get() {
            println("name is $field, it's loaded ${Static.times}")
            
            return field
        }

    init {
        println("Singleton class is loaded ${Static.times} before")
        Static.times++
        // 类里面的其他地方也可以访问到对象里面的静态成员
    }


    object Static {
        var times = 0   // 静态属性

        // 这就是静态初始化块，它只会在类的第一次初始化时被加载
        init {
            println("static init is loaded")
        }
    }
}
```

> 这个对象声明不要把它看作是类里面的单例类，就把他看作是静态成员就行，虽然它也可以嵌套

```kt
object Sta1 {
    object Sta2 {
        object Sta3 {
            const val greeting = "congregations you have found me"
        }
    }
}

println(SingletonClass.Static.Sta1.Sta2.Sta3.greeting)
```

- 如果觉得限定名很麻烦，可以加上 ***`companian object` （伴生对象） 的前缀，这样就可以省略掉限定名直接用类名访问***

> 这个**伴生对象默认的对象名是 `Companion`**

- 一个***类里面只能有一个伴生对象***，但是**可以有无数多的具名对象，二者也都可以内部再定义对象**（见上）

```kt
class TopLevelClass {

    companion object {
        fun doSomeStuff() {
            // ...
        }
    }

    object FakeCompanion1 {
        fun doOtherStuff() {
            // ...
        }
    }

    object FakeCompanion2 {
        fun doOtherStuff() {
            // ...
        }
    }
}

fun testCompanion() {
    TopLevelClass.doSomeStuff()
    TopLevelClass.Companion.doSomeStuff()
    TopLevelClass.FakeCompanion1.doOtherStuff()
    TopLevelClass.FakeCompanion2.doOtherStuff()
}
```

```kt
fun main() {

    // 不用创建对象就可以访问函数
    println("Singleton class is loaded ${SingletonClass.times} times total")

    val sing = SingletonClass("Hanson")
    sing.name

    val single = SingletonClass("Douglas")
    single.name

    println("Singleton class is loaded ${SingletonClass.times} times total")
}


class SingletonClass(name: String) {

    val name: String = name
        get() {
            println("name is $field")

            return field
        }

    init {
        println("Singleton init ${times} before")
        times++
    }


    companion object {
        var times = 0

        init {
            println("static init")
        }
    }
}
```
> 到此，Kotlin 里面为了使用顶层声明、对象声明和伴生对象彻底干掉了 static 关键字

> 还有一点，对于 `val` 的静态变量，可以声明为 ***`const val`***，这点上面讲过只不过那时候还只能***声明在顶层***，现在多了两个选择，***声明在对象声明里和伴生对象里***，这三种情况下都是静态的

- 上面说过，`object` 声明的单例类，一旦访问其中的成员就会初始化，而且不能有普通成员，现在有了 `companion object` 之后可以对其改进

```kt
fun main() {
    val sing = Singleton.getIns()
    sing.name = "Peter"
    sing.age = 30
    sing.printMsg()

    val sing1 = Singleton.getIns()
    sing1.name = "Joe"
    sing1.age = 40
    sing1.printMsg()
    // 说明指向的是同一个对象。单例
    sing.printMsg()
}


class Singleton private constructor() {

    var name = "null"
    var age = 0

    fun printMsg() {
        println("name is $name, age is $age")
    }

    companion object {
        private var instance: Singleton? = null
            get() {
                if (field == null) {
                    field = Singleton()
                } else {
                    println("singleton has been created")
                }
                return field
            }

        // 因为 get 里面可能会出先多线程同时创建，所以在这里可以加上互斥锁保证线程安全
        fun getIns(): Singleton {
            return instance!!
            // 这里如果不是断言的话，那么 main 里面所有的都要该
            // 反正也永远不可能返回一个空的出去，所以直接!!
        }
    }
}
```

- 而且可以做到**带参数的单例**，成功解决了之前 `object` 的问题

```kt
fun main() {
    val sing = Singleton.getIns("Peter", 30)
    sing.printMsg()

    val sing1 = Singleton.getIns()
    sing1.name = "Jo"
    sing1.age = 35
    sing1.printMsg()
    sing.printMsg()
}


class Singleton private constructor(var name: String, var age: Int) {

    fun printMsg() {
        println("name is $name, age is $age")
    }

    companion object {
        private var instance: Singleton? = null

        fun getIns(name: String, age: Int): Singleton {
            if (instance == null) {
                instance = Singleton(name, age)
            } else {
                println("singleton has been created")
            }

            return  instance!!
        }
        
        // 方便重载
        fun getIns(): Singleton {
            return instance!!
        }
    }
}

// 如果你不加锁的话，这种写法是可能遇到多次创建的情况，前提时多线程
// 关于双重线程锁的单例，后面会讲
```

- 虽然伴生对象看起来就是静态成员，但是它实际上还是 Kotlin 的对象，比如**伴生对象可以继承接口**

```kt
interface Factory {
    fun create()
}

class MyClass {
    companion object : Factory {
        override fun create() {
            println("create")
        }
    }
}
```

- 去看编译后的字节码，可以知道其实***伴生对象就是一个静态内部类***，无需外部类的对象就能访问

- ***伴生对象的属性的字段是静态字段，保存在伴生对象所在的类当中，但是该字段的 `get` 方法位于伴生对象里***，所以需要一个类才能去访问这个静态字段

- ***伴生对象的方法直接位于伴生对象所在的静态内部类，但是它不是静态的***，你也需要构一个类才能去使用它，唯一的例外是 ***`init {}` ，它仍然是静态初始化块***

- 伴生对象所在类有一个静态字段指向一个 `new` 出来的伴生对象，每一次调用伴生对象里的成员时都是在访问同一个静态内部类的实例，所以***伴生对象也是单例***

```kt
// MyClass.java

public final class MyClass {
   @NotNull
   public static final Companion Companion = new Companion((DefaultConstructorMarker)null);
   private static final int myCompanionVal = 20;
   @NotNull
   private static String myCompanionVar = "World";

   
   public static final class Companion {
      private Companion() {
      }

      public final void myCompanionFun() {
         String var1 = "I'm a companion function";
         System.out.println(var1);
      }

      public final int getMyCompanionVal() {
         return MyClass.myCompanionVal;
      }

      @NotNull
      public final String getMyCompanionVar() {
         return MyClass.myCompanionVar;
      }

      public final void setMyCompanionVar(@NotNull String var1) {
         Intrinsics.checkNotNullParameter(var1, "<set-?>");
         MyClass.myCompanionVar = var1;
      }

      // $FF: synthetic method
      public Companion(DefaultConstructorMarker $constructor_marker) {
         this();
      }
   }
}
// MainKt.java


public final class MainKt {
   private static final int topVal = 10;
   @NotNull
   private static String topVar = "Hello";

   public static final void topFun() {
      String var0 = "I'm a top level function";
      System.out.println(var0);
   }

   public static final int getTopVal() {
      return topVal;
   }

   @NotNull
   public static final String getTopVar() {
      return topVar;
   }

   public static final void setTopVar(@NotNull String var0) {
      Intrinsics.checkNotNullParameter(var0, "<set-?>");
      topVar = var0;
   }

   public static final void main() {
      topFun();
      int var0 = topVal;
      System.out.println(var0);
      String var1 = topVar;
      System.out.println(var1);
      MyClass.Companion.myCompanionFun();
      var0 = MyClass.Companion.getMyCompanionVal();
      System.out.println(var0);
      var1 = MyClass.Companion.getMyCompanionVar();
      System.out.println(var1);
   }

   public static void main(String[] args) {
      main();
   }
}
```

- ***位于顶层的函数和属性，其位于 `文件名kt.class` 里，都是静态的***，无论字段还是访问器

> 又多了一个不使用伴生对象的理由

- 还有一件事，**静态方法和属性能被继承吗**？因为静态变量和方法存储于专门的空间，因此即便是继承了也无法访问 `super` `this`，这我们之前讲过，即便是继承了也没什么用

- 还有，***多态也无法应用于静态成员，因为静态成员是静态绑定的***，多态的时候回去看变量的类型，而且基本上没人会去拿实例调用静态方法

- 所以***静态成员也不能被覆盖***

> 而且因为 Kotlin 奇怪的伴生对象的实现，你***没法在一个实例上调用类中的静态成员***，Java 是可以的

```kt
open class Fu {
    companion object {
        open fun hello() {
            println("Hello from Fu")
            // warning: 'open' has no effect on object.
            // 这里提示你 open 在对象上没有效果，因为对象是静态的，所以 open 也没有意义
        }

        open val name: String = "Fu"
    }
}

class Zi : Fu() {
    companion object {
        fun hello() {
            println("Hello from Zi")
            // 不能 override
        }

        val name: String = "Zi"
    }
}

fun main(args: Array<String>) {
    val f: Fu = Fu()

    // f.hello() 不行的
    Fu.hello()
}
```

- 对象表达式和对象声明之间有一个重要的语义差别：
    1. ***对象表达式是在使用他们的地方立即执行（及初始化）的***
    2. ***对象声明是在第一次被访问到时延迟初始化的***
    3. ***伴生对象的初始化是在相应的类被加载（解析）时***，与 Java 静态初始化器的语义相匹配

> 什么时候使用伴生对象，什么时候使用顶层声明呢，对于一般的方法，反正***静态成员也不能访问正常成员***，你还不如写成顶层声明的样子

> 而像静态初始化块，保留信息的静态方法，那就只能使用伴生对象了

## 7.9 扩展

- Kotlin 可以***对一个现成的类或接口扩展新的方法或或属性***而不需要继承或是其他设计模式，这种新增的成员可以被对象正常的调用，这叫**扩展方法（extension function）和扩展属性（extension property）**

### 7.9.7 扩展方法

- ***声明一个扩展方法，只需在函数名的左面写上 `类名.` ，那么这个函数就只能被这个类的对象所调用了***

```kt
fun main() {
    val userInput = readln().toULong()
    // 忘了讲 readln 就是用来读取用户输入的
    
    println(userInput.factorial())
    // 对于任何一个 ULong 类型的变量都可以使用此函数
}


fun ULong.factorial(): ULong {  // ULong 的扩展函数

    var result: ULong = 1uL

    for (i in this downTo 1uL) result *= i
    // 甚至可以访问 this ，就跟类里面的成员函数一样

    return result
}
```

- 本质上扩展函数就是普通的函数（普通函数的特性大部分他都有），如果**声明在顶层则该包内的文件都可以访问它，它也可以访问同一文件中的其他 `private` 顶层声明**，只是它***左面的接收者限定了这个函数只能被这个接收者类型的对象调用***

> 这里我们只讨论位于顶层的扩展函数，更多见下文引用篇

```kt
// 导入

// Main.kt

package com.lightko.kotlin
import com.lightko.kotlin.printFactorial // 顶层声明属于包

fun main() {
    23uL.printFactorial()
}


fun ULong.factorial(): ULong {

    var result: ULong = 1uL

    for (i in this downTo 1uL) result *= i

    return result
}


// Test.kt

package com.lightko.kotlin
import com.lightko.kotlin.factorial // 直接导入，不需要加上接收者类型

fun ULong.printFactorial() { println(this.factorial())}

// kotlinc com\lightko\kotlin\Main.kt com\lightko\kotlin\Test.kt
// kotlin com\lightko\kotlin\MainKt.class
```

- ***如果扩展是在其接收者类型外部声明的，那么它不能访问接收者的 `private` 或 `protected` 成员***，这一点不像是类的原生成员

- 实际上扩展函数并没有修改类本身，所以***扩展函数是静态绑定的***，也就是***没有多态***，见下面

```kt
fun main() {
    printClassName(Rectangle())
}


open class Shape
class Rectangle: Shape()

fun Shape.getName() = "Shape"
fun Rectangle.getName() = "Rectangle"

fun printClassName(s: Shape) {
    println(s.getName())
    
    // 理论上传入一个 Shape 的子类，调用的应该是子类的方法
    // 可是扩展方法没有多态
}
```

- 而且也不能与原有类中的方法同名，也就是***扩展方法不能重写覆盖原有类中的方法***

- 但是***扩展函数仍然可以重载***

```kt
fun main() {
    Animal().getName()
    Animal().getName(1)
}

class Animal {
    fun getName() {
        println("Animal")
    }
}

fun Animal.getName(i: Int) {
    println("Hi!")
}

```

- 可是在一种情况下重载会失效，***当扩展方法重载原有方法，并且二者的参数呈父子关系时，一定会去调用原有类的方法，不会去调用扩展方法***

```kt
fun main() {
    val mcs = MyClass()
    mcs.getItsName(Animal("Pete"))
    mcs.getItsName(Dog("Thomas"))   // 调用 MyClass 里面的而不是扩展

}

open class Animal(open val name: String)


class Dog(override val name: String) : Animal(name)


class MyClass {
    fun getItsName(animal: Animal) {
        println("Animal name is ${animal.name}")
    }
}


fun MyClass.getItsName(dog: Dog) {
    println("Dog name is ${dog.name}")  // 不会打印
}
```

> 这一切限制都是为了保证基类不受影响，所以用扩展方法的时候请慎用，不要随意使用，否则会破坏代码完整性

- 还***可以扩展可空的方法调用***，这样**即使源类没有可空方法，但是使用一个 `null` 的对象仍可以正常调用**，不过要做好非空判断

> 官方叫 ***可空接收者的扩展***

> 因为一般可空的对象要想调用非空的方法，必须加上 `?.` 安全调用，这里设置一个可以接受可空对象的方法就不需要了

```kt
fun main() {
    var animal: Animal? = Animal()
    animal.getName()
    // animal.getName(2) 不安全

    animal = null
    animal.getName()

}

class Animal {
    fun getName(i: Int) {
        println("Animal $i")
    }
}

fun Animal?.getName() {
    if (this == null)  println("null!") else this.getName(1)
    // 编译器知道经过判断后后面的 this 一定是非空的，所以可以正常使用
}
```

- ***还可以扩展伴生对象的成员***，使用方法同上

```kt
class MyClass {
    companion object { }  // 将被称为 "Companion"
}

fun MyClass.Companion.printCompanion() { println("companion") }

fun main() {
    MyClass.printCompanion()
}
```

### 7.9.2 扩展属性

- 也可以扩展已有类的属性，不过由于扩展没有实际的将成员插入类中，所以***扩展属性不能有幕后字段***

```kt
fun main() {

    val mcs = MyClass()
    println(mcs.name) // 记得我们说过的，访问变量就是 getter
    mcs.age = 12      // 赋值就是 setter
    println(mcs.age)
}

class MyClass

val MyClass.name: String
    get() { return "name" }

var MyClass.age: Int
    get() { println("age") ; return 1}
    set(value) { println("set") }

// 二者均没有幕后字段，编译后不会生成属性，至于幕后字段的限制见上文
```

- **大部分时候扩展属性比扩展方法更方便，类似对变量的操作可以替代各种 `set get` 方法**，Kotlin 本身就对 Java 的一些工具方法设置了扩展属性，我们后面也能看到

### 7.9.3 中缀表达式

- 对于上面扩展方法的常规调用写法，Kotlin 还提供了一个更为直观的调用方法，***使用中缀 `infix` 修饰的单参数成员方法和扩展方法，在调用时可以使用 `对象 方法名 参数` 的形式调用***

> 注意，***必须是成员方法和扩展方法，而且是单参数，参数不能是可变参数或默认参数的函数的才能被 `infix` 修饰***

> 像是 for 里的 downTo 和 step 就是中缀函数，所以使用起来像是关键字的样子

```kt
fun main() {

    println(1 sum 100)
    println(225 sum 980)
}


infix fun Int.sum(end: Int): Int{

    var result = 0

    for (i in this..end) {
        result += i
    }

    return result
}
```

> 也等同于下面的

```kt
fun main() {

    println(1.sum(100))
    println(225.sum(234))
}


fun Int.sum(end: Int): Int{

    var result = 0

    for (i in this..end) {
        result += i
    }

    return result
}
```

### 7.9.4 操作符重载

- ***Kotlin 里面的运算符，除了对一般的基本类型进行运算，也允许我们对非原生类型自定义的操作符的实现***，这样子就可以对我们自定义的类型方便的使用 `+ - * /` 而不是无聊的调用方法

- 如果想***声明一个重载操作符的方法，使用 `operator` 前缀修饰方法***，这样该方法位于的类的对象之间就可以使用运算符进行操作了

> [Kotlin 操作符对应方法](https://book.kotlincn.net/text/operator-overloading.html)，在这里了解每一个操作符自己对应的方法名称

```kt
// 一个坐标类

import kotlin.math.abs
import kotlin.math.sqrt
import kotlin.math.pow

// 这些导入的包之后讲

class Coordinate (val x: Double, val y: Double) {

    override fun toString(): String {
        return "Coordinate at $x , $y, The distance from the origin is ${sqrt(abs(x).pow(2) + abs(y).pow(2))}"
    }

    // 直接打印距离原点的距离
}
```

- 比如对上面的坐标类，我们想实现对两个对象间的运算不使用方法调用的格式，就可以使用操作符重载

```kt
fun main() {

    val point = Coordinate(12.434, 321.432)
    println(point)
}


class Coordinate (val x: Double, val y: Double) {

    //加法(+)
    operator fun plus(other: Coordinate): Coordinate {
        return Coordinate(x + other.x, y + other.y)
    }

    //减法(-)
    operator fun dec(): Coordinate {
        return Coordinate(x - other, y - other)
    }

    //乘法(*)
    operator fun times(other: Coordinate): Coordinate {
        return Coordinate(x * other.x, y * other.y)
    }

    //除法(/)
    operator fun div(other: Coordinate): Coordinate {
        return Coordinate(x / other.x, y / other.y)
    }

    //取模(%)
    operator fun rem(other: Coordinate): Coordinate {
        return Coordinate(x % other.x, y % other.y)
    }

}
```

- 在调用时，可以直接使用运算符操作二者

```kt
fun main() {

    val point1 = Coordinate(12.1, 2.5)
    val point2 = Coordinate(5.4, 7.9)
    println(point1)
    println(point2)

    println("--------------------------------")

    println("加: ${point1 + point2}")
    println("减: ${point1 - point2}")
    println("乘: ${point1 * point2}")
    println("除: ${point1 / point2}")
}
```

> 关于每一种操作符的重载，可以见这篇[CSDN 文章](https://blog.csdn.net/yuzhiqiang666/article/details/86706874)，这种重复量高的工作我就不复制了，这篇文章里对于每一种操作符都做了说明，应该是容易理解的

> 文章错误较多，我也不校正它了，看的时候不要照抄，还是建议看上面的官方文档

> `[]` `..` `.invoke()` 都可以重载

```kt
import kotlin.math.abs
import kotlin.math.sqrt
import kotlin.math.pow


fun main() {
    val point1 = TwoDimensionalCoordinateSystem(34.34,67.5657)
    val point2 = TwoDimensionalCoordinateSystem(345.234,432.67)
    val point3 = TwoDimensionalCoordinateSystem(345.234,432.67)
    val point4: TwoDimensionalCoordinateSystem? = null

    println(point2 == point3)
    println(point2 === point3)
    println(point2 == point4)

    println(point1.hashCode())
    println(point2.hashCode())
    println(point3.hashCode())
    println(point4.hashCode())

}


class TwoDimensionalCoordinateSystem(val x: Double, val y: Double) {


    fun distanceFromTheOrigin(): Double = sqrt(abs(x).pow(2) + abs(y).pow(2))


    //  自增自减运算符，应该返回新的对象而不是修改原有的
    operator fun inc(): TwoDimensionalCoordinateSystem {
        return TwoDimensionalCoordinateSystem(
            x = this.x + 1,
            y = this.y + 1
        )
    }


    // 二元运算符，加减乘除余，还有区间运算符 .. ..<
    operator fun plus(another: TwoDimensionalCoordinateSystem): TwoDimensionalCoordinateSystem {
        return TwoDimensionalCoordinateSystem(
            x = this.x + another.x,
            y = this.y + another.y
        )
    }


    // 比较运算符只需要写一个，< > <= >= 只是根据你返回的值进行推断
    operator fun compareTo(another: TwoDimensionalCoordinateSystem): Int = when {
            this.distanceFromTheOrigin() < another.distanceFromTheOrigin() -> (this.distanceFromTheOrigin() - another.distanceFromTheOrigin()).toInt()
            this.distanceFromTheOrigin() > another.distanceFromTheOrigin() -> (this.distanceFromTheOrigin() - another.distanceFromTheOrigin()).toInt()
            this.distanceFromTheOrigin() == another.distanceFromTheOrigin() -> (this.distanceFromTheOrigin() - another.distanceFromTheOrigin()).toInt()
            else -> 0 // 必须有一个 else 分支
    }

    // 重写 equals 就相当于重写 == ，因为 == 对于非原生类型就是在调用 equals
    // 这个 equals 并不需要保证两个引用指向的对象一样（===），只需要保证二者的值（比如类里的属性）一样
    // 如果不重写，那么上面的结果会是 point2 == point3 是 false
    override fun equals(another: Any?): Boolean {

        if (another is TwoDimensionalCoordinateS ystem) {
            if (another.x == this.x && another.y == this.y) {
                // 这里前面判断过可以保证这里的 another 一定非空而且是 TDCS 的类或子类
                return true
            }
        }

        return false
    }

    // === 不可重载
    // 重写 equals 就要重写 hashcode，是因为哈希表需要两个对象如果 equals 相等，则 hashcode 也要相等
    // hashcode 本身看下面的算法也知道它也一种对象属性的值，在哈希表里面如果发生冲突，那么会用拉链法解决
    // 所以，equals 相等则 hashcode 也要相等，反之亦然，因为如果二者相等但是索引却不一样，不是浪费？
    // 但是 equals 不等，或是 hashcode 不等，另一者不一定也不等，因为哈希表的算法
    // 如果注释掉这里，你会发现 point2 和 point3 equals 但是 hashcode 却不等，这时从父类继承来的 hashcode 不能适应我们的类
    // 至于为什么这里都是 31 乘上自身再加上属性哈希值，因为 31 是素数同时也是 2^5 -1 ，任何数 n 乘 31 都是这个数乘 2^5 减去自身，对于计算机来说可以直接移位计算（移位就相当于乘除 2 的 n 次方），速度较快
    // > n * 31 = n * (2^5 - 1) = n * 2^5 - n = n << 5 - n
    override fun hashCode(): Int {
        var result = x.hashCode()
        result = 31 * result + y.hashCode()
        return result
    }
}
```

- 同理**也可以使用扩展函数对现有的类进行操作符重载**

```kt
operator fun Point.plusAssign(other: Point) {
        x += other.x
        y += other.y
}
```

## 7.10 初识委托

> 委托（delegate）是一种设计模式，有些时候我们想在继承的时候只关心自己新方法的定义，而不关心被覆写方法的实现，就可以使用委托模式，它能把内部方法或属性的实现交给外部，自己只需要关心自己的新方法

> Kotlin 原生支持委托模式，一个关键字就能很做到在 Java 里面几十行的代码才完成的功能

- 如果一个类不想自己去实现所有的方法，而是委托给另一个类去实现，就可以使用委托模式，委托的好处就是***解耦***，***提高代码的可读性和可维护性***

- Kotlin ***使用 `by` 关键字进行方法的委托，写在继承的接口后面（只能是接口），构造函数需要一个该接口的实现对象进行委托***


```kt
// 这是一个装饰模式的呈现，使用委托

interface Shape {
    fun draw()
}

class Circle(val radius: Double) : Shape {

    override fun draw() {
        println("Drawing a circle with radius $radius")
    }
}

class Rectangle(val width: Double, val height: Double) : Shape {

    override fun draw() {
        println("Drawing a rectangle with width $width and height $height")
    }
}

class ShapeDecorator(val shape: Shape) : Shape by shape {

    // 我不想关心 draw 方法的实现，只需要调用它就行
    fun resize(factor: Double) {
        shape.draw()
        println("Resizing the shape by factor $factor")
    }
}

fun main() {

    val circle = Circle(5.0)
    val rectangle = Rectangle(10.0, 20.0)

    circle.draw()
    rectangle.draw()

    val decoratedCircle = ShapeDecorator(circle)
    decoratedCircle.resize(2.0)
}
```

```kt
// 这是另一种设计模式：代理的实现，它与装饰的区别多在与装饰在于扩充原有的功能，而代理是在实现时不去关心继承的实现，只需关心自己新的方法

interface IInstantNoodles {

    fun noodles(): String

    fun sauce(): String

    fun smallLeaves(): String

    fun extras(): String
}

class IngredientPackets: IInstantNoodles {

    override fun noodles(): String {
        return "普通即食面条"
    }

    override fun sauce(): String {
        return "红烧酱汁"
    }

    override fun smallLeaves(): String {
        return "六颗小叶子"
    }

    override fun extras(): String {
        return "香辣粉"
    }

    fun Egg(): String {
        return "鸡蛋"
    }

    fun Beef(): String {
        return "两颗牛肉"
    }
}

class PackagingTheFinishedProduct(noodlesImpl: IInstantNoodles): IInstantNoodles by noodlesImpl {   // 委托时候主构造需要一个接口类的对象（也就是接口的实现类，因为接口本身没有对象，而这个对象一定完成了接口的定义），by 后面的实现类就是主构造里面的那个对象名称
    
    // 如果还要重写继承来到方法，会让这里很乱

    fun Shell () : String {
        return "纸质外壳"
    }

    fun Label () : String {
        return "商品标签"
    }

    fun Box () : String {
        return "盒子包装"
    }

    override fun toString(): String {
        return "一包由${Shell()}${Box()}的方便面，材料是\n${noodles()}，${sauce()}，${smallLeaves()}，${extras()}"

        // 比如这里，我可以访问到继承来交给配料类的 noodles() 等方法，但是访问不到 Egg() 和 Beef() 方法
    }
}

fun main() {

    val ingredients = IngredientPackets()
    val finishedProduct = PackagingTheFinishedProduct(ingredients)

    println(finishedProduct)
}
```

- **可以为多继承的接口每一个指定一个委托对象，这样子就可以实现多继承的委托**

```kt
// 定义Flyer接口
interface Flyer {
    fun fly()
}

// 定义Swimmer接口
interface Swimmer {
    fun swim()
}

// 实现Flyer接口的具体类
class Bird : Flyer {
    override fun fly() {
        println("I can fly like a bird!")
    }
}

// 实现Swimmer接口的具体类
class Fish : Swimmer {
    override fun swim() {
        println("I can swim like a fish!")
    }
}

// FlyingFish类通过委托实现多继承
class FlyingFish(flyer: Flyer, swimmer: Swimmer) : Flyer by flyer, Swimmer by swimmer

fun main() {
    // 创建具体的Flyer和Swimmer实例
    val bird = Bird()
    val fish = Fish()

    // 创建FlyingFish实例，并委托给bird和fish
    val flyingFish = FlyingFish(bird, fish)

    // 调用fly和swim方法
    flyingFish.fly()
    flyingFish.swim()
}
```

> 去看反编译后的代码，知道本质上 Kotlin 是把自己继承接口的实现调用了主构造里的两个对象的方法

- 委托的时候***如果本身也实现了接口***的方法，那么会***调用自己实现的而不是委托对象的***，这点要注意

```kt
interface A {
    fun foo()
}


class B : A {
    override fun foo() {
        println("B.foo()")
    }
}   


class C(a: A) : A by a {
    override fun foo() {
        println("C.foo()")
    }
}


fun main() {
    val b = B()
    val c = C(b)

    b.foo()
    c.foo()
}
```

> 这里 `C` 类继承了 `A` 接口，并委托给 `b` 对象，`c` 对象调用 `foo()` 方法的时候，会调用 `b` 对象的方法，而不是 `c` 对象自己的实现，因为 `c` 对象没有实现 `foo()` 方法，而是委托给了 `b` 对象

> 这里是方法的委托，后面会讲属性的委托

## 7.11 特殊类

### 7.11.1 数据类

- ***数据类是一种特殊的类，它可以自动生成 `equals()`、`hashCode()`、`toString()` 方法，以及 `componentN()` 方法（用于解构对象），这些方法都是基于类的属性来实现的，而且还可以自动生成 `copy()` 方法，可以方便的实现对象的复制***

- 要***声明一个数据类，只需要在类名前面加上 `data` 关键字，然后在类体中声明属性即可***

```kt
data class Person(val name: String, val age: Int)

fun main() {
    val person1 = Person("Alice", 25)
    val person2 = Person("Bob", 30)

    println(person1)
    println(person2)

    println(person1 == person2)
    println(person1.copy(age = 35))
}   
```

> `toString()` 的默认格式是 `Person(name=Alice, age=25)`

> **`copy()` 方法可以复制对象，修改其中一个属性的值，而不需要关心其他属性**，然后返回新的对象，这里 `copy()` 格式是 `fun copy(name: String = this.name, age: Int = this.age): Person`

```kt
val jack = Person(name = "Jack", age = 1)
val olderJack = jack.copy(age = 2)
```

> 自动生成的 `equals` 可以方便的比较对象而不需要自己重写，默认比较类中的所有属性是否相等

- 为了保证自动生成的代码，数据类有以下规定：
    1. ***不能没有主构造***，主构造函数必须至少有一个参数
    2. ***主构造里的所有参数必须同时也是属性***，主构造函数的所有参数必须标记为 `val` 或 `var`
    - 并不代表属性无法在类体中声明，***类体中声明的属性会被 `equals()` `toString()` 等等自动生成的方法排除***，比如下面

        ```kt
        data class Person(val name: String) {
            var age: Int = 0
        }

        fun main() {
            val person1 = Person("John")
            val person2 = Person("John")
            person1.age = 10
            person2.age = 20

            println("person1 == person2: ${person1 == person2}")
            // person1 == person2: true

            println("person1 with age ${person1.age}: ${person1}")
            // person1 with age 10: Person(name=John)

            println("person2 with age ${person2.age}: ${person2}")
            // person2 with age 20: Person(name=John)
        }

        // 这里 person1 和 person2 的 age 被排除在外，所以 person1 和 person2 相等，但是 toString() 显示的 age 不同
        ```
    3. ***数据类不能是抽象、开放、密封或者内部的***

    > 也就是***数据类不能被继承***，可以看[Jet Brains 博客](https://blog.jetbrains.com/kotlin/2015/09/feedback-request-limitations-on-data-classes/#Appendix.Comparingarrays) 了解为什么

    4. **`compoentN()` 和 `copy()` 不允许自定制**
    5. **如果在数据类体中有显式实现 `equals()`、 `hashCode()` 或者 `toString()`，或者这些函数在父类中有 `final` 实现**，那么不会生成这些函数，而***会使用现有函数***

    ```kt
    open class User(open val name: String, open val age: Int) {
        final override fun toString(): String {
            return "User123(name='$name', age=$age)"

            // 父类里面 final 的可以被数据类的子类所使用，真是想不清
        }
    }

    data class Person(override val name: String, override val age: Int): User(name, age)

    fun main() {
        val person1 = Person("Alice", 25)
        val person2 = Person("Bob", 30)

        println(person1)
        println(person2)
    }
    ```

    6. **如果父类（数据类不能被继承，但是可以继承）有自己 `open` 的 `componentN()` 方法，如果返回格式兼容，则使用父类继承而来的，如果不兼容或者不开放，则会报错**

- 这个 **`conpoment()` 方法，是用来对解构声明进行重载**的，而***解构声明可以方便的从一个对象中取出一些属性***，还可以方便的赋值给变量，比如下面

```kt
data class Person(val name: String, val age: Int) 

fun main() {
    val person1 = Person("John", 30)    
    val (name, age) = person1
    println(name)
    println(age)
}
```

- 如果想对 `componentN()` 方法进行重载，实现对自定义类的解构声明，可以在类体或是扩展函数中定义 `componentN()` 方法，每一个方法返回一个类中的属性

```kt
class Person(val name: String, val age: Int) {
    // 注意：数据类不能自定义 compoentN() 方法，只能使用自动生成的，所以这里是一个普通类

    operator fun component1() = name
}
operator fun Person.component2() = age

fun main() {
    val person1 = Person("Alice", 25)
    var (name, age) = person1   // val 或 var 均可
    name = "Bob"    // 这就是普通的变量
    println(name)
    println(age)
}

// 注意，解构时变量的数量只能小于等于声明的解构重载函数（类里面加上扩展）的数量
```

- 加上前面说过的 `[]` 索引操作符重载，现在就可以声明一个类似数组的类

```kt
class Data (var firstName: String, var lastName: String, var age: Int){
    operator fun component1(): String = firstName

    operator fun component2(): String = lastName

    operator fun component3(): Int = age

    operator fun set(index: Int, value: String) { // set 就是 [] 赋值，有两个参数
        when (index) {
            0 -> firstName = value
            1 -> lastName = value
            2 -> age = value.toInt()
            else -> println("Invalid index")
        }
    }

    operator fun get(index: Int): String { // get 就是根据 [] 取值
        return when (index) {
            0 -> firstName
            1 -> lastName
            2 -> age.toString()
            else -> "Invalid index"
        }
    }
}

fun main() {
    val data = Data("John", "Doe", 30)
    data[0] = "Jane"
    data[1] = "Dorothy"
    data[2] = "35"
    val (firstName, lastName, age) = data
    println("First Name: $firstName")
    println("Last Name: $lastName")
    println("Age: $age")
    println("first name: ${data[0]}, last name: ${data[1]}, age: ${data[2]}")
}
```

### 7.11.2 枚举类

- 有些时候一些变量只能由特定且有限的值，并且值之间有很强的关联性，这时候就可以使用枚举类

- 要***声明一个枚举类，只需要在类名前面加上 `enum` 关键字，然后在类体中使用 `,` 分别声明枚举常量即可***


```kt
enum class Color { RED, GREEN, BLUE }


fun main() {
    val color1 = Color.RED
    val color2 = Color.BLUE

    println(color1)
    println(color2)
}
```

- 所谓枚举类，本质上就是一个普通的类，只不过***每一个枚举常量就是这个类的一个对象***，所以你可以理解为

```kt
class Color {
    val RED: Color = Color()
    val BLUE: Color = Color()
    val GREEN: Color = Color()
}
```

- 枚举类本身不能初始化对象，可是***枚举常量可以初始化枚举类***

```kt
enum class Day(val weekOfDay: Int) {
    MONDAY(1),
    TUESDAY(2),
    WEDNESDAY(3),
    THURSDAY(4),
    FRIDAY(5),
    SATURDAY(6),
    SUNDAY(7)

    // 每一个枚举常量都是枚举类的对象，自然可以有构造函数
}

fun main() {
    // 枚举类里的常量都是静态的，无需实例化就可以使用

    println(Day.MONDAY.weekOfDay)
    println(Day.TUESDAY)
}
```

- ***枚举类里面除了枚举常量，还可以有普通的属性和方法，枚举常量可以访问这些属性和方法***（因为他们是枚举类的实现，自然拥有这些属性和方法），但是枚举类本身不能访问（因为本身不能初始化）

```kt
enum class Day(val weekOfDay: Int, val chineseName: String) { // 这就是属性，写在了主构造里
    MONDAY(1, "星期一"),
    TUESDAY(2, "星期二"),
    WEDNESDAY(3, "星期三"),
    THURSDAY(4, "星期四"),
    FRIDAY(5, "星期五"),
    SATURDAY(6, "星期六"),
    SUNDAY(7, "星期日");

    // 枚举常量可以访问这些属性和方法
    fun isWeekend() = this == SATURDAY || this == SUNDAY

    // 枚举类可以有自己的 companion object
    companion object {
        fun daysOfWeek() = 7
    }
}

fun main() {
    println(Day.MONDAY.isWeekend())
    println(Day.TUESDAY.chineseName)
    println("一周有${Day.daysOfWeek()}天")
}
```

- 既然这样，***枚举类里面也可以有抽象的属性和方法，枚举常量也可以实现这些抽象方法，自然也可以使用匿名类的方式实现***

> 注意***枚举常量和普通成员之间使用 `;` 分号分隔***

```kt
enum class Day {
    // 直接在枚举常量名后面加上花括号，里面就是实现的抽象方法

    Monday {
        override fun getDay(): String {
            return "星期一"
        }
    },
    Tuesday {
        override fun getDay(): String {
            return "星期二"
        }
    },
    Wednesday {
        override fun getDay(): String {
            return "星期三"
        }
    },
    Thursday {
        override fun getDay(): String {
            return "星期四"
        }
    },
    Friday {
        override fun getDay(): String {
            return "星期五"
        }
    },
    Saturday {
        override fun getDay(): String {
            return "星期六"
        }
    },
    Sunday {
        override fun getDay(): String {
            return "星期日"
        }
    };

    // 使用分号分隔枚举常量和一般成员（Java ：你逃不掉吧）

    abstract fun getDay(): String
}
```

- 虽然**枚举类不能继承自类、抽象类**，但是它***可以继承接口***，每一个枚举常量必须均实现接口里的方法，可以向上面的那样单独实现，***也可以定义一个普通的函数实现，则每一个枚举常量都使用这个函数的实现***

```kt
interface DayInterface {
    fun getDay(): String
}

enum class Day: DayInterface {
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY;

    override fun getDay(): String {
        return "I don't know the day"
    }
}


fun main() {
    println(Day.MONDAY.getDay())
    println(Day.TUESDAY.getDay())
}
```

- Kotlin 也为枚举类添加了一些内置的属性，对于***每一个枚举常量都可以使用他们***，**`name` 会返回当前枚举常量的名称， `ordinal` 会返回当前枚举常量的索引（从 0 开始）**

- ***每一个枚举类本身也有内置的方法***，比如 **`values()` 方法可以返回所有枚举常量的数组，`valueOf(name: String)` 方法可以根据名称返回枚举常量**

> 在 Kotlin 1.9 以后，***建议使用 `entries` 而不是 `values()`***，具体见泛型篇

```kt
enum class Day (val chineseName: String) {
    Monday("星期一"),
    Tuesday("星期二"),
    Wednesday("星期三"),
    Thursday("星期四"),
    Friday("星期五"),
    Saturday("星期六"),
    Sunday("星期日");
}


fun main() {

    for (day in Day.values()) {
        when (day) {
            // 这里使用了好几个内置属性，可能有点晕，比如 Day.valueOf(day.name) 就是根据 day.name 得到枚举常量的名字，然后通过这个名字再得到 chineseName 属性
            // 其实只需要 day.chineseName 就可以了
            Day.Monday -> println("今天是一周内的第${day.ordinal + 1}天，是${day.chineseName}，要上班")
            Day.Tuesday -> println("今天是一周内的第${day.ordinal + 1}天，是${Day.valueOf(day.name).chineseName}，要上班")
            Day.Wednesday -> println("今天是一周内的第${day.ordinal + 1}天，是${Day.valueOf(day.name).chineseName}，要上班")
            Day.Thursday -> println("今天是一周内的第${day.ordinal + 1}天，是${Day.valueOf(day.name).chineseName}，要上班")
            Day.Friday -> println("今天是一周内的第${day.ordinal + 1}天，是${Day.valueOf(day.name).chineseName}，要上班")
            Day.Saturday -> println("今天是一周内的第${day.ordinal + 1}天，是${Day.valueOf(day.name).chineseName}，可以休息了")
            Day.Sunday -> println("今天是一周内的第${day.ordinal + 1}天，是${Day.valueOf(day.name).chineseName}，可以休息了")

            // 注意到，when 表达式不需要 else 分支，因为编译器知道这里涵盖了所有的可能，这也是之前 when 说过必须有 else 的一个特例
        }
    }
}
```

> 还可以使用 `enumEntries<T>()` 以泛型的方式访问枚举类里的常量，，但是因为目前还是测试阶段，具体看[官方文档](https://book.kotlincn.net/text/enum-classes.html)吧

### 7.11.3 密封类

- ***密封类是一种特殊的类，它对自己的子类的数量严格控制***，每一个子类都在编译时可知，在这之外不允许有继承自己的子类

- 要***声明一个密封类，只需要在类名前面加上 `sealed` 关键字，然后在类体中声明子类即可***

- ***密封类是一种特殊的抽象类***，它本身**无法被构造，但是允许声明构造函数**（子类继承），**密封类里可以有普通成员也可以有抽象成员**，特殊的地方在于***密封类的子类只能在密封类的类体里作为成员或者相同文件下声明***（不同包不允许），不允许用户继承，只能通过密封类的成员子类来访问密封类里的方法和属性

> 在 Kotlin 1.1 之前，密封类的子类只能作为成员，现在你可以在同一文件下或同一包下（1.5 以后）声明，这些地方在编译时可知，但是如果别人想在外部的包内引用是不可以的

```kt
sealed class Shape {
    class Circle(val radius: Double) : Shape() {
        override fun name() = "Circle"
        override val size: Double = radius * radius * 3.14159
    }
    class Rectangle(val width: Double, val height: Double) : Shape() {
        override fun name() = "Rectangle"
        override val size: Double = width * height
    }

    abstract fun name(): String
    abstract val size: Double

    init {
        println("Shape ${this.name()} created")
        // 这个 name 访问的方法，在调用时由于子类还没有完成初始化，如果这里 name 的实现会调用 open 的属性或 name 是一个属性，会犯下上文提过的错误，父类的构造里不要去调用 open 的方法
    }
}

class Triangle(val base: Double, val height: Double) : Shape() {
    override fun name() = "Triangle"
    override val size: Double = 0.5 * base * height
}

fun main() {
    val circle = Shape.Circle(1.0)
    val rectangle = Shape.Rectangle(2.0, 3.0)
    val triangle = Triangle(3.0, 4.0)

    println("Name: ${circle.name()}, Size: ${circle.size}")
    println("Name: ${rectangle.name()}, Size: ${rectangle.size}")
    println("Name: ${triangle.name()}, Size: ${triangle.size}")
}
```

-  ***密封类的构造函数（constructor，不是 init）只能是 `private` 或 `protected`***，默认 `private`

- 虽然**密封类本身不能被继承**，但是***密封类的成员子类是可以被任意继承的***，当然密封类内部也可以有密封类，也就是一个密封类的成员子类也是密封类并且继承自自己

- ***密封类的成员子类可以是普通类、数据类和密封类***，内部类（inner）因为无法构造外部类的对象因此无法使用

- 除了密封类，Kotlin 还加入了***密封接口***（sealed interface）

- ***密封接口同时具备接口和密封类的特性，外部包同样无法访问***，有时候我们**希望公开以一个接口可是不希望别人实现它，就可以使用密封接口**

```kt
sealed interface Animal {
    fun makeSound() {
        println("Animal makes sound")

        // 仍然允许默认实现
    }
}

class Test : Animal {
    override fun makeSound() {
        println("Test makes sound")
    }

    // 密封接口可以被普通类、数据类、密封类或是枚举类继承
}

sealed class Mammal: Animal {
    class Dog: Mammal() {
        override fun makeSound() {
            println("Woof!")
            super<Mammal>.makeSound()
        }
    }
    class Cat: Mammal() {
        override fun makeSound() {
            println("Meow!")
            super<Mammal>.makeSound()
        }
    }

    // 密封类本身可以不实现，交给自己的成员子类
}

fun main() {
    val dog = Mammal.Dog()
    val cat = Mammal.Cat()

    dog.makeSound()
    cat.makeSound()
}
```

- 因为密封类的子类成员数量在编译时可知，所以在**对一个密封类型的对象进行 `when` 筛选时，无需 `else` 分支**

```kt
sealed class Shape {
    class Circle(val radius: Double) : Shape() {
        override fun name() = "Circle"
        override val size: Double = radius * radius * 3.14159
    }
    class Rectangle(val width: Double, val height: Double) : Shape() {
        override fun name() = "Rectangle"
        override val size: Double = width * height
    }

    abstract fun name(): String
    abstract val size: Double

    init {
        println("Shape ${this.name()} created")
    }
}

class Triangle(val base: Double, val height: Double) : Shape() {
    override fun name() = "Triangle"
    override val size: Double = 0.5 * base * height
}

fun main() {
    val shape: Shape = Shape.Circle(5.0)

    when (shape) {
        is Shape.Circle -> println("Circle with radius ${shape.radius} has size ${shape.size}")
        is Shape.Rectangle -> println("Rectangle with width ${shape.width} and height ${shape.height} has size ${shape.size}")
        is Triangle -> println("Triangle with base ${shape.base} and height ${shape.height} has size ${shape.size}")
    }
}
```

- 说起来枚举类其实可以这样写

```kt
sealed class Color {
    object RED : Color()
    object GREEN : Color()
    object BLUE : Color()
}
```

### 7.11.4 内联类

> 在观看此小结前，建议阅读[Kotlin 值类型设计](https://github.com/Kotlin/KEEP/blob/master/notes/value-classes.md)这篇 Github 上的文章，会方便你了解，同时，内联类在 Kotlin 当中仍是一个较新的设计，不排除以后版本会进行修改的可能性

> 在 Kotlin 1.3 之前，使用 `inline` 去声明内联类，1.5 ***引入了 `value` 关键字，但是现在使用 `value` 仍需要加上 `@JvmInline` 的注解***，否则编译不通过（非 JVM 平台可以不写，比如 Native）。`inline class` 仍然可以用但是不排除被废弃的可能，`value` 未来仍可能添加新特性

- 很多语言里都有***值类型和引用类型的区别，对于值类型（Value Type），在赋值、传参、返回时都会进行值拷贝，对于引用类型（Reference Type），在赋值、传参、返回时都会进行引用传递***

```c
#include <stdio.h>

struct test {
    int a;
    char b;
    double c;
};

int main() {
    struct test t = {10, 'a', 3.1415926};

    struct test k = t;
    // 简单的理解为深拷贝和浅拷贝的区别也可以

    t.a = 20;

    printf("t.a = %d, k.a = %d\n", t.a, k.a);
    printf("t.b = %c, k.b = %c\n", t.b, k.b);
    printf("t.c = %f, k.c = %f\n", t.c, k.c);

    return 0;
}
```

- 那这样子的话 **Kotlin 里的基本类型就可看作是值类型**，而***其他的都是引用类型***，**引用类型的赋值是传递地址的引用，值类型会直接复制自己的全部**

- 任何变量总会关联一个值，只是在使用时，对***有些变量，我们将直接取用这个值本身，这被称为值类型变量***，而对另一些变量，我们把***这个值作为索引、取用这个索引指示的数据，这被称为引用类型变量***。***值类型变量通常在线程栈上分配，每个变量都有自己的数据副本；引用类型变量通常在进程堆中分配，多个变量可引用同一数据对象，对一个变量执行的操作可能会影响其他变量***

> 这是一段华为仓颉文档里的一段，我认为说的很好，而且明确了值类型是在线程栈，引用类型是在进程堆，看过后面第十二章的内存模型后你就知道为什么说的好了

```kt
fun main() {
    val n1: Int = 10
    val n2: Int = n1

    println(n1 == n2)
    println(n1 === n2)
    // depreciated
    // Kotlin 马上要禁用基本类型之间的比较，因为基本类型是值类型，比较的是值而不是地址，如果可以的话就太可笑了，虽然结果的地址是一样的

    val s1: String = "Hello"
    val s2: String = "Hello"

    println(s1 == s2)
    println(s1 === s2)

    val m1: Int? = 10
    val m2: Int? = 12
    println(m1 == m2)
    println(m1 === m2)
    // 同理提醒要废弃，但是结果说明二者地址是不一样的，编译后的结果也说明了

    data class Person(val name: String, val age: Int)
    val p1: Person = Person("John", 25)
    val p2: Person = Person("John", 25)
    println(p1 == p2)
    println(p1 === p2)
}
```

> 那 Kotlin 有没有类似其他语言的 `struct` 呢，有内联类

- ***使用 `value` 关键字声明一个内联类***，注意该类***有且只能有一个有字段值的只读属性（只能是 `val`），并且在主构造中声明***，**可以有没有幕后字段的属性、方法、init 代码块和次级构造函数**

> **任何次级构造都不能为空**，属性不支持 `lateinit`

```kt
@JvmInline
value class Name(val value: String)

fun main() {
    printName(Name("John"))
}

fun printName(name: Name) {
    // fun printName-Jhjajkf(name: String)
    // 这就是编译后的结果，可以看到编译器已经把 `Name` 转换成 `String` 类型了

    println(name)
}
```

```kt
@JvmInline
value class ValueName(val s: String) {

    val length: Int
        get() = s.length

    constructor(first: String, last: String) : this("$first $last") {
        println("first: $first, last: $last")
    }

    fun greet() {
        println("Hello, $s!")
    }
}

inline class InlineName(val s: String) {
    fun greet() {
        println("Hello, $s!")
    }

    val length: Int
        get() = s.length

    constructor(first: String, last: String) : this("$first $last") {
        println("first: $first, last: $last")
    }
}

fun main() {
    val valueName = ValueName("John", "Ivanov")
    valueName.greet()
    println(valueName.length)
    val inlineName = InlineName("Jane", "Macpherson")
    inlineName.greet()
    println(inlineName.length)
}
```

- 不要以为内联类就能在所有的地方优化性能，***如果你把内联类当作另一种类型，那么他就会被装箱***

> 内联类的这个概念仍不完善，就目前来讲没啥用，他最多在需要内联类的参数上优化，其他地方基本没用，还可能会带来性能的更多消耗，内联类仍会被创建，并且拥有一对拆箱装箱方法

> 还是期待未来类似 `struct` 的结构

```kt
@JvmInline
value class MyInt(val value: Int)

fun main() {
    val myInt = MyInt(10)
    printMyInt(myInt)   // 拆箱
    println(myInt)      // 装箱，因为 println 参数是 Any 类型
}

fun printMyInt(myInt: MyInt) {
    println(myInt.value)
}
```

- ***内联类允许继承接口***，但是除此之外***内联类不允许继承任何类也不允许被任何类继承***

- ***内联类的属性允许委托实现接口***

```kt
interface MyInterface {
    fun bar()
    fun foo() = "foo"
}

@JvmInline
value class MyInterfaceWrapper(val myInterface: MyInterface) : MyInterface by myInterface

fun main() {
    val my = MyInterfaceWrapper(object : MyInterface {
        override fun bar() {
            // body
        }
    })
    println(my.foo()) // prints "foo"
}
```

- 因为内联类既可以表示为基础类型有可以表示为包装器，***引用相等 `===` 对于内联类***而言毫无意义，因此这也***是被禁止的***

```kt
fun main() {
    val p1 = Person("Alice")
    val p2 = p1
    println(p1 == p2)
    // println(p1 === p2) 编译不通过，因为内联类不允许引用相等
}

@JvmInline
value class Person(val name: String)
```

- 可以看到在底层接受内联的参数的函数后面会加上一个独特的哈希值，这是为了避免在声明多个名称不同但是属性相同的内联类时，由于编译后会被化为同样的参数类型，命名会冲突的问题，同时 Java 也不能去调用接受内联参数的函数除非你手动加上 `@JvmName` 注解

```kt
@JvmInline
value class Name(val value: String)

@JvmInline
value class Message(val value: String)

fun func(msg: Name) {
    println("Hello, $msg!")
}

fun func(msg: Message) {
    println("Message: $msg")
}
```

> 底层

```java
public static final void func_75PUH38(@NotNull String msg) {
    Intrinsics.checkNotNullParameter(msg, "msg");
    String var1 = "Hello, " + Name.toString-impl(msg) + '!';
    System.out.println(var1);
}

public static final void func_3FFIWmM(@NotNull String msg) {
    Intrinsics.checkNotNullParameter(msg, "msg");
    String var1 = "Message: " + Message.toString-impl(msg);
    System.out.println(var1);
}
```



# 第八章：泛型

## 8.1 泛型概述

> 假如我们有一个类想要接受所有类型参数都可以传入，而不需要对每一个类型都进行重写，我们可能会想到使用 `Any` 类型，最后对它返回的类型进行强制转换，比如

```kt
fun main() {
    val printer = Printer("Hello")
    printer.print()
    val str: String = printer.getMsg() as String
    println(str)
    
    val printer2 = Printer(123)
    printer2.print()
    val num: Int = printer2.getMsg() as Int
    println(num)
}


class Printer (val message: Any) {
    fun print() {
        println(message)
    }

    fun getMsg(): Any {
        return message
    }
}
```

> 但是强制转换还是会带来一些可能隐患，其实 Kotlin 还有一种更方便的

- ***泛型（generics）*** 是一个重要特性，它允许我们在定义类、函数、接口时使用类型参数（type parameter）来表示类型，从而可以编写更灵活、更具表现力的代码

> 比如我们有一个类，我们希望无论用户传入什么类型，都可以正常运行，而不是创建一堆同样功能只不过构造类型不同的类

- 要使用泛型，***将泛型参数 T 放在尖括号 `<T>` 中 , 该泛型参数放在类名后 , 主构造函数之前, 该泛型参数 T 是类型占位符***，可以替换为任意字母，但是一般用大写字母 T、K、V 来表示类型参数


```kt
class Box<T>(val value: T) {
    fun get(): T {
        return value
    }
}

fun main() {
    val box1 = Box<Int>(10)
    val box2 = Box<String>("Hello, world!")
    val box3 = Box<Double>(3.14159)

    println(box1.get())
    println(box2.get())
    println(box3.get())
}
```

- 如果类型参数可以推断出来，例如从构造函数的参数或者从其他途径， 就***可以省略类型参数***

- ***泛型也可以有多个类型参数，每一个泛型参数之间使用逗号 `,` 分隔***


```kt
class Tuple <T, K> (one: T, two: K){
    val first: T = one
    val second: K = two

    fun printTuple() {
        println("First element: $first")
        println("Second element: $second")
    }
}

fun main() {
    val tuple = Tuple(10, "Hello")
    // 等于 val tuple = Tuple<Int, String>(10, "Hello") 可以不指定类型参数，因为编译器知道 10 是 Int 类型， "Hello" 是 String 类型
    tuple.printTuple()
}
```

> 把泛型理解为一个类型占位符更容易理解，使用泛型类的时候需要把泛型参数的类型也传入，比如 `MyClass` `MyClass<T>` 是两个不同的类型

- 记住***泛型参数本身只是一个占位符，在编译时会被擦除，因此编译后的字节码中并没有泛型参数，只有泛型参数对应的真实类型***，这个叫做***类型擦除***，是 JVM 平台的天生特性

```kt
class Tuple <T, K> (one: T, two: K){
    val first: T = one
    val second: K = two

    fun printTuple() {
        println("First element: $first")
        println("Second element: $second")
        println("Factorial of first element: ${first.factorial()}")

        // 这里不可以访问 factorial 方法，因为类型参数 T 在运行时实际上是 Any 类，Any 没有这个扩展方法
    }
}

fun Int.factorial(): Int {
    if (this == 0) {
        return 1
    }
    return this * this.factorial()
}

fun main() {
    val tuple = Tuple(10, "Hello")
    tuple.printTuple()
    println("Factorial of 5: ${5.factorial()}")

    // 但是这里可以访问 factorial 方法
}
```

> 请记住这个特性，有关泛型的所有问题基本上都是基于这个特性带来的疑惑，下面会再讲解

> 上面我们自己声明了一个 `Tuple`元组，其实 Kotlin 也有内置的元组类型，但***请注意元组已经被抛弃***，现在只有二元元组和三元元组可用，多元元组不可用

```kt
fun main() {
    val tuple1 = Pair(1,"Hello")
    val tuple2 = Triple(2,"World", 3.14)
    val tuple3 = '\n' to 42

    // public infix fun <A, B> A.to(that: B): Pair<A, B> = Pair(this, that)
    // 中缀操作符 to 可以快速生成二元元组，请记住这个方法，后面讲集合的时候会遇见

    println(tuple1)
    println(tuple2)
    println(tuple3)
}

// 元组的本质就是泛型数据类

public data class Pair<out A, out B>(
    public val first: A,
    public val second: B
) : Serializable
```

- 当**定义了一个泛型类，该类里面的方法和属性都可以把这个类型参数当作一个真正的类型来使用**

- 因为Kotlin 支持顶层函数，***函数如果想要使用泛型，在 `fun` 后面，函数名前面写上 `<T>`***，然后自己的参数和函数体内部就能使用这个类型占位符使用时传入的类型

- 怎样判断需不需要写新的泛型参数呢？关键在于如果函数所在的类已经声明了这个泛型，但***函数需要返回一个新的类型***，这个类型跟类声明的泛型类型是不一样的，或者说***函数位于顶层***，都***需要自己写上尖括号去声明新的泛型类型***，如果**类里面的方法自己重新声明一个类型参数，无论名称是否一样都是会覆盖掉原来的类型参数的**

```kt
class User<T> (val msg: T) {
    
    fun <K> function(func: (T) -> K): K = func(msg)
}

fun main() {
    val user = User("Hello, World!")
    println(user.function {value: String -> 
        value.toString()
        
        // 这里 value 写明了是 String 类型，所以在泛型里面也可以使用 String 类的 length 属性返回 Int 类型的值
    })
}
```

```kt
class PairTuple <T, K> (val first: T, val second: K) {

    fun <T> getFirst(t: T): T {
        println(t == first)
        return first as T

        // 如果这里没有 as 转换，编译器会说 “期望 T 类型，但是得到了 T 类型”，实际上就是新声明的类型覆盖了原来的
    }
}

fun main() {
    val pair = PairTuple(1, "Hello")
    val first = pair.getFirst(1)
    println(first)

}
```

- 同样，***泛型类也可以实现泛型接口或继承泛型类***

```kt
interface A <T>{
     fun foo(t: T)
}

open class B <T> {
    open fun bar(t: T) {
        println(t)
    }
}

class C <T, K ,V> (t: T, k: K, v: V) : B<K>(), A<V> {
    // 这里的意思是，C 类有三个泛型参数 T 、 K 和 V，把 K 作为 B 类的泛型参数，把 V 作为 A 接口的泛型参数
    // 是作为泛型参数，跟传值是两个概念，泛型参数一旦传入，则该类里面所有使用该参数作为类型占位符的方法或属性都会被替换成该类型
    
    val tuple = Triple<T, K, V>(t, k, v)

    override fun bar(k: K) {
        println(k == tuple.second)
    }

    fun baz(t: T) {
        println(t == tuple.first)
    }

    override fun foo(v: V) {
        println(v == tuple.third)
    }

}


fun main() {
    val c = C(1, "Hello", 3.14)
    c.bar("Hello")
    c.baz(2)
    c.foo(3.14)
}
```

- 还有**泛型扩展函数**

```kt
fun <T: Number?> T.isNull(): Boolean = if (this == null) true else false

fun main() {
    val num: Int? = 10
    val nullNum: Int? = null
    // val str: String? = "Hello" 无法使用 isNull() 方法
    
    println(num.isNull()) // false
    println(nullNum.isNull()) // true
}
```

## 8.2 泛型的约束

- 上面讲过，JVM 的类型擦除导致我们无法使用传入对象的独有方法，可以***在声明泛型参数的时候在类型参数后面加上冒号 `:` 约束，来限制泛型参数的类型范围，只有该类的子类或是实现类才能传入，这样就可以使用这个父类继承给子类的方法和属性了***

```kt
class User<T: Name> (val msg: T) {

    fun <K> function(func: (T) -> K): K = func(msg)
}


class Name (val name: String)


fun main() {
    val user = User(Name("John"))
    println(user.function { it.name.toString() })
}
```

- 这个叫***泛型的上界（upper bound）约束***，表示泛型参数 T 的类型必须是某个类的子类，或者是该接口的实现类

- 对于***默认的类型参数，它是 `Any?` 的子类***，所以你传入 `null` 是可以的

```kt
class Generics<T> (val value: T) {  // <T :Any?>
    fun printValue() {
        value.printValue()
    }
}

fun Any?.printValue() {
    println("Yes, I am Any")

    if (this == null) println("I am null") else println("I am not null")
}

fun main() {
    val generics = Generics(null)
    generics.printValue()
}
```

- 默认在尖括号里只能声明一个父类，***如果类型参数需要多个父类（接口）的约束，请使用单独 `where` 的子句***

> 这里请看清楚 `where` 声明的位置和格式

```kt
interface Animal {
    fun makeSound(): String
}

interface Runnable {
    fun run()
}

class Dog<T>(val name: String, val animal: T) : Animal by animal, Runnable by animal
where T : Animal, T : Runnable {
// where 另起一行声明

    fun printName() {
        println(name)
    }
}

fun <T> makeDog(name: String, animal: T): Dog<T>
where T : Animal, T : Runnable {
// 另起一行声明

    return Dog(name, animal)
}

class Impl : Animal , Runnable {
    override fun makeSound(): String {
        return "Woof!"
    }

    override fun run() {
        println("Running...")
    }
}


fun main() {
    val dog = makeDog("Fido", Impl())
    dog.printName()
    dog.run()
    println(dog.makeSound())
}
```

## 8.3 reified

> 最好先看下[Kotlin 官方文档](https://book.kotlincn.net/text/generics.html)对这里的描述，同时复习一些 Java 的知识点

- 因为**类型擦除**的存在，所以你可以判断一个泛型值是不是某个类型，但是***不能判断某个值是不是泛型类型的***

```kt
fun <T> Int.isInt(value: T) = this is T // 错误，不能判断某个值是不是泛型类型的

fun main() {
    println(1.isInt(1))
    println(1.isInt("1"))
}
```

- 但是 Kotlin 有一个***关键字 `reified`，只能使用在内联函数的泛型参数声明上***，可以让你在运行时判断某个值是不是某个泛型类型

```kt
inline fun <reified T> Int.isInt(value: T) = this is T

fun main() {
    println(1.isInt(1))
    println(1.isInt("1"))
}
```

> reified 关键字并没有修改 JVM 的类型擦除，只不过由于内联函数可以知道泛型参数的具体类型，所以运行时直接硬编到返回指里

## 8.4 协变和逆变

- 泛型能实现多态吗？看下面的第一个变量 value1 是被允许的，但是第二个变量 value2 是不被允许的，也就是说，你***不能把一个泛型类型子类的对象赋给泛型类型父类的引用***

```kt
open class Base<T> (open val value: T) {
    open fun func() {
        println("Base func $value")
    }
}

class Derived<T> (override val value: T) : Base<T>(value) {
    override fun func() {
        println("Derived func $value")
    }
}

fun main() {
    val stringBase = Base<String>("Hello")
    val intBase = Base<Int>(10)
    println(stringBase::class == intBase::class)

    val value1: Base<String> = Derived<String>("Polymorphism") // 允许
    value1.func() // 多态生效
    val value2: Base<Any> = Base<String>("Can't do this") // 报错
}
```

> 还是类型擦除的存在，导致无法判断某个值是不是某个泛型类型的，可以看下面这段官网的示例

```kt
// Java
List<String> strs = new ArrayList<String>();

// 报错；类型不匹配
List<Object> objs = strs;

// 如果它不报错呢？
// 就可以把 Integer 类型添加到 ArrayList<Object> 中
objs.add(1);

// 然后运行时就会抛异常了
// a ClassCastException: Integer cannot be cast to String
String s = strs.get(0);
```

### 8.4.1 Java 的实现

- 在介绍协变和逆变之前，先看看 Java 是怎么处理的，**Java 里面使用通配符 `? extends Base` 来表示接受一个 Base 或者它子类的泛型类型**，这样我们就可以***安全的从中读取数据，但不能写入数据***，因为我们不知道 Base 的子类的具体类型，如果贸然写入可能会导致子类的方法调用时出现类型不匹配的错误

> 从中取出的数据是 Base 类型，子类的对象可以赋给父类

```java
class Fu <T> {
    T value;

    void func() {
        System.out.println("Fu func" + value);
    }

    public T getValue() {
        return value;
    }

    public void setValue(T value) {
        this.value = value;
    }

    Fu(T s) {
        value = s;
    }
}

class Zi <T> extends Fu<T> {
    T value;

    void func() {
        System.out.println("Zi func" + value);
    }

    public T getValue() {
        return value;
    }

    public void setValue(T value) {
        this.value = value;
    }

    Zi(T s) {
        super(s);
        value = s;
    }
}


public class Test {
    public static void main(String[] args) {
        Fu<? extends Object> fu = new Fu<String>("Hi there");
        System.out.println(fu.getValue());
        // fu.setValue("Hello"); 报错，不能写入数据
    }
}
```

- 相反，如果想要从中写入，可以使用通配符 **`? super Base` 来表示接受一个 Base 或者它父类的泛型类型**，这样我们就***可以安全的写入数据，但不能读取数据***，因为不知道 Base 未来会传入怎样的父类，所以只能返回 Base 而不是它的具体父类

> 比如赋给它一个 Object 父类，Base 类型的引用当然可以持有 Object 类型的对象

```java
class Fu <T> {
    T value;

    void func() {
        System.out.println("Fu func" + value);
    }

    public T getValue() {
        return value;
    }

    public void setValue(T value) {
        this.value = value;
    }

    Fu(T s) {
        value = s;
    }
}

class Zi <T> extends Fu<T> {
    T value;

    void func() {
        System.out.println("Zi func" + value);
    }

    public T getValue() {
        return value;
    }

    public void setValue(T value) {
        this.value = value;
    }

    Zi(T s) {
        super(s);
        value = s;
    }
}


public class Test {
    public static void main(String[] args) {
        Fu<? extends Object> fu = new Fu<String>("Hi there");
        System.out.println(fu.getValue());

        Zi<? super Integer> zi = new Zi<Object>(100);
        zi.setValue(213);
        Object obj = zi.getValue(); // 只能是 obj
        System.out.println(obj);
    }
}
```

> 无论你的声明的类型是什么，它真正存储的区域都是这个传入的对象所开辟在内存中的部分，我们通过 getValue 返回的虽然是 `Object` 类型，但是它只是把它整数部分的那一块完整的区域被隐藏起来了，通过 `println` 这个函数调用时，toString 方法是Integer 的 toString，好好理解一下

- `? extends E` 声明的类型是***协变（covariant）***的，意思是***泛型类型参数可以是引用变量泛型参数子类的类型***，在实现泛型多态的代价就是***只能 `getter`，无法使用有关 `setter` 类的方法***

- `? super E` 声明的类型是***逆变（contravariant）***的，意思是***泛型类型参数可以是引用变量泛型参数父类的类型***，虽然***可以使用有关 `setter` 类的方法，但是无法使用有关 `getter` 类的方法***

- ***Java 默认的泛型是抗变（不变，invariant）的，也就是说，泛型类型参数不能是引用变量泛型参数子类的类型，也不能是引用变量泛型参数父类的类型***

> 有一个 PECS 法则，`Producer（生产者）- Extends, Consumer（消费者）- Super`，看看就好

### 8.4.2 in out

- **Kotlin 的泛型默认也是不变的**，但是你可以通过***声明 `in` 和 `out` 关键字来声明协变和逆变，`out` 关键字表示协变，等于 `? extends`，只能 `getter`，`in` 关键字表示逆变，等于 `? super`，只能 `setter`***

> 比 Java 的好记吧

```kt
class MyClass <T> (var value: T)

fun main() {
    val cls1: MyClass<out Number> = MyClass<Int>(12) // 协变
    val cls2: MyClass<in Int> = MyClass<Any>("Hello") // 逆变

    println(cls1.value) // 调用 getter 方法，允许
    cls2.value = 'a' as Any as Int
    // 想不到吧，是可以的，编译器不报错，运行时报错，但是强烈不建议，你声明一个逆变的类就是用类存放它父类的引用的，不是用来存其他的
    val obj = cls2.value // 这里 obj 是 Any?
    println(obj)
}
```

- 这叫***使用处型变***，也就是**在声明** ***泛型对象*** **的时候使用 `in` `out`**

> Kotlin 管这个叫***类型投影***，个人没明白这个起名的意义

```kt
data class Person<T, U> (var first: T, var second: U)

fun duplicate(from: Person<out Any, out Any>): Person<Any, Any> = Person(from.first, from.second)

// 因为我们像让任何类型的 Person 传入，所以形参必须是实参的父类，也就是 Any ，需要 out 来修饰，因为我们只是访问 first 和 second ，所以没有问题

fun main() {
    val person1 = Person("John", 25)
    val person2 = duplicate(person1)
    println(person2)
}
```

- 还有一种***声明处型变***，也就是在**声明** ***泛型类（抽象类、接口）*** **的时候使用 `in` `out`**，**表示自己这个类里面所有的方法都是输入或输出的***，这样在使用的时候就无需再使用 `in out` 了

```kt
abstract class Prosumer <out T> {
    abstract fun func(): T 
}

interface Consumer <in T> {
    fun consume(t: T)
}

// 每一处使用处都是协变或逆变的，不需要再声明 in out
```

> **但是使用了声明处型变的类（接口），里面的每一个方法必须遵守声明时的限制**

```kt
class MyClass <out T> (value: T){
    val value: T = value
    
    var myVar: T = value // 报错，var 属性有 set 方法，与 out 冲突
    
    fun myFunction(): T {
        return value
    }
    
    fun functionWithParam(param: T): T { // 报错，不能使用带有类型参数的函数
        return param 
    }
}
```

> 如果你有一个类是专门用来输入或输出的，那么就可以使用声明处型变；如果本身尽既包含类型参数作为参数的方法，也有返回类型参数的方法，那么最好还是在使用的时候再去型变

- ***请分清楚泛型型变和泛型的上界约束***，二者完全不同

- 有时候我们对泛型参数并不了解，但仍然想使用它，就可以使用***星号通配符 `<*>` 来表示***，它会如下工作

    1. ***对于 `Foo <out T : TUpper>`***，其中 **T 是一个具有上界 TUpper 的协变类型参数**，`Foo <*>` 等价于 `Foo <out TUpper>`， 意味着当 T 未知时，你***可以安全地从 `Foo <*>` 读取 TUpper 的值***

    2. ***对于 `Foo <in T>`，其中 T 是一个逆变类型参数***，`Foo <*>` 等价于 `Foo <in Nothing>`。 意味着当 T 未知时， ***没有什么可以以安全的方式写入 `Foo <*>`***
    
    > 这里 **Nothing 是所有类型的子类**，这是后面的知识点，`in Nothing` 是所有类型，当然不安全，某种意义上可以说 `in Nothing == out Any`

    3. ***对于 `Foo <T : TUpper>`***，其中 **T 是一个具有上界 TUpper 的不型变类型参数**，***`Foo<*>` 对于读取值时等价于 `Foo<out TUpper>` 而对于写值时等价于`Foo<in Nothing>`***

> Kotlin 叫这个星号通配符为***星投影***，***星投影只能用在声明变量时的类型和函数参数这两个使用处***，而不能使用在声明处

> 官网有个示例：对于 `Function1<in T, out U>`  
> `Function<*, String>` 表示 `Function<in Nothing, String>`  
> `Function<*, *>` 表示 `Function<in Nothing, out Any?>`  
> `Function<Int, *>` 表示 `Function<Int, out Any?>`  
>> 因为 `Function1<in T, out U>` 就是 `Function1<in T, out U: Any?>`

- 还有**下划线 `<_>` 运算符用于省略编译器可以自行推断出的类型参数***

```kt
fun <T, K, V> func(t: T, k: K, v: V) {
    println("T: $t, K: $k, V: $v")
}

fun main() {
    func<Int , _ , _>(1, "Hello", true)
}
```

## 8.5 类型别名

- 有时候我们使用的类型名称过长，不便于阅读，Kotlin 提供了***类型别名（type alias），可以给一个类型起一个别名***，方便使用

```kt
typealias Name = String

fun main() {
    val name: Name = "Alice"
}
```

> 类型别名不区分声明范围，无论声明顺序，整个文件都可以使用，不过一般是放在文件顶部，方便阅读

> 但是***类型别名只能声明在顶层***

- 类型别名经常用于给冗长的泛型类型起别名

```kt
class Quadruple <T, K, V, R> {
    var first: T? = null
    var second: K? = null
    var third: V? = null
    var fourth: R? = null
}

typealias IntQuadruple = Quadruple<Int, Int, Int, Int>

fun main() {
    val intQuadruple = IntQuadruple()
    intQuadruple.first = 1
    println(intQuadruple.first)
}
```

- 需要注意的是，***类型别名没有引入新的类型***，他只是在编译时把所有用到类型别名的地方替换为原名

```kt

typealias Name = String

fun printName(name: Name) {
    println("Hello, $name!")
}


fun main() {
    val name: String = "John"
    printName(name)
    // String 也可以使用参数为 Name 的函数，因为本质上 printName 接收的就是 String 类型
}
```

>  包括下面的，虽然顺序错了，但是本质上是一样的

```kt
typealias MyInt = Int
typealias YourInt = Int

fun func(num: MyInt, num2: YourInt) {
    println("num: $num, num2: $num2")
}

fun main() {
    val num: MyInt = 10
    val num2: YourInt = 12
    
    func(num2, num)
}
```

- ***类型别名可以为能在变量声明时冒号右面出现的类型起别名***，其他的并不行

> 类型别名声明后的标识符**可以用在变量类型声明、泛型参数的上界约束、`is` `as` 转换**

```kt
// 比如函数类型，是可以声明为变量冒号右面的，这个是比较使用的，因为面对一堆参数声明一般是没有可读性的

typealias MyHandler = (Int, String, Any) -> Unit

typealias Predicate<T> = (T) -> Boolean

// 还有内部类

class A {
    class Inner
}
class B {
    class Inner
}

typealias AInner = A.Inner
typealias BInner = B.Inner

// 单例

object Test {
    fun doSomething() {
        println("Hello, world!")
    }
}

typealias printSomething = () -> Unit
typealias Print = Test

fun main() {
    val doSomething: printSomething = { Print.doSomething() }
    doSomething()
}

// 包括带有泛型参数位置的类型别名

class MyClass <T> (val x: T)

typealias MyAlias<T> = MyClass<T>

fun main() {
    val myAlias: MyAlias<Int> = MyAlias(10)
    println(myAlias.x)
}

// 可空类也是可以的，因为它也可以出现在变量声明的右面

class Test (val name: String)

typealias TestAlias = Test?

fun main() {
    val test: TestAlias = null
    println(test?.name)
}
```

- 你可能会想到 `import as` ，它与类型别名有什么区别吗？

|目标|类型别名|import as|
|:---:|:---:|:---:|
|类和接口|✔|✔|
|可空类|✔|✘|
|泛型参数未知的泛型类型|✔|✘|
|有泛型参数的泛型类型|✔|✘|
|函数类型|✔|✘|
|枚举|✔|✔|
|枚举对象|✘|✔|
|object|✔|✔|
|object 里的函数|✘|✔|
|object 里的属性|✘|✔|

- 同样的，类型别名和函数式接口的区别也是，类型别名没有引入新的类型



# 第九章：引用和反射

> 这是第一次使用非标准库的特性，记住***本章的大部分内容都要导入 `kotlin.reflect` 库***，对于使用 JVM 的读者可以直接使用，无需添加依赖项

- 如果你没有接触过 Java 的反射，简单说***反射（reflection）就是在运行时动态获取类、对象、方法的信息***

> 请注意，引用和反射是最后一章会引入新概念的章节，之后的所以内容都是基于前九章内容的扩展和丰富，因此请扎实理解本篇内容

## 9.1 顶层函数的引用

> 上文中我们讲过 Kotlin 里的函数是一等公民，函数可以当作对象来实现，下面我们对此进行深入探索

- 双冒号用于引用一个函数，而*函数类型*的本质就是一个实现了 `kotlin.jvm.functions.FunctionN` 接口的对象，函数体就保存在 `invoke` 里面

```kt
// JVM 上的 Functions 定义

package kotlin.jvm.functions

/** A function that takes 0 arguments. */
public interface Function0<out R> : Function<R> {
    /** Invokes the function. */
    public operator fun invoke(): R
}

/** A function that takes 1 argument. */
public interface Function1<in P1, out R> : Function<R> {
    /** Invokes the function with the specified argument. */
    public operator fun invoke(p1: P1): R
}

/** A function that takes 2 arguments. */
public interface Function2<in P1, in P2, out R> : Function<R> {
    /** Invokes the function with the specified arguments. */
    public operator fun invoke(p1: P1, p2: P2): R
}

// ``` 一共有 22 个，但不代表你不能使用超过 22 个参数的函数类型
```

> 所以请看下文

```kt
// 因为是默认函数类型，所以无需导包

fun func1(str: String) {
    println("Hello, $str!")
}

fun func2(func: (String) -> Unit) {
    func("Kotlin")
}

fun main() {
    val func3 = ::func1
    func2(func3)
    func2.invoke("Python")
    
    val func4: Function1<String, Unit> = ::func1
    // Functions1 表示该函数类型有一个参数，有几个参数就是 Function 几
    // 泛型参数里的类型，最后一个是函数返回值类型，前面的都是函数参数的类型，顺序不能错
    // func4 和 func2 是一样的
    func4("Java")
    func4.invoke("CPP")
    // func1.invoke 同理，func2 就 func 4 的函数体就保存在 invoke 里面，但是普通函数 func1 没有
}
```

- 所谓***函数类型的对象，其实也是 SAM 类型***，只不过 Kotlin 原生提供了支持，它们的***函数体都保存在 `invoke` 方法***里，而且 **`invoke` 可以重载**，所以你也可以对一个类的对象像是使用函数一样调用

```kt
data class User (val name: String, val age: Int) {
    operator fun invoke(greeting: String) {
        println("$greeting, my name is $name and I am $age years old.")
    }
}

fun main() {
    val user = User("John", 30)
    user("Hello")
    // 注意是 user 对象可以直接调用，而不是 User
}
```

> 还有骚操作

```kt
// 一般写法

interface SAM {
    fun func() 
}


fun main() {
    val sam = object : SAM {
        override fun func() {
            println("Hello, world!")
        }
    }

    sam.func()
}

// invoke 写在伴生对象里面也是可以的，只要他不访问类

interface SAM {
    fun func()

    companion object {
        operator fun invoke(f: () -> Unit): SAM {
            return object : SAM {
                override fun func() {
                    f()
                }
            }
        }
    }
}


fun main() {
    val sam = SAM { println("Hello, world!") }
    /* 等于
    val sam = SAM.invoke() {
        println("Hello, world!")
    }
    */

    sam.func()
}
```

- 还可以**声明 `FunctionN` 接口的实现对象，重载 `invoke` 方法**，实现自己的函数类型

```kt
fun main() {
    val func:Function1<String, Unit> = object : Function1<String, Unit> {
        override fun invoke(p1: String) {
            println("Hello, $p1!")
        }
    }

    func("Kotlin")

    // 函数类型的对象本质上也是这样
}
```

- 引入 `kotlin.reflect.*` 后，我们还可以***使用 `KFunction` 当作函数类型对象的类型***，它提供了更多在运行时可以与函数互动的操作，***`KFunctionN` 和`FunctionN` 兼容，可以互相转换***

```kt
import kotlin.reflect.KFunction1
// 或者 import kotlin.reflect.* 不然的话每一种参数的函数都要导入

fun func1(str: String) {
    println("Hello, $str!")
}

fun func2(str: String, func: (String) -> Unit) {
    func(str)
}


fun func3(str: String, func: KFunction1<String, Unit>) {
    println("func is a ${if (func.isFinal) "final" else "open"} function")
    // 是否 open 或者 final 等信息

    println("func name is ${func.name}")
    // 函数名

    println("enter the argument:")
    func.call(readln())
    // 调用函数，类似 invoke
}

fun main() {
    val func: KFunction1<String, Unit> = ::func1
    func2("Kotlin", func)

    func3("Reflection", func)
    func3("Reflect", ::func1 as KFunction1<String, Unit>)

    func.invoke("1")
    func.call("2")
    // 都是可以的
}
```

- 具体每一种 `KFunctionN` 都有哪些方法，可以参考[官方文档](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.reflect/-k-function/)

## 9.2 类的引用

### 9.2.1 Java 中的反射

> 因为**反射是在运行时动态反射**，而 Kotlin 是一门 JVM 语言，所以 ***Java 里的反射 API 也适用于 Kotlin***

> 如果对 Java 的反射不了解的话，可以看[Reflecting in Java](https://www.bilibili.com/video/BV1K4421w7zP/)，这位老哥讲的很清楚，因为这里是 Kotlin 所以就不过多讲解了

- 要想在 Kotlin 里获得一个类的类引用，使用 ***`类名::class` 的方法，返回一个 `KClass` 对象***，如果想要使用 Java 的类对象，可以使用 ***`类名::class.java` 方法，返回的是 `java.lang.Class` 对象，对它可以使用 Java 的反射 API 来操作***

> Kotlin 这里反射的 API 明显不如 Java 丰富，大部分情况下需要使用 ***`Java CLass` 和 `KClass`*** 互相转换，***二者都可以通过 `.java` `.kotlin` 互相转换***

- **一个 `Class` 对象是虚拟机在运行时保存的类的信息，每一个类都有自己的类对象，要想使用 Java 的方式获取类对象，有如下三种方法**

```kt
data class Person(val name: String, val age: Int) {

    fun finalFun() {
        println("This is a final function")
    }

    open fun openFun() {
        println("This is an open function")
    }

    init {
        println("This is an init block")
    }

    companion object {

        fun companionFun() {
            println("This is a companion function")
        }

        val companionVal = "This is a companion val"

        init {
            println("This is a companion init block")
        }
    }
}


fun main() {
    val personClass1: Class<Person> = Person::class.java
    // 等于 Class<Person> personClass1 = Person.class; 这个泛型参数里的类型是 Person，因为在编译时可知
    println()

    val person = Person("John", 25)
    val personClass2: Class<Person> = person.javaClass
    // 等于 CLass<?> personClass2 = person.getClass(); 这个是通过已有实例的方法获取它的类对象，注意到 Kotlin 这边 Class 的泛型类型是可知的

    println()
    val personClass3: Class<*> = Class.forName("Person")
    // 泛型参数里的 * 表示不知道具体的类型，因为在运行时才知道具体的类型，所以只能用 out Any 作为参数类型
}
```

- 这个 Class 类对象有很多方法，***一般来说 `getDeclaredXXX` 方法可以获取类声明的所有成员，甚至 `private` 的，但是无法获取父类继承给自己的，`getXXX` 获取该类所有成员包括从父类继承而来的，但是无法访问 `private` 的***

- ***可以获取 `Field`（属性） `Method`（方法）`Constructor`（构造器）***

> 理论上 Kotlin 应该会自动导入 `java.lang.*` 在 JVM 平台上，可是我发现如果你不显性的声明对象的类型，是可以不导入的；但一旦出现 `Field` `Method` 等词就会说必须导入

```kt
import java.lang.reflect.Constructor
import java.lang.reflect.Field
import java.lang.reflect.Method


data class Person(val name: String, val age: Int) {

    fun finalFun() {
        println("Person is having a final fun")
    }

    init {
        println("Person is being initialized")
    }

    constructor() : this("Default Name", -1) {
        println("secondary constructor is being called")
    }

    val tulple = Pair(1, "Hello")

    fun funcWithParam(param: String) {
        println("Person is having a function with param: $param")
    }

    companion object {
        fun companionFun() {
            println("Companion object is having a fun")
        }

        var companionVar = 10

        init {
            println("Companion object is being initialized")
        }
    }
}



fun main() {
    val clazz: Class<*> = Class.forName("Person")
    val fields: Array<Field> = clazz.getDeclaredFields()
    // val fields: Array<Field> = clazz.getFields() 获取所有公开的字段，包括继承而来的字段，注意 Kotlin 默认字段是 private 的
    // val fields = clazz.getSuperclass().getDeclaredFields() 获取所有父类的字段
    for (field in fields) {
        println("field name: ${field.name}, type: ${field.type}")
        // println("field name: ${field.getName()}, type: ${field.getType()}")
        // 这里使用的是 Kotlin 为 Java 方法设置的扩展属性方式，本质上完全一样，后文也会经常这样用，注意一下
    }
    println()

    val field = clazz.getDeclaredField("age") // 获取指定字段
    println(field.name)
    // val field = clazz.getField("hello") 由于是运行时反射，所以编译时不会报错，而是在运行时抛异常
    println()

    println(clazz.getDeclaredField("tulple").getGenericType()) // 获取字段的泛型类型，否则是类型擦除后的类型
    println()

    val methods: Array<Method> = clazz.getDeclaredMethods()
    // 同上，获取声明的方法
    for (method in methods) {
        println(method.getName())
    }
    println()

    val anotations: Array<Annotation> = clazz.getAnnotations()
    // 获取注解，默认会有一个 MetaData 的注解
    for (annotation in anotations) {
        println(annotation)
    }
    println()

    val constructors: Array<Constructor<*>> = clazz.getConstructors()
    // 获取构造方法
    for (constructor in constructors) {
        println(constructor.getName())
    }
    println()

    val staticVal: Field = clazz.getDeclaredField("companionVar")
    staticVal.setAccessible(true)  // 设置为可访问，因为字段默认 private
    staticVal.setInt(Person(), 99) // 这是直接吧默认值改了，而不是某一个实例的值
    println(staticVal.getInt(Person()))
    // 与 Java 真 static 不同，Kotlin 里面的伴生对象里的成员都不是静态的，所以必须给一个外部类的对象
    // 就像 Java 里的静态内部类，如果访问静态内部类里的静态成员无需实例，但是访问静态内部类的正常成员也是需要实例的
    println()

    val finalMethod: Method = clazz.getDeclaredMethod("finalFun")
    finalMethod.invoke(Person()) // 对于每一个类成员的调用，你必须传入一个类的实例作为第一个参数，让他们知道自己是谁的
    println()

    val funcWithParamMethod: Method = clazz.getDeclaredMethod("funcWithParam", String::class.java) // 参数类型作为第二个
    funcWithParamMethod.invoke(Person(), "Hello") // 调用带参数的方法，传入参数类型和参数值
    println()

    val constructor: Constructor<*> = clazz.getConstructor(String::class.java, Int::class.java) // 获取带参数的构造方法
    // val constructor = clazz.getDeclaredConstructor() // 获取无参数的构造方法
    val person: Any = constructor.newInstance("Alice", 25) // 注意 person 是 Any 类型，因为是运行时才知道
    if (person is Person) {
        // 确保类型安全
        println(person.name)
        println(person.age)
        println()
        // 也可以通过 clazz.cast() 转换类型，不过由于是运行时才知道 clazz 类型，所以只能对通过字面量获得的类对象有效，像这里的字符串是不行的

        val field = clazz.getDeclaredField("name")
        field.setAccessible(true)
        field.set(person, "Bob")
        // 即便是 private final 字段，也可以直接修改
        println(person.name)
        println()

        val method = clazz.getDeclaredMethod("finalFun")
        method.setAccessible(true)
        // 可以访问 final (默认都是 final 的)方法，但不可以访问 private 方法和 private final，我也不知道为啥
        method.invoke(person)
    }
}
```

### 9.2.2 Kotlin 中的反射

- 上面说了，***使用 `类名::class` 就能获得 `KClass` 类型的对象***，因为有类型推断的存在，很多时候我们不需要显式地声明类型，也不用管具体是不是编译时才可知

- 这个 **`KClass` 里面只有一些简单的判断某个类是不是 Kotlin 里面的特殊类的方法**

```kt
import kotlin.reflect.KClass

data class Person(val name: String, val age: Int)

fun main() {
    val personClass = Person::class
    println(personClass.simpleName)
    println(personClass.isData)
}
```

![](https://i-blog.csdnimg.cn/blog_migrate/385f77981f408b9c5a975c7d129aa9d4.png)

> 这是 Kotlin 和 Java 里面反射类的组织结构

- 当然也有很多很好用的方法，具体就不细讲了，可以参考[官方文档](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.reflect/-k-class/)，里面肯定比我说的详细

```kt
import kotlin.reflect.full.functions
import kotlin.reflect.jvm.jvmName

data class Person(val name: String, val age: Int)

fun main() {
    val personK = Person::class
    personK.isInstance(Person("John", 25)) // 参数是不是该类的实例
    println(personK.functions)
    println(personK.jvmName)
}
```

## 9.3 方法的引用

- 要***引用一个类中的方法，使用 `类名::方法名` 的方式，得到的是一个 `KFunctionN` 类型的对象，调用时必须传入一个类的实例作为第一个参数***

> 因为是类中的方法，所以他必须知道是谁在调用我

```kt
import kotlin.reflect.KFunction2


data class Person(val name: String, val age: Int) {
    fun func(str: String) {
        println("Hello, $str!")
    }
}


fun main() {
    val func: KFunction2<Person, String, Unit> = Person::func
    func(Person("Alice", 25), "world")
}
```

### 9.3.1 扩展函数的引用

- 同理，***扩展函数也可以被引用，也是 `被扩展类::扩展函数名` 的格式，引用时也必须传入一个类的实例作为第一个参数，或者显性声明这是个扩展函数的引用函数类型***

> 就跟成员函数的引用一样，我要知道是谁在调用我

```kt
import kotlin.reflect.KFunction1

fun Int.isEven() = this % 2 == 0

fun main() {
    val isEven1: Int.() -> Boolean = Int::isEven
    val isEven2: (Int) -> Boolean = Int::isEven
    val isEven3: KFunction1<Int, Boolean> = Int::isEven
    
    println(12.isEven1())
    println(isEven2(75))
    println(isEven3(100))
}
```

- 而且对于第一种引用类型，***它既可以作为成员函数调用，也可以作为带有实例参数的普通方法调用***

```kt
import kotlin.reflect.KFunction1

fun Int.isEven() = this % 2 == 0

fun main() {
    val isEven1: Int.() -> Boolean = Int::isEven
    val isEven2: (Int) -> Boolean = Int::isEven
    val isEven3: KFunction1<Int, Boolean> = Int::isEven

    println(12.isEven1())
    println(isEven1(12))
}
```

- 而且二者还可以互相转换，***你可以把有接收者的函数赋给无接收者的函数，反过来也是可以的***

```kt
fun Int.isEven() = this % 2 == 0

fun isOdd(n: Int) = n % 2!= 0

fun main() {
    val fn1: (Int) -> Boolean = Int::isEven
    val fn2: Int.() -> Boolean = ::isOdd
    val fn3: (Int) -> Boolean = fn2
    val fn4: Int.() -> Boolean = fn1
}
```

- 那如果***扩展函数同时还是成员函数***呢？这个时候它的调用者又是谁？是他的扩展接收者，还是所在的类？

> 之前讲过的所以扩展函数都是顶层的，这里扩充下知识点

- 这样的话***它既是所在类的成员函数，又是一个 `Int` 的扩展函数***，也就意味着你***只能在 `MyClass` 实例上调用 `isEven()` 方法***，不能在外部 `Int` 实例上调用，因为外部 `Int` 实例访问不到 `isEven()` 方法

```kt
class MyClass {
    fun Int.isEven() = this % 2 == 0
    
    fun func() {
        println(4.isEven())
    }
}

fun main() {
    // 4.isEven() 报错
}
```

### 9.3.2 隐式的接收者

- 这个***接收者，在 Kotlin 里面叫 `receiver`***，也就是 `this` 差不多，指的是成员所在的类或扩展函数被扩展的类

> 大部分情况下，接收者是可以不写的（就像你在类里面的成员是可以不写 `this.` 的），除非像内部类嵌套时需要通过 `this@label` 的写法指定接收者，所以也叫***隐式的接收者（implicit receiver）***

- 像上面这样的叫做***双重接收者***，如果真的想要使用它，可以***通过多重嵌套函数的方法同时指定多重接收者***

```kt
// 1

class MyClass {
    fun Int.isEven() = this % 2 == 0

    fun func(fn: MyClass.() -> Unit) {
        fn()
        // 等于 this.fn() ,隐式的接收者是 MyClass
    }
}

fun main() {
    val myClass = MyClass()
    myClass.func { // 隐式接收者是 MyClass
        println(2.isEven()) // 又是 Int 的接收者，同时满足 isEven() 的条件
    }
}
```

### 9.3.3 作用域函数

> 上面所说的特定作用域下的接收者，其实 Kotlin 已经为我们提供了很多方便的语法糖，这些函数的具体使用方法如下

- Kotlin 标准库包含多个函数，其唯一目的是***在对象的上下文中执行代码块***。当您在提供 lambda 表达式的对象上调用此类函数时，它会形成一个临时作用域，***在此范围内，您可以访问不带其名称的对象***，此类函数称为***作用域函数***

> 如以下例子：

```kt
data class Person(var name: String, var age: Int, var city: String) {
    fun moveTo(newCity: String) { city = newCity }
    fun incrementAge() { age++ }
}

fun main() {
    Person("Alice", 20, "Amsterdam").let {
        println(it)
        it.moveTo("London")
        it.incrementAge()
        println(it)
    }
}
```

- 一共有***五个作用域函数，`let` `also` `run` `with` `apply`，他们接受一个 `lambda` 表达式作为参数，并返回一个值***

- 这些函数都是在对对象执行 `lambda` 里面的代码，唯一***不同的点在于对象的格式，和 `lambda` 的返回值***

|名称|对象引用的名称|返回值|是扩展函数?|
|----|:----:|:----:|:----:|
|`let`|it|Lambda 表达式的返回值|是|
|`run`|this|Lambda 表达式的返回值|是|
|`run`||Lambda 表达式的返回值|否，可以不带上下文时调用|
|`with`|this|Lambda 表达式的返回值|否，将上下文对象作为参数|
|`apply`|this|调用对象|是|
|`also`|it|调用对象|是|

- ***`let` 和 `also` 接受的 `lambda` 参数里可以不用对每一次调用都做非空判断***，直接使用 `it.成员` 调用即可，区别在于二者 ***`let` 返回 `lambda` 的最后一行表达式作为返回值***，而 ***`also` 返回扩展函数的接收者本身***

```kt
data class Person(var name: String, var age: Int)

fun Person.doSomething(func: (it: Person) -> Unit) {
    func(this)
}

fun main() {
    val person = Person("Alice", 30)

    // 使用 let
    val resultLet = person.let {
        println("Inside let: ${it.name}, ${it.age}")
        it.age
        // it?.age 无需作非空判断
    }
    println("Result of let: $resultLet")  // 输出: Result of let: 35

    // 使用 also
    val resultAlso = person.also {
        println("Inside also: ${it.name}, ${it.age}")
        // also 返回调用它的对象
    }
    println("Result of also: ${resultAlso.name}, ${resultAlso.age}")  // 输出: Result of also: Alice, 30

    val nullPerson: Person? = null

    // 如果不使用 let，每一此调用都需要 ?. 进行非空判断
    println("Before using let: ${nullPerson?.name}, ${nullPerson?.age}")
    println("Before using let: ${nullPerson?.name}, ${nullPerson?.age}")


    val resultLetNull = nullPerson?.let {
        println("Inside let: ${it.name}, ${it.age}")
        println("Inside let: ${it.name}, ${it.age}")
        // it?.age 无需作非空判断
    }
    println(resultLetNull)

    // 因为 ?. 是非空就不执行，所以上面的 let 根本不会执行（返回了 null），但是下面的 let 会执行，可是里面又必须非空检测
    nullPerson.let {
        println("Inside let: ${it?.name}, ${it?.age}")
    }

    // 类似如下
    nullPerson?.doSomething {
        println("Inside doSomething: ${it.name}, ${it.age}")
    }
}
```

- `it` 只是 `lambda` 默认的单参数参数名，你也可以自定义

```kt
data class Person(var name: String, var age: Int)

fun main() {
    val person = Person("Alice", 25)

    person.let { value: Person ->
        println("Name: ${value.name}, Age: ${value.age}")
    }
}
```

- 除了传递 `lambda` ，还***可以传递函数引用***

```kt
data class Person(val name: String, val age: Int)

fun main() {
    val person = Person("John", 25)
    person.let(::println)
    person.let { println(it) }
    // person.let { ::println } ，这是不行的
}
```

- ***`with` 把调用对象作为参数，传给 `lambda` 的参数是隐式的 `this`，所以使用的时候可以直接拿成员名称调用，同样把 `lambda` 的返回值作为返回值***

```kt
data class Person(var name: String, var age: Int)

fun main() {
    val person = Person("John", 25)

    with(person) {
        println("Name: $name, Age: $age")
        // 等于如下，this 是隐式的接收者，相当于是在类里面使用
        println("Name: ${this.name}, Age: ${this.age}")
    }

    val nullPerson: Person? = null

    println(with(nullPerson) {
        println("Name: ${this?.name}, Age: ${this?.age}")
        // 不具备非空判断功能，直接用会报空指针异常

        this?.name ?: "null name"
    })
}
```

> 一般 `with` 会用在不返回值的地方，把要一系列调用的成员放在 `with` 里面同意调用

- ***`run` 和 `apply` 这两个函数相当于 `let + with` `also + with`，不需要作非空判断，里面可以直接调用对象的方法（隐式的 `this`）***

- 区别在于 ***`run` 返回的是 `lambda` 的返回值***，而 ***`apply` 返回的是调用对象本身***

- ***`apply` 只能作为扩展函数调用***，但是 ***`run` 既可以作为扩展也可以作为普通的单参数 `lambda` 函数来使用***

```kt

data class Person(var name: String?, var age: Int?)

fun main() {
    val person = Person("Alice", 30)

    // 使用 run
    val resultRun = person.run {
        println("Inside run: $name, $age")
        age = 31
        age
    }
    println("Result from run: $resultRun")

    // 使用 apply
    val resultApply = person.apply {
        println("Inside apply: $name, $age")
        age = 32
    }
    println("Result from apply: $resultApply")

    val complexNumber = run {
        // run 还可以作为单独的表达式，这就很适合单个表达式无法声明的变量赋值，需要声明一些临时的变量
        
        val n = 1.0
        val m = 2.0

        n + m
    }
    println("Complex number: $complexNumber")

    // 打印最终的 person 对象
    println("Final person: $person")
}
```

> 注意 `run` 单独拿来使用的时候，不像 `with` 一样能有接收者，只能用一个 `lambda` 传给他作为它唯一的参数

- 因为 ***`apply` `also`  返回的是调用对象本身，所以你可以链式调用***，比如如下

> `also` 基本上也就用在链式调用的地方，逻辑清晰

> 链式调用很像 Java 的 Stream API，Kotlin 真是用惯了 Java 的人写出来的

```kt
data class NumBox<T : Number>(var value: T) {
    fun add(t: T) {
        value += t
    }
}


operator fun <T : Number> Number.plus(other: T): T {
    return when (this) {
        is Int -> this + other.toInt()
        is Double -> this + other.toDouble()
        is Float -> this + other.toFloat()
        is Long -> this + other.toLong()
        is Short -> this + other.toShort()
        is Byte -> this + other.toByte()
        else -> 0
    } as T
}

fun main() {
    val nb = NumBox(1)
    nb.also { println(it)
    }.apply {
        add(2)
        add(3)
        add(4)
    }.also { println(it) }
}
```

> `run` 用在既返回值又初始化对象的地方很好用

> `apply` 一般使用在对象配置的时候，不需要返回其他值的地方

```kt
data class Person(var name: String, var age: Int = 0, var city: String = "")

fun main() {
    val adam = Person("Adam").apply {
        age = 32
        city = "London"        
    }
    println(adam)
}
```

> 需要注意的，上文所有的作用域函数因为都能拿到对象的引用，所以他是真的在修改对象的成员，而不是只返回一个新的对象，如果不明白的话看上面说过的传值引用

- 还有 `takeIf` `takeUnless` 这两个扩展函数，有的时候我们想对经过链式调用的对象做一些简单的 `if` 判断，但又不想新建一个临时变量，可以使用他们

- ***`takeIf` 接受一个 `lambda` 表达式作为参数，如果 `lambda` 返回 `true` 则返回对象本身，否则返回 `null`，注意要进行安全调用 `?.`***

- ***`takeUnless` 相反，如果 `lambda` 返回 `false` 则返回对象本身，否则返回 `null`***

```kt
data class Person(val name: String, val age: Int)

fun main() {
    val person = Person("John", 25)
    person.run {
        age
    }.takeIf {
        it % 2 == 0
    }?. run {
        println("this guy's age is even")
    }
}
```

> 这样看起来更优雅了不是？不过看代码的人就要疯了，用的时候注意可阅读性就好

- 讲了这么多，回到我们一开始的问题，对于有双重接受者的扩展函数，你也可以这样调用

```kt
class MyClass {
    fun Int.isEven() = this % 2 == 0
}

fun main() {
    val myClass = MyClass()
    println("10 is even? ${
        myClass.run {  // 隐式接收者是 MyClass
            with (23) { // 显式接收者是 Int
                isEven() // 同时满足
            }
        }
    }")
}
```

### 9.3.4 构造函数的引用

- **构造函数本质上就是一个接受构造参数，返回类对象的函数**，想要***引用构造，使用 `::类名` 的写法***

> 构造函数也是 `KFunctionN` 类型

```kt
data class Person(var name: String, var age: Int) {
    constructor() : this("Default Name", 0)
}

fun makePerson(name: String, age: Int, func: (String, Int) -> Person): Person {
    val person = func(name, age).apply {
        println("Person has been created with name: $name and age: $age")
        this.name = "Updated Name"  // 因为 name 和函数参数冲突了，本地优先他会以为我要修改函数参数，后者在 Kotlin 里面是 val 的
        this.age += 10
    }

    return person
}

fun main() {
    val person = makePerson("Harsh", 25, ::Person).apply {
        println("Person has been updated with name: $name and age: $age")
    }
}
```

> 说实话这个作用域函数真爽，相见恨晚

- ***引用构造函数时必须显性的声明构造函数的参数***，不支持引用重载

```kt
data class Person(var name: String, var age: Int) {
    constructor() : this("Default Name", 0) {
        println("Person has been created with default values")
    }
    
    init {
        if (name != "Default Name" || age!= 0) println("Person has been initialized with non-default values")
    }
}


fun main() {
    val cst1: (String, Int) -> Person = ::Person
    val cst2: () -> Person = ::Person
    // val cst3 = ::Person 报错，因为重载
}
```

- Kotlin 里的 **`KClass` 有一个 `primaryConstructor` 属性，可以拿到类的主构造函数**，不用手动判断了

```kt
import kotlin.reflect.KClass
import kotlin.reflect.full.primaryConstructor

data class Person(val name: String, val age: Int) {
    constructor() : this("Default Name", 0)
}

fun main() {
    val kclass: KClass<Person> = Person::class
    println(kclass.primaryConstructor)
}
```

## 9.4 属性的引用

- 要想***引用一个类中的属性，使用 `类名::属性名` 的方式***，因为 Kotlin 的属性都自动封装了 `getter` 和 `setter`，所以本质上跟 `KFunction` 也差不多

- 如果该属性是不可变变量 `val`，这样返回一个 ***`KProperty` 对象，他跟 `KFunction` 一样继承了 `KCallable` 接口***，都属于可调用

```kt
import kotlin.reflect.KProperty1

data class Person(val name: String, val age: Int)

fun main() {
    val kName: KProperty1<Person, String> = Person::name
    // KProperty1说明有一个参数，类型是 Person，返回值是 String
    println(kName.get(Person("Alice", 25)))
}
```

- 当我们对一个 ***`KClass` 调用 `members` 属性时返回的就是一个 `Collection<KCallable<*>>` 的集合，里面包括了所有可调用的方法，也包括属性的访问器***

```kt
import kotlin.reflect.KClass

data class Person(val name: String, var age: Int)

fun main() {
    val kclass: KClass<Person> = Person::class
    for (f in kclass.members) {
        println(f.name)
    }
}
```

- 注意到 ***`KProperty` 一共有 `KProperty0` `KProperty1` `KProperty2` 三种实现***，其中 ***`KProperty1` 对应着普通类中属性的引用***，唯一的参数就是调用者对象，***`KProperty0`  对应着顶层属性和伴生对象属性的引用***，他们不需要调用者，***`KProperty2` 对应着有双重接收者属性的引用***

> `KProperty2` 比较特殊，一般情况下你是不能引用一个双重接收者的函数的，同样也不能引用位于类中的扩展属性，不知道有没有人知道怎样才能引用

```kt
// 普通扩展属性的引用

val String.lastChar: Char
    get() = this[length - 1]

fun main() {
    println(String::lastChar.get("abc"))
}
```

- ***引用一个顶层属性，使用 `::属性名`*** 的写法，***引用一个伴生对象里的属性跟引用正常属性格式相同***

> 其实 `KProperty0` 引用的都是静态属性

```kt
import kotlin.reflect.KProperty0
import kotlin.reflect.KProperty1
import kotlin.reflect.KProperty2

data class Person(val name: String, val age: Int) {
    val String.lastchar
        get() = this[length - 1]

    companion object {
        val nameC = "23312"
    }
}

val nameTop = "John"

fun main() {
    val nameK: KProperty1<Person, String> = Person::name
    val topK: KProperty0<String> = ::nameTop
    val nameC: KProperty0<String> = Person::nameC
}
```

- ***对于 `KProperty0` 可以直接取值，而 `KProperty1` 需要传入接收者对象***

```kt
import kotlin.reflect.KProperty0
import kotlin.reflect.KProperty1
import kotlin.reflect.KProperty2

data class Person(val name: String, val age: Int) {
    val String.lastchar
        get() = this[length - 1]

    companion object {
        val nameC = "23312"
        fun doSomething() {
            println("do something")
        }

        init {
            println("static init")
        }
    }
}

val nameTop = "John"

fun doSomething(name: String) {
    println(name)
}

fun main() {
    val nameK: KProperty1<Person, String> = Person::name
    val topK: KProperty0<String> = ::nameTop
    val nameC: KProperty0<String> = Person::nameC
    println() // static init 初始化

    println(nameC.get())
    println(nameTop)
    println(nameK.get(Person("Alice", 25)))
}
```

- 如果是***可变变量 `var` ，则这个属性类型是 `KMutablePropertyN`，会多一个 `set` 方法***

```kt
import kotlin.reflect.KMutableProperty1

data class Person(val name: String, var age: Int)

fun main() {
    val person = Person("John", 25)
    val ageK: KMutableProperty1<Person, Int> = Person::age

    println(ageK.isConst)
    println(ageK.isFinal)
    // 还有很多操作
    
    ageK.set(person, 30)
    println(person.age)
}
```

> 具体 `KProperty` 的方法，请看[官方文档](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.reflect/-k-property/)，这里不对每一种进行讲解

## 9.5 参数的引用

- ***对 `KCallable` 使用 `parameters` 属性可以拿到它的所有参数，返回的是一个 `KParameter` 的集合，可以查看函数的参数信息***

> [KCallable 官方文档](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.reflect/-k-callable/)

- Kotlin 把***参数分为三类，分别是函数的参数 `KParameter`、函数的返回值 `KType` 和泛型的类型参数 `KTypeParameter`***

```kt
import kotlin.reflect.KClass
import kotlin.reflect.KCallable

data class Person(val name: String, val age: Int)

fun main() {
    val kc: KClass<Person> = Person::class
    for (m in kc.members) {
        print("${m.name} -> ")
        for (p in m.parameters) 
            print("${p.type}\t")
        println()
    }
}
```

> [KParameter 官方文档](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.reflect/-k-parameter/)

```kt
import kotlin.reflect.KClass
import kotlin.reflect.KCallable

data class Person(val name: String, val age: Int)

fun main() {
    val kc: KClass<Person> = Person::class
     for (m in kc.members) {
         println("${m.name} return ${m.returnType}")
     }
}
```

> [KType 官方文档](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.reflect/-k-type/)

```kt
import kotlin.reflect.KClass
import kotlin.reflect.KCallable

data class Person <T> (val name: String, val age: T) {
    fun <K> doSomething(k: K) {
        println("Doing something with $name and $age, and $k")
    }
}

fun main() {
    val kc: KClass<Person<*>> = Person::class
     for (m in kc.members) {
         println("${m.name} typeParameters: ${m.typeParameters}")
     }
}
```

> [KTypeParameter 官方文档](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.reflect/-k-type-parameter/)

## 9.6 绑定的引用

- 之前我们讲过的引用，只要是位于类里面的，在调用时都要传入一个对象作为它的第一个参数，但是有些时候可能我们为了方便并不像这么做，所以 ***Kotlin 也允许你引用一个实例对象上的成员，使用 `对象名::成员名`*** 的方法，这样在使用的时候会被换为实际成员的调用，并且**无需指定调用者**

```kt
data class Person(val name: String, val age: Int) {
    fun printSelf()= "My name is $name and I am $age years old."

}

fun main() {
    val strLen = "Hello, Kotlin!"::length
    println(strLen())
    // 注意是这是个方法，只不过不用传指定的调用者，不是普通的属性

    val person = Person("Alice", 25)::printSelf
    println(person())
}
```

> 官网这里用了一个***正则表达式***（Regex Expression）的例子来说明，我就不讲了，可以看下[Kotlin 正则表达式](https://geek-docs.com/kotlin/kotlin-tutorial/regularexpressions.html)、[正则表达式速查表](https://cheat-sheet.cn/post/regex-cheat-sheet/)、[Kotlin Regex API](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-regex/) 这几个网站自行了解

```kt
fun main() {
    val isNumber = Regex("\\d+")::matches // 也可以使用 "\\d+".toRegex()::matches 的方式生成 Regex 对象
    println("Enter something:")
    readln().run {
        if (isNumber(this)) {
            println("It is a number")
        } else {
            println("It is not a number or it is empty")
        }
    }
}
```

## 9.7 属性的委托

> 上面在讲委托的时候只是简单的介绍了类中方法实现的委托，并没有过于深入，其实委托用的最多的地方是这里的属性委托，只不过由于第七章还没有讲泛型和反射，所以放到这里做个总结

- 有些时候我们想对属性的初始化或者赋值拥有更多的操控权，因此 Kotlin 还为我们提供了***属性委托（property delegation）***的机制，通过委托我们可以***自定义属性的访问和赋值***

- 想把一个属性的访问器委托给另外一个对象，只需要***在属性声明时使用 `by` 关键字，并指定委托对象即可***

> 注意这时候该类里面除了有委托对象的方法外，***本身这个委托属性是没有幕后字段的***，他的所有访问都转交给了外部的对象，如果想要使用赋值和设值的话是不能用参数里面的 `KProperty` 的，只能在这个类里面自己设置属性

```kt
import kotlin.reflect.KProperty

class MyClass {
    var varible: String by Delegate()
}

class Delegate {
    private var value: String? = null

    operator fun getValue(thisRef: Any?, property: KProperty<*>): String {
        println("$thisRef, thank you for delegating '${property.name}' to me!")
        return value ?: "value not set yet"
    }

    operator fun setValue(thisRef: Any?, property: KProperty<*>, value: String) {
        println("$value has been assigned to '${property.name}' in $thisRef.")
        this.value = value
    }
}

fun main() {
    val myClass = MyClass()
    myClass.varible = "Hello"
    println(myClass.varible)
    myClass.varible = "World"
}
```

- 需要注意，***被委托对象必须有一个 `setValue` 的操作符函数（`val`），必须有 `setValue` `getValue` 两个操作符函数（`var`）***，函数的参数见上面，其中：
    - ***`thisRef` 必须与属性所有者类型（对于扩展属性必须是被扩展的类型）相同或者是其超类型***
    - ***`property` 必须是类型 `KProperty<*>` 或其超类型***
    - ***`value` 必须与属性类型相同（或者是其超类型）***
    - ***`getValue()` 必须返回与属性相同的类型（或其子类型）***

- ***这两个操作符函数都可以通过成员函数或扩展函数的方式实现***

- ***属性还可以把自己的访问器委托给其他属性，委托的时候使用属性引用***，这种委托***对于顶层和类的属性（成员和扩展）都可用，委托属性可以为***：
    - ***顶层属性***
    - ***同一个类的成员或扩展属性***
    - ***另一个类的成员或扩展属性***

```kt
var topLevelInt: Int = 0
class ClassWithDelegate(val anotherClassInt: Int)

class MyClass(var memberInt: Int, val anotherClassInstance: ClassWithDelegate) {
    var delegatedToMember: Int by this::memberInt
    var delegatedToTopLevel: Int by ::topLevelInt

    val delegatedToAnotherClass: Int by anotherClassInstance::anotherClassInt
}
var MyClass.extDelegated: Int by ::topLevelInt
```

- ***局部变量都可以委托，同样在第一次访问的时候才初始化***

```kt
fun main() {
    fun example(func: () -> String) {
        val value: String by lazy(func)

        if (func() == "Hello") {
            println(value)
        }
    }

    example { "Hello" } // Hello
    example { "World" } // 只有第一次访问才会初始化，这里 value 不会被初始化
}
```

> Kotlin 为我们提供了一些常用的操作方法：

### 9.7.1 lateinit

- 有些时候我们知道这个属性虽然不在初始化的时候就初始化，但是我们使用的时候是一定非空的，就可以使用 ***`lateinit` 标识该变量稍后初始化***，注意的是该修饰符***只能用于在类体中的 `var` 属性（不能是在主构造函数中声明的 `var` 属性，并且仅当该属性没有自定义 `getter` 或 `setter` 时），也用于顶层属性与局部变量，该属性或变量必须为非空类型，并且不能是原生类型***

> 在初始化前访问一个 `lateinit` 属性会抛出一个特定异常，该异常明确标识该属性被访问及它没有初始化的事实

- ***检测一个 `lateinit` 的变量有没有初始化，可以在该变量的引用上调用 `isInitialized`***

```kt
fun main() {
    val user = User()

    // user.printName() Error: lateinit property name has not been initialized
    user.name = "John"

    user.printName()
}

class User {
    lateinit var name: String

    fun printName() {
        if (this::name.isInitialized) {
            println(name)
        } else {
            println("Name is not initialized")
        }
    }
}
```

### 9.7.2 by lazy

- ***延迟属性（lazy property）会委托一个 `lazy` 函数，该函数接受一个 `lambda` 表达式作为参数***，并返回一个 `Lazy<T>` 对象，***该对象在第一次访问时会执行 `lambda` 表达式并缓存结果，之后的访问都直接返回缓存的结果***，可以避免不必要的计算

- 跟 `lateinit`相反，***`lazy` 只能用于 `val` 的属性***

```kt
class MyClass {
    val value: String by lazy {
        println("Enter a string: ")
        readln().run {
            if (this.isEmpty()) {
                "default value"
            } else {
                this
            }
        }
    }
}

fun main() {
    val myClass = MyClass()
    println("Not initialized yet:")
    println(myClass.value)
    println(myClass.value)
    println(myClass.value)
}
```

- ***而且 `lazy` 默认是线程锁***的，该值只在一个线程中计算，但所有线程都会看到相同的值，至于更多见[官方文档](https://book.kotlincn.net/text/delegated-properties.html)

### 9.7.3 observable

- 有些时候我们***想观察某个属性的变化，可以使用 `Delegates.observable` 委托***，该委托接受三个参数：
    - **第一个参数是属性的初始值**
    - **第二个参数是一个函数，该函数的参数被赋值的属性、旧值和新值**

- ***每当我们给属性赋值时会调用该函数（在赋值后执行）***

```kt
import kotlin.properties.Delegates

class Name {
    var name: String by Delegates.observable("John") { prop, old, new ->
        println("($prop) has changed from $old to $new")
    }
}

fun main() {
    val name = Name()
    name.name = "Alice"
    name.name = "Bob"
}
```

- 如果你想对输入的值进行判断再赋值，可以使用 ***`vetoable` 委托***，该委托与 `observable` 委托的区别是***它接受一个函数，该函数的参数是赋值的属性、旧值和新值，如果该函数返回 `false`，则赋值被拒绝，`true` 则接受***

```kt
import kotlin.properties.Delegates

class Num {
    var value: Int by Delegates.vetoable(0) { prop, old, new ->
        println("newer value is ${if (new > old) 
            "greater than the old value, allowed" 
        else 
            "lesser than the old value, not allowed" }"
        )
        new > old
    }
}

fun main() {
    val num = Num()
    num.apply {
        value = 5
        println(value)
    }.apply {
        value = 3
        println(value)
    }.apply {
        value = 7
        println(value)
    }
}
```



# 第十章：集合和序列

- 恭喜你看完了前面的九章，Kotlin 所有基础的东西都包含在这里了，后面的内容只不过是前面内容的扩展和丰富，如果还有不了解的请再多看几遍，你多看几遍花费的时间肯定是比我写这个省时间的

- 下面的内容里会对 Kotlin 里相对独立的几个板块挨个讲解，分别是集合、异常处理、与 Java 互操作、标准库里一些其他东西和多线程

- 加油 💪

> 在经过前面的九章不能使用列表数组的痛苦后，终于可以介绍这个了

## 10.1 数组

> Kotlin 里面的数组和 Java 里的原生数组不太一样，并且里面的值是装箱的，如果需要性能可以使用原生数组（见后文），如果没有特殊需求还是推荐使用列表，列表可以只读，而且很容易增删检查，数组虽然方便取值但是增删元素比较耗时

### 10.1.1 创建数组

- ***创建一个数组，可以使用 `arrayOf()` `arrayOfNulls()` `emptyArray()`  或使用 `Array` 类的构造器***

- ***`arrayOf()` 可以传入多个参数，创建一个包含这些参数的数组***。数组一旦被创建长度就不可变

```kt
fun main() {
    val myArray = arrayOf(1, 2, 3, 4, 5)
    println(myArray)
    println(myArray.joinToString())
    // jotinToString() 带有很多参数
    println(myArray.joinToString(separator = " -> ", prefix = "Start: ", postfix = " End"))
    println(myArray.joinToString(transform = { "Item: $it" }))
}
```

- ***`arrayOfNulls()` 可以创建一个指定长度为空的数组，以后可以进行赋值***，因为每一个元素都是 `null`，所以使用泛型参数需要指定泛型类型

```kt
fun main() {
    val nullArray = arrayOfNulls<Int>(5)
    // val nullArray: Array<Int?> = arrayOfNulls(5) 这样子也可以，因为有类型推断，所以左面右面写类型都可以
    println(nullArray.joinToString())
    println(nullArray.apply {
        for (i in 0..size - 1) {
            if (this[i] == null) {
                this[i] = i
            }
        }
    }.joinToString())
}
```

- ***`emptyArray()` 创建一个空数组***，因为数组长度是不变的，所以***这个数组什么都干不了***，所以***一般赋给的都是 `var` 的变量***，用于初始化占位

> 是用于初始化数组类型的引用变量的，而不是数组里面元素的初始值，所以一般赋值给 `var` 的变量，不然的话他就一辈子不可变一直是空的，那我为什么声明它？

```kt
fun main() {
    var empty = emptyArray<Int>()
    println(empty)
    println(empty.isEmpty())
    empty = arrayOf(1, 2, 3)
    println(empty.joinToString())
}
```

- ***`Array` 类的构造器接受数组的长度，还接受一个 `lambda` 参数，`lambda` 的参数是数组索引，返回值会被赋给索引位置的值***

```kt
fun main() {
    Array<Int>(5) {
        it * it
    }.forEach { print("$it -> ") }

}

// forEach 是一个很方便的函数，他提供给你传入的函数每一个元素，然后执行你函数内的操作
```

- ***也可以创建多维数组马，也就是一个元素为数组的数组***

```kt
fun main() {
    println(Array<Array<Int>>(3) { Array<Int>(3) { 0 } }.contentDeepToString())
    println(Array<Array<String>>(2) {
        Array<String>(2) {
            when {
                it == 0 -> "Hello"
                else -> "World"
            }
        }
    }.contentDeepToString())
}

// joinToString() 由于里面还是数组，所以要用 contentDeepToString()
```

### 10.1.2 索引数组

- ***使用索引操作符中括号 `[]` 来访问或修改数组里的元素，索引从 `0` 开始***

```kt
fun main() {
    val simpleArray = arrayOf(1, 2, 3)
    val twoDArray = Array(2) { Array<Int>(2) { 0 } }

    simpleArray[0] = 10
    twoDArray[0][0] = 2

    println(simpleArray[0].toString())
    println(twoDArray[0][0].toString())
}
```

- ***索引操作符允许重载***，所以也可以对自己的类设定索引的方式

```kt
data class Name(var firstName: String, var lastName: String) {
    operator fun get(index: Int) = when (index) {
        0 -> firstName
        1 -> lastName
        else -> println("Index $index is out of bounds for this Name object")
    }

    operator fun set(index: Int, value: String) = when (index) {
        0 -> firstName = value
        1 -> lastName = value
        else -> println("Index $index is out of bounds for this Name object")
    }


    // 除了正常的取值，还可以使用字符串索引
    operator  fun get(name: String) = when (name) {
        "firstName" -> firstName
        "lastName" -> lastName
        else -> println("$name is not a valid property of Name object")
    }

    operator fun set(name: String, value: String) = when (name) {
        "firstName" -> firstName = value
        "lastName" -> lastName = value
        else -> println("$name is not a valid property of Name object")
    }
}

fun main() {
    val name = Name("John", "Doe").apply { println(this) }

    name.apply {
        println(this[0])
        println(this[1])
        this[0] = "Harry"
        this[1] = "Smith"
        println(this[0])
        println(this[1])
    }.apply {
        println(this["firstName"])
        println(this["lastName"])
        this["firstName"] = "Jenny"
        this["lastName"] = "Doe"
        println(this["firstName"])
        println(this["lastName"])
    }
}
```

- ***索引一个数组，可以直接使用 `for ··· in ···` 循环，也可以使用 `forEach` 函数，数组的 `indices` 属性可以拿到数组的索引范围，`size` 属性可以拿到数组的长度***

```kt
fun main() {
    val array = arrayOf(1, 2, 3, 4, 5)

    for (i in array) {
        println(i)
    }

    for (i in array.indices) {
        println(array[i])
    }

    for (i in 0..(array.size - 1)) {
        // 因为 size 返回的是数组的长度，而数组索引因为从 0 开始所以长度会比 size 小 1
        println(array[i])
    }

    for (i in 0 ..< array.size) {
        println(array[i])
    }

    for (i in 0 until array.size) { // until 就是 ..<
        println(array[i])
    }
}
```

> 同时获得元素索引和元素本身

```kt
fun main() {
    val array = arrayOf(1, 2, 3, 5, 7, 11, 13, 17, 19, 23)
    for (i in array.indices) {
        println("array[$i] = ${array[i]}")
    }
}
```

### 10.1.3 数组的比较

- 数组不可以使用 `==` 比较（也不是不可以），***建议使用 `contentEquals()` 来比较两个数组是否相等***，具体为什么看下面

```kt
fun main() {
    var prime = arrayOf(2, 3, 5, 7, 11, 13, 17, 19, 23)
    val numbers = arrayOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    var primes = prime
    println(prime == primes)
    println(prime === primes)
    println("prime at $prime: ${prime.joinToString()}, primes at $primes: ${primes.joinToString()}")
    // == === 都可用

    primes += 29
    // prime = prime + 29 
    // 数组使用加法是创建了一个新数组，而不是用原先的，可以看下面的打印结果，对象的位置变了
    println(prime == primes)
    println(prime === primes)
    println("prime at $prime: ${prime.joinToString()}, primes at $primes: ${primes.joinToString()}")
    // === 不相等，== 也不相等

    prime += 29
    println(prime == primes)
    println(prime === primes)
    println("prime at $prime: ${prime.joinToString()}, primes at $primes: ${primes.joinToString()}")
    // 这里 === 虽然不等，但是 == 应该是相等的，可是并没有出现如预期的结果
    // 所以建议使用下面的 contentEquals() 来比较两个数组是否相等

    println(prime.contentEquals(primes))

    val p1 = arrayOf(1, 2, 3)
    val p2 = arrayOf(1, 2, 4)
    println(p1 == p2)
    // 这就更明显了，对于对象不同的两个数组 equals 无法判断相等是否
}
```

> ***`var` `val` 的数组并不代表他的元素不可变，只是代表他的引用不可变，可以修改他的元素***，这里 `==` 很想 `===`，检查的是变量的指向而不是指向对象的值

### 10.1.4 原生数组类型

- 需要注意的是，***对于基本类型的数组，其实在编译后是使用的装箱类***的基本类型数组，也就是 `arrayOf(1, 2, 3) == Integers var1 = new Integer[]{1, 2, 3}` ，所以这多少对性能有些损失

- 要***想使用原生类型数组，可以用 `IntArray` `ByteArray` 等等类***，他们编译后的结果对应 Java 里的原生类型数组

- **在普通数组和原生数组之间转换，可以用提供的 `toByteArray()` `toIntArray()` 等等方法**，***也可以用 `toTypedArray()` 来把原生数组转换为普通数组***

```kt
fun main() {
    val array = arrayOf(1, 2, 3, 4, 5)
    val intArray = array.toIntArray()
    val byteArray = Array<Byte>(5) { (it + 1).toByte() }.run { this.toByteArray() }
    // 因为 toByteArray() 接受一个 out Byte 的泛型参数，Int 可不是，所以需要这样新建一个出来
    val charArray = Array<Char>(5) { "${it + 1}".first() }.run { this.toCharArray() }

    println(array.joinToString())
    println(intArray.joinToString())
    println(byteArray.joinToString())
    println(charArray.joinToString())
}
```

- 之前我们讲过**可选参数 `varargs` ，它的运作原理是一个数组**，如果想传入一个***原生数组，也要先进行转换***

```kt
fun <T> func(str: String, vararg args: T) {
    // 这样 args 就可以接受任何类型
    for (arg in args) {
        println("$str: $arg")
    }
}

fun main() {
    val intArray = IntArray(5) { it + 1}
    func("Hello", *(intArray.toTypedArray()))
    func("Hi", args = Array(3) { when (it) {
        // 也可以使用具名参数指定，不过这个时候就需要一个明确的数组了，而不像是可以一个一个传入
        0 -> "Kotlin"
        1 -> "Java"
        2 -> "Scala"
        else -> "Unknown"
    } })
}
```

- 最后讲两个方便的方法，***`sum()` `shuffle()`***，听名字就知道他们是干啥的

```kt
fun main() {
    val array = arrayOf(1, 2, 3, 4, 5)
    println(array.joinToString())
    println(array.sum())
    array.shuffle()
    println(array.joinToString())
}
```

> 数组还有很多方便的方法，具体看[官方文档](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-array/)

- 注意 Kotlin 在有关集合方面的解构函数都只有五个，超过五个的需要自己扩展

```kt
fun main() {
    val array = arrayOf(1, 2, 3, 4, 5, 6)
    println(array.joinToString())

    val (a, b, c, d, e, f) = array
    // 这个解构比较缺德，只有五个，大于五个的没法解构，但是好在这是 Kotlin 可以扩展
    println(a)
    println(b)
    println(c)
    println(d)
    println(e)
    println(f)
}

operator fun <T> Array<T>.component6() = get(5)
```

- `filter()` 函数接受一个 `lambda` 函数，根据 `lambda` 函数的返回布尔值来过滤元素，返回一个新的 `list`

```kt
fun main() {
    val array = arrayOf(1, 2, 3, 4, 5, 6)

    array.filter { it % 2 == 0 }.run { println(this.joinToString()) }
}
```

- `zip` 函数接受两个 `list` 作为参数，返回一个 `list` 列表，其中包含两个 `list` 中对应位置的元素组成的 `pair`

```kt
fun main() {
    val names = arrayOf("Alice", "Bob", "Charlie", "David")
    val hobbies = arrayOf("reading", "swimming", "running", "painting")
    val person = names zip hobbies
    for ((name, hobby) in person) {
        // pair 类型解构
        println("$name loves $hobby")
    }
}
```

## 10.2 集合

### 10.2.1 概念

> 集合在任何一门语言中都是重要的存在，对我们对数据的存取读写提供了方便的操作方式，Kotlin 中的集合位于 `kotlin.collections` 包下，会默认导入

- ***Kotlin 的集合统统基于泛型***，可以存储任何类型的数据，包括基本类型、对象、集合等等

- ***Kotlin 主要有三种集合类型：`list` `set` `map`***
    - ***`list`：是一个有序集合***，元素可以出现多次，可以进行索引访问
    - ***`set`：是一个无序集合，元素不可以重复***，里面只存放唯一值，所谓无序集合说明我们不关心取出来时的顺序，也无法索引
    - ***`map`：是一个键值对集合，每一个键值对都是一个映射，用于存放逻辑关系紧密的数据***，每一个键用来索引值，Python 里的字典就是这种结构

> **数组不是集合**

- 与数组中的元素可以任意修改不同，Kotlin 中的集***合分为 `Collection` `MutableCollection` 两种，前者的元素是不可变的，后者的元素是可变的***

> **这跟 `var` `val` 无关**，这两个只是说明该变量是否可以随意指向，`var` 变量可以重新指向新的集合类型，但是 `val` 不可以

```kt
fun main() {
    val numbers = mutableListOf("one", "two", "three", "four")
    numbers.add("five")   // 这是可以的
    println(numbers)
    //numbers = mutableListOf("six", "seven")      // 编译错误
}
```

- 下面是 Kotlin 集合的继承和实现关系：

![](https://book.kotlincn.net/images/collections-diagram.png)

- ***Kotlin 里面所有的只读集合都是协变的***，也就是 `List<Int>` 是 `List<Any>` 的子类，可以互相引用；反过来，***所有可变集合不是协变的***，也就是 `MutableList<Int>` 不是 `MutableList<Any>` 的子类，不能互相赋值

> 可变集合不协变是为了类型安全，因为如果 `MutableList<Int>` 是 `MutableList<Any>` 的子类，那么 `MutableList<Int>` 里面可以放入 `String` 类型的元素，这违反了类型安全

> 你试一下就知道，***Kotlin 里面的数组是不协变的***，Java 里面数组是协变的，但是集合是不协变的

- **`Collection<T>` 是根层次的集合，它拥有最简单的遍历和取值操作等等**，如果你需要匹配大部分的集合（没错 map 不行）可以使用它

```kt
fun printAll(strings: Collection<String>) {
    for(s in strings) print("$s ")
    println()
}

fun main() {
    val stringList = listOf("one", "two", "one")
    printAll(stringList)

    val stringSet = setOf("one", "two", "three")
    printAll(stringSet)
}
```

### 10.2.2 创建集合

#### 10.2.2.1 list 列表

- ***创建一个 `List` ，一般就用 `listOf` 这个顶层函数***，它接受一些可变参数，返回一个 `List` 对象

- ***`List<T>` 以指定的顺序存储元素，并提供使用索引访问元素的方法***。索引从 `0`（第一个元素的索引）开始直到 `lastIndex`，即 `list.size - 1`

> 编译器知道 `listOf` 里面参数的类型，所以无需手动指定列表类型

```kt
fun main() {
    val numbers = listOf("one", "two", "three", "four")
    println("Number of elements: ${numbers.size}")
    println("Third element: ${numbers.get(2)}")
    println("Fourth element: ${numbers[3]}")
    println("Index of element \"two\" ${numbers.indexOf("two")}")
}
```

- ***`list` 允许空值和重复值***，因此在**判断两个列表相等的时候只要在索引相同的位置有值相等的元素就可以了**

```kt
data class Person(var name: String, var age: Int)

fun main() {
    val bob = Person("Bob", 31)
    val people = listOf(Person("Adam", 20), bob, bob)
    val people2 = listOf(Person("Adam", 20), Person("Bob", 31), bob)
    // Bob 这里存的是对对象的引用
    println(people == people2)
    bob.age = 32
    println(people == people2)
}
```

```kt
fun main() {
    val list: List<Int?> = listOf(1, null, 3, 4, null, 6)
    var nullList: List<Int>? = null
    // nullList = listOf(1, null, null) 是不行的
    // 注意 List<Int?> 和 List<Int>? 的区别
    nullList = listOf(1, 2, 3)
}
```

- 一个 `list` 在声明之后长度和元素就是固定了的无法改变，而一个 ***`mutableList` 可以添加、删除元素***

> 一个数组虽然声明后长度也不可变，但是可以修改元素的，一个 `list` 不仅是不可以改变长度，而且元素也不可变，而 `mutableList` 可以修改元素，也可以添加、删除元素

|`List`|`Array`|`MutalbeList`|
|-|-|-|
|长度不可变|长度不可变|长度可变|
|元素不可变|元素可变|元素可变|

```kt
fun main() {
    val names = mutableListOf("Alice", "Bob", "Charlie").apply {
        forEach { println("Name is $it") }
        println(size)
        println()
    }

    names.run {
        add("Dave")
        add("Eve")
        forEach { println("Name is $it") }
        println(size)
        println()
    }

    names.run {
        remove("Bob")
        removeAt(0)
        removeFirst()
        removeLast()
        forEach { println("Name is $it") }
        println(size)
    }
}
```

> 官方文档说 `ArrayList` 是 `MutableList` 的默认实现，估计是用 `ArrayList`  比 `LinkedList` 的人多（但是 `ArrayList` 增删麻烦，性能不好啊），注意到 ***Kotlin 没有原生的 `LinkedList`***

- Kotlin 虽然没有原生的 `LinkedList`，但是别忘了 Java 里面有一堆原生的数据结构，而且完全兼容，所以**如果要创建具体的数据类型只需导入后声明即可**

```kt
import java.util.LinkedList

fun main() {
    val linkedlist = LinkedList<Int>(listOf(1, 2, 3, 4, 5))
    // linkedlist 可以接受 Kotlin 里面的集合类型 Collection 
    linkedlist.add(6)
    linkedlist.addFirst(0)
    linkedlist.addLast(7)
    linkedlist.reverse()
    println(linkedlist.joinToString(prefix = "[", postfix = "]", separator = " -> "))
    // 估计是 Kotlin 为 LinkedList 做的扩展，Java 里是没有这个的
}
```

- 除了这些方式，还可以***使用 `buildList` 函数，该函数接受一个 `lambda` ，在 `lambda` 内可以把需要初始化的只读列表当作可变列表一样增删改，最后返回经过处理的 `List` 对象，注意是只读的***


```kt
import java.util.LinkedList

fun main() {
    val  names = buildList /*<String>*/ {
        add("Alice")
        add("Bob")
        add("Charlie")
        remove("Bob")
        removeFirst()
        addAll(listOf("Dave", "Eve"))
    }.apply {
        println(this)
    }
}
```

- 创建一个***空的 `list` 也可以用 `emptyList` 函数***，他返回的 `List` 对象的 `size` 为 `0`，也不能增删元素

> 注意他返回的这个 `List` 如果是不变的 `List`，如果你的变量也是 `val` 的，那么这个变量就是没用的

```kt
fun main() {
    var names = emptyList<String>()
    println(names.isEmpty())
    println(names.size)
    names = listOf("Alice", "Bob", "Charlie")
    println(names.isEmpty())
}
```

- ***多数情况下我们会直接使用 `listOf` ，然后参数为空，这样也是会返回空列表的***，或者 `mutalbeListOf` 这样结果可以 `add`

```kt
fun main() {
    val list = mutableListOf<Int>()
    println(list)
    println(list.isEmpty())

    list.apply {
        add(1)
        add(2)
        add(3)
    }
    
    println(list)
    println(list.isEmpty())
}
```

- ***`List` 有一个构造器***，允许你像声明数组一样初始化列表，***它接受列表的长度和一个 `lambda`***，在 `lambda` 内可以把需要初始化的元素逐个添加到列表中

- 同时，***列表也是可以使用 `..` 生成的迭代器初始化的，这个后面讲***

```kt

fun main() {
    val evens = List(5) { it * 2 }
    val evenNumbers = (1..100).filter { it % 2 == 0 }
    println(evens)
    println(evenNumbers)
}
```

- 列表的值也可以指向另一个列表，这个时候就需要注意源列表改动对引用列表产生的影响

- 如果***直接拿变量名引用，这样产生的结果类似浅拷贝***（shallow copy），即指向同一个对象，修改其中一个会影响另一个；而***使用 `toXXX()` 类似的方法产生的对象，结果是深拷贝***（deep copy）的，即指向不同对象，修改其中一个不会影响另一个

```kt
data class Person(var name: String)

fun main() {
    val alice = Person("Alice")
    val sourceList = mutableListOf(alice, Person("Bob"))
    val copyList = sourceList.toList()
    sourceList.add(Person("Charles"))
    alice.name = "Ace"
    println("First item's name is: ${sourceList[0].name} in source and ${copyList[0].name} in copy")
    println("List size is: ${sourceList.size} in source and ${copyList.size} in copy")
}
```

- 这样**许多引用都指向同一个实例的时候，每一个引用对实例的修改都会影响到其他引用，包括在函数里面也是**

- ***可以把一个可变列表的引用赋值给不可变列表的变量，这样可以收窄该引用变量的作用范围***，他**只能访问但不能修改实际上可变的元素**

```kt
fun main() {
    val ml = mutableListOf(1, 2, 3)
    val list: List<Int> = ml
    // list.add(4)

    // func(list)
    func(ml)
}

fun func(list: MutableList<Int>) {
    list.add(666)
    println(list)
}
```

- `list` 的***取值操作符 `get()` 可以使用 `[]` 来使用，也有防止越界的 `getOrNull` `getOrElse` 方法***

- 同理，**`set()` 方法也可以使用 `[]`**

```kt
fun main() {
    val list = listOf(1, 2, 3, 4, 5)
    println(list.get(3))
    println(list.getOrElse(6) { it })
    // list[6]
    println(list.getOrNull(5))
}
```

- ***`subList()` 返回列表中指定的索引范围的列表，对这个子列表的操作直接影响到源列表，反之亦然***

```kt
fun main() {
    val numbers = (0..10).toMutableList()
    println(numbers.subList(3, 6))
    numbers.subList(3, 6).clear()
    println(numbers)
    numbers.retainAll { it % 2 == 0 }
    // println(numbers.subList(3, 6))
}
```

- **`index` 线性查找**

```kt
fun main() {
    val nums = listOf(1, 2, 3, 4, 5)
    val numbers = listOf(1, 3, 123, 45, 6, 2, 3)

    // indexOf() lastIndexOf() 线性查找，找不到返回 -1
    println(nums.indexOf(3))
    println(numbers.lastIndexOf(3))
    println(nums.indexOf(6))

    // indexOfFirst() indexOfLast() 接受参数，返回第一个或最后一个匹配项的索引，找不到返回 -1
    println(nums.indexOfFirst { it % 2 == 0 })
    println(nums.indexOfLast { it % 2 == 0 })
    println(numbers.indexOfFirst { it > 100 })   
}
```

- ***`binarySearch()` 二分查找，速度优于线性查找，但是要求列表要有一定的顺序***

- ***如果找到，则返回元素的索引；如果找不到，则返回 `-(insertPosition - 1)`，其中 `insertPosition` 是新元素应该插入的位置***

```kt
fun main() {
    val list = mutableListOf('a', 'b', 'c', 'd', 'e')
    println(list.binarySearch('d'))

    list.remove('d')

    // -(insertion point - 1)
    val invertedInsertionPoint = list.binarySearch('d')
    val actualInsertionPoint = -(invertedInsertionPoint + 1)
    println(actualInsertionPoint)

    list.add(actualInsertionPoint, 'd')
    println(list)
}
```

#### 10.2.2.2 set 集

- ***`Set<T>` 存储唯一的元素***，顺序一般无所谓，***`setOf` 函数可以创建一个 `Set` 对象，它接受一些可变参数，返回一个 `Set` 对象***

- **`null` 元素也是唯一的**，***如果两个 `Set` 对象长度一样，并且每个元素对方也都有，那么认为这两个 `Set` 对象相等***

```kt
fun main() {
    val set = setOf(1, 2, 3, 4, 5)
    println(set.sum())
    println(set.average())
    println(set.max()) // or min()
    println(set.count())
    println(set)

    for (i in set.indices) { println(" Set Contains $i ? -> ${set.contains(i)}") }
}
```

```kt
fun main() {
    val set1 = setOf(1, 2, 3, 4, 5)
    val set2 = setOf(5, 4, 3, 2, 1)
    println(set1 == set2)
    // 无视顺序只看元素
}
```

- 同样，***集合也有自己的可变类 `MutableSet`，它就可以添加、删除元素，使用 `mutableSetOf` 来创建***

```kt
fun main() {
    val set1 = mutableSetOf(1, 2, 3, 4, 5)
    set1.add(6)
    set1.remove(2)
    println(set1)
}
```

- **也有自己的 `buildSet` 方法**

```kt
fun main() {
    val set = buildSet {
        add("apple")
        add("banana")
        add("orange")
    }.also {
        println(it)
    }
}
```

- `Set` 中的元素没有顺序，***判断一个元素是否在 `Set` 中，可以使用 `contains()` 方法，还可以用 `in` 中缀***

```kt
fun main() {
    println(setOf("one", "two", "three").contains("one"))
    println("one" in setOf("one", "two", "three"))
}
```

- ***`Set` 的默认实现是 `LinkedHashSet`，听名字也能知道他会保留元素的插入顺序***，因此像是 `first` `last` 这些本来对集合没用的操作，`Set` 都可以用，而且如预期实现

```kt
fun main() {
    val numbers = setOf(1, 2, 3, 4)
    val numbersBackwards = setOf(4, 3, 2, 1)


    println(numbers == numbers)
    println(numbers.first() == numbersBackwards.first())
    println(numbers.first() == numbersBackwards.last())
}
```

> 另一种 `HashSet` 使用依赖顺序的方法时不会向上面这样，但是好处是占用内存和时间复杂度都比 `LinkedHashSet` 低，同样 `HashSet` 使用的是 Java 里面的，可以发现在 JVM 的上的 Kotlin 真是用惯了 Java 的库

```kt
fun main() {
    val numbers = HashSet<Int>(4).apply { add(1); add(2); add(3); add(4) }
    val numbersBackwards = HashSet<Int>(4).apply { add(4); add(3); add(2); add(1) }


    println(numbers == numbers)
    println(numbers.first() == numbersBackwards.first())
    println(numbers.first() == numbersBackwards.last())
}
```

- 说到集，就要补充几个***跟集合概念有关的操作：交集、差集、并集***等等，放心比数学上的概念简单多了，***这些方法对集合有关的类都通用，但是在不同数据结构上的结果可能不一样***，需要注意下

```kt
fun main() {
    val set = setOf(1, 2, 3, 4, 5)
    val primeSet = setOf(2, 3, 5, 7, 11)

    println("加法：${set + primeSet}")
    // plus 的结果包括原始集合和第二个集合的元素
    println("减法：${set - primeSet}")
    // minus 返回第一个中的所有元素，但是第二个集合中的有的除外，如果第二个集合是一个单独元素，则移除其在在原始集合中的第一次出现
    // 如果是一个集合，那么移除其元素在原始集合中的所有出现
    println("交集：${set.intersect(primeSet)}")
    // 交集，返回两个集合中都有的元素
    println("并集：${set.union(primeSet)}")
    // 并集，返回两个集合中所有元素，注意因为是set，所以默认的加法跟并集的结果是一样的，但是如果是list，并集会去重，加法不会
    println("差集：${set.subtract(primeSet)}")
    // 差集，返回第一个集合中有，第二个集合中没有的元素，没错跟 minus 也就是减法是一样的
    println("补集：${primeSet.minus(set)}")
    // 补集，返回第一个集合中没有，第二个集合中有的元素
}
```

- ***想创建一个空集合，同样在使用 `setOf` 的时候不填参数就可以***

```kt
fun main() {
    val set = mutableSetOf<Int>()
    println(set)
    println(set.isEmpty())

    set.apply {
        add(1)
        add(2)
        add(3)
    }

    println(set)
    println(set.isEmpty())
}
```

#### 10.2.2.3 map 字典

> `Map<K, V>` 不是 `Collection` 接口的继承者，但是它也是 Kotlin 的一种集合类型

- ***`Map` 存储键值对（Key Value Pairs），键是唯一的，但是不同的键可以与相同的值配对***，`Map` 接口提供特定的函数进行通过键访问值、搜索键和值等操作

- ***创建一个字典，使用 `mapOf` 函数，它接受一些键值对（其实是我们见过的 `Pair` 数据类），返回一个 `Map` 对象，还有对应的 `mutableMapOf` 函数返回可变字典***

```kt
fun main() {
    val map = mapOf("Alice" to 25, "Bob" to 30, "Charlie" to 35)
    println(map)
    for ((name, age) in map) {
        println("\t$name is $age years old")
    }

    for (i in 0..map.size - 1) {
        println("\t\t${map.keys.elementAt(i)} is ${map.values.elementAt(i)} years old")
    }

    for (i in map) {
       println("\t\t\t$i")
    }
}
```

- 这个 **`to` 不是一个关键字，他只是二元元组里的一个中缀方法**用于快速创建元组，而 `map` 的初始化方法接受的就是一堆元组的可变参数

```kt
fun main() {
    val map = mapOf(Pair("apple", 1), Pair("banana", 2), Pair("orange", 3))
    val map1 = mapOf("apple" to 1, "banana" to 2, "orange" to 3)

    // 二者效果相等
}
```

- 因为二元元组是一个数据类，所以**在需要性能的地方最好少去使用 `to` 的方式初始化字典**

```kt
fun main() {
    val map = mutableMapOf<String, String>().apply {
        // apply 返回对象本身
        put("apple", "$1.00")
        // map 有 put 而不是 add 方法
        put("banana", "$0.50")
        put("orange", "$0.75")
        remove("banana")
        // 移除掉键的它对应的值
        put("pear", "$2.00")
        this["grape"] = "$3.00" // 没有键则添加
        this["apple"] = "$1.50" // 已有键则更新
        println(this)
    }
}
```

- ***字典的 `equals` 方法只看键对应的值相等与否***，顺序无所谓

```kt
fun main() {
    val numbersMap = mapOf("key1" to 1, "key2" to 2, "key3" to 3, "key4" to 1)    
    val anotherMap = mapOf("key2" to 2, "key1" to 1, "key4" to 1, "key3" to 3)

    println("The maps are equal: ${numbersMap == anotherMap}")
}
```

- ***`mutableMap` 是一个允许读写操作的字典***

```kt
fun main() {
    val numbersMap = mutableMapOf("one" to 1, "two" to 2)
    numbersMap.put("three", 3)
    numbersMap["one"] = 11
    // map 的 set 方法也支持 [key] 的索引方式

    println(numbersMap)
}
```

- Kotlin 里的**字典默认实现是 `LinkedHashMap` ，可以保留插入的顺序**，如果**为了追求性能可以自己指定 `HashMap` 用作实现**

> 具体 `LinkedHashMap` 和 `HashMap` 的区别，可以看网上的资料，这里不了解就不介绍了

```kt
fun main() {
    val linkMap = mapOf("Kotlin" to "https://kotlinlang.org", "Java" to "https://www.java.com")
    val hashMap = HashMap<String, String>(linkMap)

    println("hashMap: $hashMap")
    println("linkMap: $linkMap")
}
```

### 10.2.3 集合的常见操作

> 这里不会对 Kotlin 里面集合的每一个操作进行讲解，费力不讨好，直接看官方文档就好了，很简单，这里列出常用方法的名称方便索引

- [集合转换操作](https://book.kotlincn.net/text/collection-transformations.html)

> `map()` `filter()` `associate` `flatten()` `joinTo`

```kt
fun main() {
    val list = listOf("apple", "banana", "orange", "grape", "pear")
    val map = mapOf("Nikon Z6" to 1200, "Canon EOS 5D" to 1800, "Sony Alpha 6800" to 2000)

    // map() 方法接受一个 lambda 表达式作为参数，并将每个元素应用到 lambda 表达式中，返回一个新的集合，顺序不变
    // Indexed 函数可以获取元素的索引，如果要返回的元素可以为空，请使用对应的 NotNull 方法
    println(list.map { "$it is a fruit" })
    println(list.mapIndexed { index, fruit -> "$index: $fruit is a fruit" })
    println(list.mapNotNull { if (it.length > 5) it else null }.apply { println(this.size) })
    // 注意这个 NotNull 方法的使用，他返回的并不是 List<String?> 而是 List<String>，略过了 null 元素，下面同理
    println(list.mapIndexedNotNull { index, fruit -> if (fruit.length > 4) "$index: $fruit" else null })

    // 如果操作的对象是 map，可以选择 mapKeys() 和 mapValues() 方法，前者对键进行操作保留值，后者对值进行操作保留键
    println(map.mapKeys { it.key.uppercase() })
    println(map.mapValues { it.value * 2 })
    println(map
        .mapKeys { it.key.lowercase() }
        .mapValues { it.value * 3 }
        .map { "${it.key} costs $ ${it.value}" }
    )
    println()

    // filter() 方法接受一个 lambda 表达式作为参数，并将每个元素应用到 lambda 表达式中，返回一个新的集合，顺序不变
    // 只有满足 lambda 表达式的元素才会被保留，不满足的元素会被过滤掉
    println(list.filter { it.length > 5 })
    println(list.filterIndexed { index, fruit -> index % 2 == 0 })
    println(list.filterNot { it.length > 5 })
    println()

    val dogs = listOf("Rufus", "Max", "Buddy")
    val cats = listOf("Fluffy", "Whiskers")
    // zip() 方法接受两个集合作为参数，返回一个包含两个 Pair 的 list，每一个 Pair 包含两个元素，第一个元素来自第一个集合，第二个元素来自第二个集合
    // 如果两个集合的元素个数不一致，则只会返回最短集合的元素
    println(dogs zip cats)
    // 还可以指定一个 lambda 表达式来自定义结果集
    println(dogs.zip(cats) { d, c -> "$d is a good dog, $c is a good cat" })
    println(dogs.zip(cats, transform = { d, c -> d to c })) // 等于默认
    println()

    // 同理，如果有一个只包含 Pair 的 list，还可以使用 unzip() 方法将其解压为两个集合，第一个集合包含所有 Pair 的第一个元素，第二个集合包含所有 Pair 的第二个元素
    val pairs = listOf("apple" to 10, "banana" to 20, "orange" to 30)
    val fruits = pairs.unzip()
    println(fruits)
    println()

    // associate() 系列方法可以把一个集合与另外的元素关联从而返回一个字典
    // associateWith() 方法接受一个 lambda 表达式作为参数，并将每个元素应用到 lambda 表达式中，返回一个字典，键是元素，值是 lambda 表达式的结果
    println(list.associateWith { it.length })
    // associateBy() 方法可以指定键的生成和值的生成方式
    println(list.associateBy(keySelector = { it.first() }, valueTransform = { it.length }))
    // associate() 方法可以同时指定键和值的生成方式，lambda 表达式需要返回一个 Pair，里面就是键和值
    println(list.associate { it.first().uppercase() to it.length + 10 })
    println()

    // flatten() 方法可以将一个包含集合的集合中的元素展开为一个单独的元素列表
    println(listOf(listOf(1, 2, 3), listOf(4, 5, 6)).flatten())
    // flatMap() 方法可以将一个集合中的元素应用到一个 lambda 表达式，然后将结果展开为一个单独的元素列表，注意 lambda 表达式拿到的是集合而不是集合中的元素，并且必须返回一个可迭代的对象
    println(list.flatMap { it.toList() })
    println(listOf(listOf("apple", "banana"),
        listOf("orange", "grape"),
        listOf(1, 2, 3)
    ).flatMap { it.map { it.toString() } })
    println()

    // joinToString() 方法可以方便的格式化集合为字符串
    println(list.joinToString()) // 默认
    println(list.joinToString(prefix = "(", postfix = ")", separator = " -> ", transform = { it.uppercase() })) // 自定义
    // joinTo() 方法可以将集合中的元素以指定的方式连接到一个 StringBuilder 中
    val sb = StringBuilder("This is a list: ")
    list.joinTo(sb, separator = " | ", prefix = "(", postfix = ")")
    println(sb.toString())
    println()
}
```

- [过滤集合](https://book.kotlincn.net/text/collection-filtering.html)

> `filter()` `partition()` `any()` `none()` `all()`

```kt
fun main() {
    val list = listOf(1, 2, 3, 4, 5)
    val map = mapOf("1th" to 1, "2nd" to 2, "3rd" to 3, "4th" to 4, "5th" to 5)
    val anyList = listOf(1, "2", 3.0, '4', null)
    val emptySet = setOf<Int>()

    // filter() 函数用于过滤列表中的元素，返回一个新的列表，参数为一个 lambda 表达式，该表达式接收一个元素作为参数，返回一个布尔值，表示是否保留该元素
    println(list.filter { it % 2 == 0 })
    // list 和 set 都返回 list，map 过滤后返回 map
    println(map.filter { (key, value) /*Pair 解构*/ -> value % 2 == 0 && key.endsWith("th") })
    // filterIndexed() 还可以拿到元素的索引
    println(list.filterIndexed { index, value -> (index + 1) % 2 == 0 && value % 2 == 0 })
    // filterNot() 正好与 filter() 相反，返回一个新的列表，保留原列表中不满足 lambda 表达式的元素
    println(list.filterNot { it % 2 == 0 })
    // filterNotNull() 过滤掉 null 元素
    println(anyList.filterNotNull())
    // filterIsInstance() 可以拿到指定类型的元素集合，从而可以针对特定类型使用它的特点方法
    println(anyList.filterIsInstance<String>().forEach { print("${it.uppercase()} and ") })
    println()

    // partition() 函数可以将列表分成两个列表，第一个列表是满足 lambda 表达式的元素，第二个列表是不满足的元素
    val (evens, odds) = list.partition { it % 2 == 0 }
    println("evens = $evens, odds = $odds")
    println()

    // any() none() all() 函数用于简单判断，any() 有一个元素满足 lambda 表达式，返回 true，否则返回 false；
    // none() 所有元素都不满足 lambda 表达式，返回 true，否则返回 false
    // all() 所有元素都满足 lambda 表达式，返回 true，否则返回 false。
    println(list.any { it % 2 == 0 })
    println(list.none { it % 2 == 0 })
    println(list.all { it % 2 == 0 })
    // 这些方法不带参数使用的话就简单的判断列表是否为空或非空，如果为空 any() 返回 false，none() 返回 true
    println(emptySet.isEmpty())
    println(emptySet.none())
    println(emptySet.any())
    println()   
}
```

- [分组](https://book.kotlincn.net/text/collection-grouping.html)

> `group()` 和它的衍生方法

```kt
fun main() {
    val list = listOf(1, 2, 3, 4, 5)

    // groupBy() 方法用于将集合按照给定的条件分组，返回字典，其中键是分组的条件（lambda表达式的返回值），值是分组后的元素
    println(list.groupBy { if (it % 2 == 0) "even" else "odd" })
    // 注意这里 keySelector 和 valueTransform 两个中的 it 都是指集合中的元素，不是索引
    println(list.groupBy(keySelector = { it % 2 }, valueTransform = { "$it : ${it * 2}" }))

    // groupingBy() 返回的是一个 Grouping 类型的实例，可以对它在调用方法，比如 eachCount() 方法，用于统计每个分组的元素数量
    println(list.groupingBy { it % 2 }.eachCount())
}
```

- [取集合的一部分](https://book.kotlincn.net/text/collection-parts.html)

> `slice()` `take()` `drop()` `chuncked()` `windowed()`

```kt
fun main() {
    val list = listOf("1th", "2nd", "3rd", "4th", "5th")

    // slice() 函数接受一个区间，返回索引在区间内对应的元素
    println(list.slice(1..3))

    // take() takeLast() 函数接受一个整数，返回从开头或结尾取指定数量的元素
    println(list.take(3))
    println(list.takeLast(3))

    // drop() dropLast() 函数接受一个整数，返回从开头或结尾去掉指定数量的元素
    println(list.drop(3))
    println(list.dropLast(3))
    println(list) // 源列表不变
    // 注意当 take 和 drop 都取出了相同数量的元素时，结果将会是整个列表
    println(list.take(10))
    println()

    // takeWhile() 函数接受一个 lambda 表达式，返回从开头开始，直到 lambda 表达式返回 true 的元素，其他的 takeLastWhile() dropWhile() dropLastWhile() 函数类似
    println(list.takeWhile { it.endsWith("th") })
    println(list.takeLastWhile { it.endsWith("th") })
    println(list.dropWhile { it.endsWith("th") })
    println(list.dropLastWhile { it.endsWith("th") })
    println()

    // chunked() 函数接受一个整数，返回一个二维列表，里列表的大小为指定的整数，列表的元素是源列表的连续片段
    println((1..10).toList().chunked(3))
    // chunked() 函数还可以接受一个 lambda 表达式，对每个片段进行处理
    println((1..10).toList().chunked(3) { it.sum() })
    println()

    // windowed() 函数用于把集合分割成指定大小的窗口，返回一个二维列表，这个窗口的大小，每次移动的步长，包不包含不完整的窗口都可以指定，他返回的二位列表就是一个个窗口展示出的元素
    println(list.windowed(3))
    println(list.windowed(size = 3, step = 2))
    println(list.windowed(size = 2, step = 1, partialWindows = true))
    println()
}
```

- [取单个元素](https://book.kotlincn.net/text/collection-elements.html)

> `elementAt()` `first()` `last()` `random()` `contains()` `isEmpty()`

```kt
fun main() {
    val list = listOf("1th", "2nd", "3rd", "4th", "5th")

    // elementAt() 函数用于取值，不过对于 list 来说还是使用 get() 函数更方便
    println(list.elementAt(2)) // == list[2]

    // elementAtOrNull() 函数用于取值，如果越界则返回 null
    // elementAtOrElse() 函数用于取值，如果越界则返回 lambda 函数的返回值
    println(list.elementAtOrNull(10))
    println(list.elementAtOrElse(10) { "out of bounds" })

    // first() last() 函数用于取第一个和最后一个元素
    println(list.first())
    println(list.last())
    // first() last() 函数也可以传入 lambda 函数作为参数，用于筛选第一个符合要求的元素
    println(list.first { it.endsWith("th") })
    println(list.last { it.endsWith("th") })
    // 注意，如果没有符合要求的元素，first() last() 函数会抛出 NoSuchElementException 异常，可以使用 firstOrNull() lastOrNull() 函数
    println(list.firstOrNull { it.endsWith("th") })
    println(list.lastOrNull { it.endsWith("6th") })
    // Kotlin 还贴心的准备了 find() findLast() 用于简化 firstOrNull() lastOrNull()，二者功能完全相同
    println(list.find { it.endsWith("th") })
    println(list.findLast { it.endsWith("6th") })

    // random() 函数用于随机取一个元素
    println(list.random())

    // contains() 函数用于判断元素是否存在于列表中，一般用于 set 集合
    println(list.contains("2nd"))
    println(list.contains("6th"))
    println()

    // firstNotNullOf() 函数遍历集合，返回 lambda 返回的第一个非 null 值，如果遍历完仍没有找到非 null 值，则抛出 NoSuchElementException 异常
    println(listOf(null, "1", 23, "2nd", null).firstNotNullOf { it.toString().takeIf { it == "1" } })
    // firstNotNullOfOrNull() 不会报错取而代之的是返回 null
    println(listOf(null, '1', 23, "2nd", null).firstNotNullOfOrNull { it.takeIf { it is String } })
    // 因为要返回 null 才会调用，这也是为什么一般与 takeIf() 一起使用
}
```

- [排序](https://book.kotlincn.net/text/collection-ordering.html)

- [聚合操作](https://book.kotlincn.net/text/collection-aggregate.html)

> `min()` `max()` `sum()` `average()` `count()` `reduce()` `fold()`

```kt
fun main() {
    val numbers = listOf(6, 42, 10, 4)

    // count 返回集合中元素的数量，对 list 来说类似 size
    // maxOrNull 返回集合中最大的元素，如果集合为空，则返回 null
    // minOrNull 返回集合中最小的元素，如果集合为空，则返回 null
    // average 返回集合中元素的平均值
    // sum 返回集合中元素的总和
    println("Count: ${numbers.count()}")
    println("Max: ${numbers.maxOrNull()}")
    println("Min: ${numbers.minOrNull()}")
    println("Average: ${numbers.average()}")
    println("Sum: ${numbers.sum()}")

    // sumOf()
    println("Sum of squares 1 to 10: ${(1..10).sumOf { it * it }}") // 每一个数的平方的和，sumOf 允许你在求和之前对每一个元素再做一次操作

    // maxBy() maxByOrNull() maxWithOrNull() minBy() minByOrNull() minWithOrNull() 看下面
    println(numbers.maxBy { it % 2 == 0 })
    println(numbers.maxWithOrNull(compareBy { it % 2 }))

    // fold() reduce() 都是累积对集合操作，一个参数是之前的累加值，另一个是当前索引
    // 唯一不同点是 fold 接受一个初始值并当作第一次的累加值，而 reduce 把第一第二个元素作为参数
    println(numbers.fold(0) { sum, i -> sum + i })
    println(numbers.reduce { sum, i -> println("$sum and $i") ; sum + i })
    println(numbers.reduce { sum, i -> println("$sum and $i") ; sum + i * 2})
    println()

    // foldRight() reduceRight() 类似 fold() reduce() ，但是从右边开始累积，注意参数的顺序也变了
    println(numbers.foldRight(0) { i, sum -> sum + i })
    println(numbers.reduceRight { i, sum -> println("$i and $sum") ; sum + i })
    println(numbers.reduceRight { i, sum -> println("$i and $sum") ; sum + i * 2})
    println()

    // foldIndexed() reduceIndexed() 类似 fold() reduce() ，但是可以访问索引，同理 foldRight() reduceRight()
    println(numbers.foldIndexed(0) { index, sum, i -> sum + index + i })
    println(numbers.reduceIndexed { index, sum, i -> println("$index and $sum and $i") ; sum + index + i })
    println(numbers.reduceRightIndexed { index, i, sum -> println("$index and $i and $sum") ; sum + index + i })
    println()

    // 最后，所有的这些都会在集合为空的时候报错，他们都有对应的OrNull() 版本，如果集合为空，则返回 null
}
```

- [集合写操作](https://book.kotlincn.net/text/collection-write.html)

> `add()` `remove()` `addAll()` `removeAll()` `clear()`

```kt
fun main() {
    val list = mutableListOf(1, 2, 3, 4, 5)
    println(list.apply { add(6) })
    println(list.apply { remove(2) })
    println(list.apply { removeAll { it % 2 == 0 } })
    println(list.apply { clear() })
    println(list.apply { this += 1 })
    println(list.apply { addAll(listOf(7, 8, 9, 2, 4)) })
    println(list.apply { retainAll(listOf(1, 3, 5)) })
    println(list.apply { this -= 1 })
}
```

> 在写这一章的时候，发现了很有意思的一件事

```kt
fun main(args: Array<String>) {
    val greeting = "Hello, world!".also {
        if (it is String) { println("it's a string") } else { println("it's not a string") }
    }

    // it is String 正好像是一句话了
}
```

### 10.2.4 队列

- Kotlin 推荐使用自己的 ***`ArrayDeque<T>` ，这是一个双端队列***，允许从开头或者末尾添加元素，所以也可以充当队列或是栈来使用，实际上是一个可调整大小的数组

> 当然使用 Java 的集合框架也可以

```kt
fun main() {
    val deque = ArrayDeque(listOf(1, 2, 3))

    deque.addFirst(0)
    deque.addLast(4)
    println(deque) // [0, 1, 2, 3, 4]

    println(deque.first()) // 0
    println(deque.last()) // 4

    deque.removeFirst()
    deque.removeLast()
    println(deque) // [1, 2, 3]
}
```

## 10.3 排序

- 对集合来说，排序（sorting）是很重要的操作，我们在上面曾经讲过 **`compareTo()` 这个操作符重载方法，利用它可以对我们自定义的类使用 `>` `<` 之类的比较操作符**

- Kotlin 里**一般的类型 `Int` `String` 一类都继承自 `Comparable` 类，并且自己实现了 `compareTo()` 方法**，所以可以直接进行比较，比如 $1 > 0$ $-2 > -3.5F$ ，当然***自己的类也可以继承自 `Comparable`***

```kt
fun main() {
    println(1 > 7)
    println(-1.2 < -3.4f)
    println("Hello, world!" > "Kotlin")
    println("Hello, world!" > "Hello, Kotlin!")
    // 字符默认按照字母顺序排序
}
```

- ***`compareTo()` 必须接受同类型的单参数并返回一个整数，正数自己大负数说明没有人家大，`0` 说明一样大***

```kt
fun main() {
    println(Version(1, 2) < Version(1, 3))
    println(Version(1, 4) < Version(1, 3))
    println(Ver(1, 2) < Ver(1, 3))
    println(Ver(1, 4) < Ver(1, 3))
}

data class Version(val major: Int, val minor: Int) {

    operator fun compareTo(other: Version): Int = when {
        this.major!= other.major -> major - other.major
        this.minor!= other.minor -> minor - other.minor
        else -> 0
    }

    // 使用操作符重载的方式

}

class Ver(val major: Int, val minor: Int) : Comparable<Ver> {

    override fun compareTo(other: Ver) = when {
        this.major != other.major -> this.major - other.major
        this.minor != other.minor -> this.minor - other.minor
        else -> 0
    }

    // 使用继承并重写 compareTo() 方法的方式
}
```

- ***使用方法 `sorted()` 可以集合中对继承自 `Comparable` 的元素进行排序***，返回一个新的排序后的列表，***默认是升序排序***

- ***`sortedDescending()` 是降序排序***

```kt
fun main() {
    println(listOf(1, 4, 7, 8, 5).sorted())
    println(listOf(Version(1, 2), Version(1, 3), Version(1, 1)).sorted())

    println(listOf(1, 4, 7, 8, 5).sortedDescending())
    println(listOf(Version(1, 2), Version(1, 3), Version(1, 1)).sortedDescending())
}


data class Version(val major: Int, val minor: Int) : Comparable<Version> {

    override fun compareTo(other: Version) = when {
        this.major != other.major -> this.major - other.major
        this.minor != other.minor -> this.minor - other.minor
        else -> 0
    }

}
```

- ***`shuffled()` 方法可以对集合进行随机排序，返回一个新的随机排序后的列表***

- ***`reversed()` 方法可以对集合进行反转，返回一个新的反转后的列表***。还有一个 ***`asReversed()` 方法，他的返回是源列表的反向引用，也就是索引方式是倒着的，但是仍然是源列表的引用，你的更改会影响到源列表***

```kt
// list 不可变

fun main() {
    val list = listOf(1, 2, 3, 4, 5)
    list.run {
        println(this.shuffled())

        println(this.sorted())

        println(this.reversed())
    }

    println(list)
}
```

- 对于 `mutableList`，还有 `shuffle()` `reverse` `sort()` 这类不是过去式的单词，他们代表这会改变原集合，而不是返回一个新的集合

- `asReversed()` 也能改变原集合了

```kt
fun main() {
    val list = mutableListOf(1, 2, 3, 4, 5)

    list.shuffle()
    println(list)

    list.sort()
    println(list)

    val reverseList = list.asReversed()
    println("reverseList: $reverseList")
    println("list: $list")

    reverseList.reverse()
    println("reverseList: $reverseList")
    println("list: $list")

    reverseList[0] = 100
    println("reverseList: $reverseList")
    println("list: $list")

    reverseList.fill(0)
    println("reverseList: $reverseList")
    println("list: $list")

    reverseList.clear()
    println("reverseList: $reverseList")
    println("list: $list")
}
```

- 既然说到了随机，顺带讲一下 Kotlin **自带的 `Random` 类，可以方便的生成伪随机数**，各种类型都有

> 导入 `kotlin.random.Random` 即可，这个包下就这一个类

```kt
import kotlin.random.Random

fun main() {
    val randomValues = List(10) { Random.nextInt(0, 100) }
    println(randomValues)

    val nextValues = List(10) { Random.nextInt(0, 100) }
    println(nextValues)
    println("randomValues != nextValues is ${randomValues != nextValues}")
}
```

- 要想***自定义排序，可以使用 `sortedBy()` 和 `sortedByDescending()` 方法，传入一个 `lambda` 接受集合里的每一个元素，然后根据这个 `lambda` 的返回值进行自然排序***（也就是返回 `Int` 则按照默认 `Int` 排序，返回 `String` 则按照字母顺序排序）

```kt
fun main() {
    println(listOf("one", "two", "three", "four", "five").sortedBy { it.length })
    println(listOf("one", "two", "three", "four", "five").sortedByDescending { it.last() })
}
```

- 如果自己***对自定义要求程度高，可以使用 `sortedWith()` 方法，该方法需要一个 `Comparator` 对象用来比较***

- 前面我们没讲过，***`Comparator` 其实是一个 `fun interface` ，也就是单参数方法，它的唯一方法 `compare()` 接受两个参数，返回一个 `Int` 值，正数自己大负数说明没有人家大，`0` 说明一样大***

```kt
fun main() {
    println(listOf("one", "two", "three", "four", "five")
    .sortedWith(Comparator { a, b ->
        a.length - b.length 
    }))

    // 使用 Kotlin 便捷 SAM 实现写法
}
```

- ***使用 `compareBy()` 就可以快速生成 `Comparator` 对象***

```kt
fun main() {
    println(listOf("one", "two", "three", "four", "five").sortedWith(compareBy { it.length }))

    // 等同于上文
}
```

- ***`then` 方法还可以对排序后的列表再次排序，同样接受一个 `Comparator` 对象，返回一个新的排序后的列表***，**`then` 是中缀形式的，`thenBy()` 无需再传入 `Comparator` 对象**

```kt
fun main() {
    val list = listOf("a", "b", "c", "aa", "bb", "ab", "ba")

    println(list.sortedWith(compareBy { it.length }))
    println(list.sortedWith(compareBy<String> { it.length } then compareBy { it }))
    println(list.sortedWith(compareBy<String> { it.length }.thenBy { it }))
}
```

## 10.4 区间

- Kotlin 里的***区间一般是使用 `rangeTo()` `rangeUntil()` 这两个中缀方法创建的，当然更常见的是使用 `..` `..<` 这两个操作符***

- ***Kotlin 里面有 `CharRange` `IntRange` `LongRange` 这三个区间类***，位于 `kotlin.ranges` 包下，默认会被导入

```kt
fun main() {
    val intRange = 1..10 // 1, 2, 3 ... 10
    val charRange = 'a'..<'z' // 'a', 'b', 'c' ... 'y'

    for (i in intRange) println(i)
    for (c in charRange step 2) println(c)
}
```

- 这个 **`Range` 还包含一些工具方法**

```kt
fun main() {
    println(('a'..'g').contains('C'))
    println(('A'..'G').contains('C'))
    println('c' in ('a'..'g'))
    // in 除了泛型、for、现在还有了一个用途
    println((0..-1).isEmpty())
}
```

```kt
fun main() {
    println(charKind('a'))
    println(charKind('A'))
    println(charKind('0'))
}

fun charKind(c: Char): String = when (c) {
    in 'a'..'z' -> "lowercase"
    in 'A'..'Z' -> "uppercase"
    in '0'..'9' -> "digit"
    else -> "other character"
}
```

- ***`in` 甚至能判断字符串区间***，不过当然字符串区间不存在，**他会把 `"a" in "abc".."xyz"` 看作是 `"a" >= "abc" && "a" <= "xyz"` 之类的关系**

```kt
fun main() {
    println("kotli" in "java".."scala")
    println("bash" in "cpp".."rust")
}
```

> Kotlin 还有一个数列，个人觉得没用，[官方文档](https://book.kotlincn.net/text/ranges.html)有介绍，自己看吧

## 10.6 迭代器

> 如果要遍历元素，最通用的是使用迭代器（iterator），他会逐个返回集合里的元素，而无需暴露底层结构

- ***在一个实现了 `Iterable<T>` 的继承者（`List` `Set`）上，可以调用 `iterator()` 方法得到一个迭代器对象，这个对象首先指向头指针，可以用 `hasNext()` `next()` 方法来遍历元素***

> `Map` 也有 `iterator()` 方法，只不过它不继承自 `Iterable`，并且是扩展方法的方式

```kt
fun main() {
    val numbers = listOf("one", "two", "three", "four")
    val numbersIterator = numbers.iterator()
    while (numbersIterator.hasNext()) {
        println(numbersIterator.next())
    }
}
```

> **一但迭代器走到了末尾，那么它就会被作废**，也无法再拿到元素和索引

- 当然，***最常用的 `for` 循环在遍历时会隐式的调用集合的迭代器***，所以一般迭代器用的很少

> `in` 在循环外面表示判断区间，在循环里面表示循环变量

```kt
fun main() {

    val map = mapOf("apple" to 1, "banana" to 2, "orange" to 3)

    for ((key, value) in map) {
        println("$key -> $value")
    }
}
```

- 还有我们一直在用的 ***`forEach`，轮流拿到元素***

```kt
fun main() {

    val map = mapOf("apple" to 1, "banana" to 2, "orange" to 3)

    map.forEach { key, value ->
        println("$key -> $value")
    }
}
```

- ***`List` 有一个特有的 `listIterator()` 方法，它返回一个 `ListIterator` 对象，可以双向遍历***

> 这样就可以无限迭代下去没有抵达最后的限制

```kt
fun main() {
    val numbers = listOf("one", "two", "three", "four")
    val listIterator = numbers.listIterator()

    while (listIterator.hasNext()) listIterator.next()
    println("Iterating backwards:")
    while (listIterator.hasPrevious()) {
        print("Index: ${listIterator.previousIndex()}")
        println(", value: ${listIterator.previous()}")
    }

    println("Iterating forwards:")
    while (listIterator.hasNext()) {
        print("Index: ${listIterator.nextIndex()}")
        println(", value: ${listIterator.next()}")
    }

    // 可以无限下去
}
```

- 还有 ***`MutableList` 为 `listIterator()` 方法提供了修改元素的能力***，比如 `set()` `add()` `remove()` 等方法

```kt
fun main() {
    val list = mutableListOf("one", "two", "three", "four", "five")
    val listIterator = list.listIterator()

    println(listIterator)
    while (listIterator.hasNext()) {
        print("${listIterator.next()} ")
        if (listIterator.nextIndex() % 2 == 0) {
            listIterator.remove()
            // 知道为什么除了 one 以外的元素都被移除了，是因为 nextIndex() 方法是动态的原来的列表在 remove 之后的索引也是会变的，一直在 2 的位置移除
        }
    }

    println()
    println(list)

    listIterator.apply {
        add("six")
        previous()
        add("seven")
        previous()
        // 注意下反向迭代时候 add 是在哪里加入
    }

    println(list)

    listIterator.set("eight")
    // set 是把当前指向的元素替换掉
    println(list)
}
```

## 10.7 序列

> 我们在前面从介绍作用于函数开始，就一直在使用链式调用，写起来逻辑清晰直观，但是**链式调用总是会创建出一堆使用完后就被丢弃的中间对象**，如果调用很多的话或许是个问题

> 说实话作用域函数不就是为了解决临时变量过多的吗？

- Kotlin 有另一种类型，***序列（sequence），它是惰性的，只有在需要的时候才会生成元素，而且可以无限迭代下去，相比迭代器的一个个链式产生的中间对象，序列会对每个元素逐步执行所有操作后再遍历下一个***

- ***创建一个序列，可以使用顶层函数 `sequenceOf()`***，就像是 `listOf()` 一样

```kt
fun main() {
    val sq = sequenceOf(1, 2, 3, 4, 5)
    println(sq) // 拿不到元素，后面就知道了
    println(sq.sum())
}
```

- 或者是 **`asSequence()` 把现有的集合转为序列**

```kt
fun main() {
    val sq1 = listOf(1, 2, 3, 4, 5).asSequence()
    val sq2 = setOf(1, 2, 3, 4, 5).asSequence()
    val sq3 = mapOf(1 to "one", 2 to "two", 3 to "three", 4 to "four", 5 to "five").asSequence()

    println(sq1.toList())
    println(sq2.toList())
    println(sq3.toList())
}
```

- 使用 `generateSequence()` 函数，提供第一个元素，使用 `lambda` 里的元素当作下一个元素，一直生成下去，直到 `lambda` 返回 `null` 为止

> 如果不返回 `null` ，那么这是一个无限序列，可以无限迭代下去，在使用的时候才会报错

```kt
fun main() {
    val sq = generateSequence(1) {
        if (it == 100) null else it + 1
    }

    val infiniteSq = generateSequence(0) {
        it + 2
    }

    println(sq.sum())
    println(infiniteSq.sum())
    // 到也不是报错，但是会无响应
}
```

- ***`sequence()` 函数可让我们像是使用 `buildList()` 类似的方式初始化序列，在他的里面使用 `yield()` 用于添加单个元素，`yieldAll()` 用于添加多个元素***

> **`yieldAll()` 也可以添加无限的序列，只不过这样的元素必须在 `lambda` 的最后一个操作**，之后的操作都不会执行

```kt
fun main() {
    val oddNumbers = sequence {
        yield(1)
        yieldAll(listOf(3, 5))
        // yieldAll 可以接受其他集合类型或对象
        yieldAll(generateSequence(7) { it + 2 })
    }
    println(oddNumbers.take(5).toList())
}
```

- 序列的操作分为两种：
    - ***返回一个序列，这叫做中间操作或无状态操作***，因为它不需要具体的状态，比如 `filter()` `map()` ，或者是接受少量参数的 `take()` `drop()`，***中间操作永远是惰性的***，如果有很多中间操作但是没有末端操作的话操作内是访问不到具体的元素的

    - ***返回另一个结果，这叫末端操作或有状态操作***，需要具体状态（通常与元素数量成正比），***会触发所有的惰性操作（中间操作）***，比如 `toList()` `sum()` ，***这些操作会遍历序列并且返回一个需要累加（上一个元素值）的结果***

```kt
fun main() {
    val sq = sequenceOf(1, 2, 3, 4, 5)
    // val sq = listOf(1, 2, 3, 4, 5) 自己试一试列表会发生什么
    sq.filter { 
        println("Filtered: $it")
        it % 2 == 0
    }.map { 
        println("Squared: $it")
        it * it
    }.sorted()
}
```

> 那这么多的方法，我怎么才知道哪个是终端的哪个是中间的，看[官方文档](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.sequences/-sequence/)

- **所有的中间操作执行的步骤都会被保留起来，知道终端操作加入会对每一个元素一次性执行完毕中间操作，这就是惰性的意思**

- 下面来看一个经典的例子：

```kt
fun main() {    
    val words = "The quick brown fox jumps over the lazy dog".split(" ")

    val lengthsList = words.filter { println("filter: $it"); it.length > 3 }
        .map { println("length: ${it.length}"); it.length }
        .take(4)

    val lengthSequence = words.asSequence()
        .filter { println("filter: $it"); it.length > 3 }
        .map { println("length: ${it.length}"); it.length }
        .take(4)

    println("Lengths of first 4 words longer than 3 chars:")
    println(lengthsList)

    println("Lengths of first 4 words longer than 3 chars (sequence):")
    println(lengthSequence.toList())
    // 这里才是末端操作
}
```

> 集合的流程：

![](https://book.kotlincn.net/images/list-processing.png)

> 序列的流程：

![](https://book.kotlincn.net/images/sequence-processing.png)

- 最后引用官网的一句话：**序列可避免生成中间步骤的结果，从而提高了整个集合处理链的性能。但是，序列的惰性性质增加了一些开销，这些开销在处理较小的集合或进行更简单的计算时可能很重要。因此，应该同时考虑使用 `Sequence` 与 `Iterable`， 并确定在哪种情况更适合**

> Kotlin 里的序列才是真 `Stream API`，面对数量大且操作多的集合时候明显序列才是更好的选择

## 10.8 命令行参数

> 说了那么多，终于讲到了

- 回过头来看 Java 的 `Hello World`，我们会注意到 `main` 函数有一个参数 `String[] args`，这就是***命令行参数，我们可以用它来接收外部传入的参数***

> 也就是你使用控制台的时候输入的东西，比如 `java HelloWorld arg1 arg2` 中的 `arg1` `arg2` 就是命令行参数

- Kotlin 也有类似的机制，不过它是通过 ***`Array<String>` 类型的 `args` 变量来访问***

```kt
fun main(args: Array<String>) {
    for (arg in args) {
        println(arg)
    }
}
```

> 注意编译的时候不要写，你在编译的时候输入的是编译器的命令行参数，只有在运行时才拿到的你的参数，***命令行参数以空格来区分***，如果想要包含空格的话可以使用 `""` 双引号（Windows）

> 不知道为什么，Kotlin 里面的 `main` 函数不能被重载，当然也不能覆盖了，可是编译以后的 `class` 说明本身是可以被重载的

```java
public final class MainKt {
    public static final void main() {
    }

    public static void main(String[] args) {
        main();
    }
}
```

- **Kotlin 没有原生的获取环境变量的方法，不过我们可以用 Java 里面的，完美兼容**

> 由于 Kotlin 会默认导入 `java.lang.*`，所以位于 `java.lang.System` 包下的 `getenv()` 方法可以拿来用

```kt
fun main(args: Array<String>) {
    val env = System.getenv()
    env.forEach { (key, value) ->
        println("$key=$value")
    }
}

// 输出你电脑里面所有的环境变量，也就是每一个控制台能拿到的信息

fun main(args: Array<String>) {
    val env = System.getenv("PATH")
    env.split(';').forEach {
        println(it)
    }
}

// PATH 里面的信息
```

- 要想拿到 Java 的环境变量，使用 `System.getProperties()` `System.getProperty(key)` 方法

```kt
fun main(args: Array<String>) {
    val env = System.getProperties()
    // env 是 Properties 类型，就是之前反射的属性类型
    for (i in env) {
        println(i)
    }
}
```

> 恭喜你看完本章



# 第十一章：异常处理

> 只要是个高级语言，都会宣传自己的错误处理功能（C：我靠），Java 也是如此，如果你很熟悉 Java 的异常处理，那么你可以直接略过本章，因为大体是一样的

## 11.1 概念

- 下面是 Java 异常的结构图，***所有异常的父类是 `Throwable`，`RunTimeException` 和自己的子类都叫运行时异常（RunTime Exception），`Exception` 和自己非  `RunTime` 的异常，我们叫受检异常（Checked Exception）***

- **受检异常在编译时就可知，而我们真正关心的运行时异常只有在运行时才会被抛出**，对于受检异常，如果你不捕获的话编译是不通过的

```kt
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

> 虽然 Java 的受检异常本心很好，为了让写代码的人在编译时就知道自己要对可能发生的异常做出反应，但是结果就是到处都是 `try catch`，所以

- ***Kotlin 没有受检异常***，比如 Java 里面的 `Thread.sleep()` 是会抛出 `InterruptedException` 的，这是个受检异常，所以你不写在捕捉里是不会编译的

> 但是 Kotlin 可以不写

```kt
fun main(args: Array<String>) {
    println("Hello, Kotlin!")
    Thread.sleep(2000)
    println("Goodbye, Kotlin!")
}
```

```java
public class Test {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("Goodbye, Java!");
    }
}
```

- **Kotlin 里的异常继承结构大体上也是上面的那样子，只不过没有受检异常和运行时异常的区分了**

> [官方文档](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-throwable/)在这，具体哪个是什么样的异常类型不是自己看去


## 11.2 捕捉异常

- Kotlin ***使用 `try catch finally` 语句来捕捉异常***

> `finally` 可选，**但是 `catch` `finally` 必须要有一个**

```kt
try {
    可能产生异常的语句
} catch(异常类型: 异常类型变量名){
    // 将来引用类型的变量会指向一个异常类型
    处理异常的语句
} catch(其他异常类型){
    ···
} finally {
    收尾工作
}
```

```kt
fun main(args: Array<String>) {
    val list = listOf(1, 2, 3, 4, 5)

    try {
        println(list[6])
    }
    catch(e: ArrayIndexOutOfBoundsException) {
        println("No Such Element")
        println(e.message)
    }
}

// 对比前后不使用异常处理的代码，我们发现经过处理后程序是顺利运行结束的，而不是运行失败
```

- ***`try` 里面的代码块如果发生了异常，他会按着 `catch` 接受的类型一个个找下去，找到第一个匹配的 `catch` 就会执行，如果没有匹配的 `catch`，那么就会执行 `finally` 里面的代码，然后程序终止***

- ***如果 `catch` 一个合适的也没有找到，那么程序会报错推出，但是是在执行完 `finally` 里面的语句之后才退出***

```kt
fun main(args: Array<String>) {
    val list = listOf(1, 2, 3, 4, 5)

    try {
        println(list[6])
    }
    catch(e: ArrayIndexOutOfBoundsException) {
        println("No Such Element")
        println(e.message)
        // message 是异常的消息，可以打印出来
        println(e.stackTrace)
        // stackTrace 打印具体信息
    } finally {
        println("Finally block executed")
        // 会被打印
    }
}
```

> 如果使用的 `Native` 的 Kotlin，还有一些方法可供使用，如果跟我一样是命令行 `JVM` `Native` 都存在的话，必须要使用 `kotlinc-native` 来编译

```kt

@kotlin.experimental.ExperimentalNativeApi
fun main(args: Array<String>) {
    val list = listOf(1, 2, 3, 4, 5)

    try {
        println(list[6])
    }
    catch(e: IndexOutOfBoundsException) {
        println("No Such Element")
        println(e.message)
        println()
        println(e.getStackTraceAddresses())
        println()
        println(e.getStackTrace())
        println()
        e.printStackTrace()
    } finally {
        println("Finally block executed")
    }
}

// 说实话这个功能比 JVM 的多
```

- ***`finally` 有两种情况不会被执行，发生了错误和使用了 `System.exit()` 直接退出***

```kt
fun main(args: Array<String>) {
    val list = listOf(1, 2, 3, 4, 5)

    try {
        println(list[6])
    }
    catch(e: ArrayIndexOutOfBoundsException) {
        println("No Such Element")
        println(e.message)
        System.exit(0)
        // 跟 C 一样，程序以 0 退出为成功，其他为失败
    } finally {
        println("Finally block executed")
    }
}
```

- 错误捕获的时候***如果父类在前，那么子类的异常永远不会被捕获***

```kt
fun main(args: Array<String>) {
    val list = listOf(1, 2, 3, 4, 5)

    try {
        println(list[6])
    }
    catch (e: Exception) {
        println("Caught Exception")
        println(e.message)
    }
    catch(e: ArrayIndexOutOfBoundsException) {
        println("No Such Element")
        println(e.message)
    } finally {
        println("Finally block executed")
    }
}
```

- Kotlin 里面的 ***`try catch` 是一个表达式***，也就是他们**可以当作 `lambda` 把自己的最后一行给返回**

```kt
fun main(args: Array<String>) {
    println("please enter a number:")

    val num: Int? = try {
        readln().toInt()
    }
    catch(e: NumberFormatException) {
        println("Invalid input, please enter a number.")
        null
    }
    finally {
        println("Thank you for entering a number.")
        // finally 里的代码不受影响
    }

    println("num = $num")
}
```

## 11.3 使用异常

- ***要想自定义一个异常类型，只需继承自异常类即可***

- 想要***抛出异常，使用 `throw` 关键字***

> Kotlin 没有受检异常，所以**抛出任何异常类都不需要 `try catch`**

> 又与 Java 不同，Kotlin 里面 `throw` 所在的函数不需要声明异常类型

- **`throw` 位于 `try` 里面不会导致程序终止，位于 `try` 外面会终止程序，无论是自己抛出的还是函数里面抛出的**

```kt
fun main(args: Array<String>) {
    try {
        throw CostomException("This is a custom exception")
    }
    catch (e: CostomException) {
        println(e.message)
    }

    throwEx()
}

fun throwEx(){
    throw CostomException("This is a custom exception")
}

class CostomException(message: String) : Exception(message) 
// 可以自定义属性
```

- 同时 ***`throw` 也是一个表达式，他返回一个 `Nothing` 类型***，这是一个很特殊的类型

```kt
fun main() {
    val person = Person(null, 25)
    val name = person.name ?: throw IllegalArgumentException("Name cannot be null")
}

data class Person(val name: String?, val age: Int?)
```

- ***`Nothing` 类型永远没有实例***，也就是你永远找不到它的实际值，所以***返回 `Nothing` 的函数***也就表示该函数永远找不到一个值去返回，也就是该函数***永远不返回（抛异常）***

> 当函数返回 `Nothing` 类型时，相当于是提醒使用者该函数就用来抛异常

```kt
// Nothing
public class Nothing private constructor()

fun main() {
    throwException()
}

fun throwException() : Nothing {
    throw Exception("Something went wrong")
}

// 也挺有意思，永远不返回就表示返回 Nothing
```

- ***`Nothing` 是所有类型的子类***，没错你没听错，它是所有类型的子类

> Java：靠！

```kt
fun main() {
    println("String" is Any)
    println(3 is Number)

    println(Nothing is Any)
    // 放心这里不会被编译，因为 Nothing 又不是单例，他就没有对象，怎么去比较
}
```

> 这就很方便了，比如下面的

```kt
fun main(args: Array<String>) {
    strNullOrNot(null)
}

fun strNullOrNot(str: String?): String {
    if (str == null) {
        throw IllegalArgumentException("String cannot be null")
    } else {
        return str
    }
}

// 简化

fun main(args: Array<String>) {
    strNullOrNot(null)
}

fun strNullOrNot(str: String?): String = if (str == null) throw IllegalArgumentException("String cannot be null") else str

// 这里返回 String? Unit 都可以，因为都是 Nothing 的父类
```

> `return` 的返回值也是 `Nothing` 类型

- `Nothing` 是所有类型的子类一般情况下没有什么问题，因为你也找不到一个合适的值去付给其他变量

- 可是如果当作泛型参数呢？***使用了协变的泛型类型的泛型参数都可以填上 `Nothing`***，这样就有了一个***可以给所有类型初始化的空列表***

```kt
fun main(args: Array<String>) {
    val emptyList = listOf<Nothing>()
    var strList: List<String> = emptyList
    var intList: List<Int> = emptyList

    // 一般都是 var ，否则的话一辈子也不能变了

    println(strList)
    println(intList)
}

// MutableList 这种可变集合是不协变的，所以休想创造一个 union 联合体那样的结构
```

```kt
fun main(args: Array<String>) {
    val x = null

    // 还有就是，直接写 null 值推断出的是 Nothing? 类型，这个是不违反 Nothing 不能有实例的，因为是 null
}
```



# 第十二章：线程和并发

> 这章的内容很多，并且大部分比较抽象，包括 Java 里的多线程、同步、互斥锁等等，也有 Kotlin 里的协程、挂起函数，本章不会对每一个概念都做非常基础的理解，只讲解 API 的使用和简单的介绍，如果哪里有不懂的地方，可以参考官方文档或者其他资料

## 12.1 线程的概念

- ***进程（Process）是操作系统中正在运行的的一个任务***，现代的操作系统基本都可以***多任务并行***，这就像是你可以随意切换程序

- ***线程（Thread）是进程中的一个独立立运行的任务，进程中的线程可以并行***

- ***线程是 CPU 调度和分配的基本单位，进程是操作系统进行资源分配 (包括cpu、内存、磁盘IO等) 的最小单位***，CPU 是看不到其他的进程的，只有操作系统才能看到

- ***进程拥有自己独立立的内存地址空间等资源，一个进程中的所有线程共享进程的内存地址空间等资源***

> 注意，不要着急理解多核心 CPU 的调度，先假设这是单核心

- 并行和并发都是同一时间运行多个任务，***并发 (Concurrent) 是逻辑上同时运行，但由于 CPU 的速度快，在感知上像是所有的任务都在同一时间运行着，实际上是依靠调度器切换来切换去的运行***

![](https://i-blog.csdnimg.cn/blog_migrate/2190b36b6bb9edb821b825cf45f8bc32.png)

- ***并行 (Parallel) 是物理上的同时运行，比如多核心 CPU 每一个核心运行着不同的任务***，本文中可能有些地方会把二者混淆请注意区分

![](https://i-blog.csdnimg.cn/blog_migrate/abeb21004d0aed99d460ecfbab8aab73.png)

> 那回过头来，我们为什么需要多线程呢？目前讲到的地方好像没有需要并行需求的啊？

- 当我们编写图像界面的程序的时候，比如在 `main()` 方法里有一个耗时的计算操作，因为程序是一步一步执行的，所以当这个操作需要花费很长的时间，用户就会感觉到界面卡顿，这时候我们就可以使用多线程来解决这个问题，让程序的执行不被阻塞，让用户感觉不到卡顿

- **多线程（Multi Threade）的出现，就是为了解决我们想让某些前台任务和后台任务同时运行的需求**

## 12.2 创建线程

> 本节先来介绍 Java 中的线程相关的 API，协程的放在后面

- ***一个进程最起码有一个线程***（主线程，Main Thread），我们的 `main()` 就运行在主线程

### 12.2.1 Thread

- 要创建新的线程，可以***继承自 `Thread` 类，覆盖 `run()` 方法，`run()` 里面的代码就是一个线程要执行的任务***

```kt
fun main(args: Array<String>) {
    
    println("Main Thread is running")

    val myThread1 = MyThread()
    myThread1.run()

    val myThread2 = MyThread()
    myThread2.run()
    
    println("Main Thread is finished")
}

class MyThread : Thread() {
    override fun run() {
        println("MyThread is running")
        for (i in 1..10) {
            println(i)
        }
        println("MyThread is finished")
    }
}
```

> 但是可以看到这种方法并没有创建出我们预期中的两条线程同时运行的状态，而是一个接一个（串行，Serial）的执行

- 去***开启一个线程，可以直接调用 `Thread` 类的 `start()` 方法***，这时候线程就会在内存中开辟一块自己的空间，然后执行 `run()` 方法，这时候他就跟 `main()` 方法所在的主线程一起并行运行了

> 何为开辟一块自己的空间？我们知道一个函数（方法）对应一个内存中的栈，那么开启一个新线程可以简单理解为新开了一块栈，这个栈内的函数在自己的空间内再一层层运行，如果不理解栈的概念可以看我的 C 入门

> `main` 函数所在的函数栈执行完后（`main` 的最后一个语句结束了），主线程也就退出了，同样，自己开辟的线程在执行完 `run()` 方法后也就结束了

```kt
fun main(args: Array<String>) {
    
    println("Main Thread is running")

    val myThread1 = MyThread("MyThread1")
    myThread1.start()

    val myThread2 = MyThread("MyThread2")
    myThread2.start()
    
    println("Main Thread is finished")

    // main 方法在开启两条线程后就结束了
    // 每一次打印的顺序都不一样，这是操作系统决定的
}

class MyThread (val tName: String = "MyThread") : Thread() {
    override fun run() {
        println("$tName is running")
        for (i in 1..10) {
            println("$tName is running $i")
        }
        println("$tName is finished")
    }
}
```

### 12.2.2 Runnable

- 也可以***实现 `Runnable` 接口，覆盖 `run()` 方法，然后创建 `Thread` 对象，并传入 `Runnable` 对象，这样也可以创建线程***

- ***`currrentThread().name` 可以获取当前线程的名字***

```kt
fun main(args: Array<String>) {
    println("${Thread.currentThread().name} is running")

    val mt1 = Thread(MyThread())
    // Runnable 传入 Thread 的构造方法
    mt1.start()

    val mt2 = Thread(MyThread())
    mt2.start()

    println("${Thread.currentThread().name} is finished")
}

class MyThread : Runnable {
    override fun run() {
        println("Thread ${Thread.currentThread().name} is running")
        println("Thread ${Thread.currentThread().name} is finished")
    }
}
```

- 我们***也可以使用匿名类实现 `Thread` 接口，然后调用 `start()` 方法***

```kt
Thread(object : Runnable {
    override fun run() {
        println("Hello World")
    }
}).start()

// 因为 Runnable 接口只有一个方法，所以可以使用 Kotlin 的语法糖

Thread(Runnable {
    override fun run() {
        println("Hello World")
    }
}).start()

// 又可以再简化

Thread {
    println("Hello World")
}.start()
```

- 相比直接使用 `Thread` 开线程，**继承 `Runnable` 可以实现多继承的优点**（因为它是接口），虽然麻烦了些

```kt
import kotlin.random.Random

interface Person {
    val age: Int
    val name: String
    fun sayHello(str: String = this.name, num: Int = this.age)
}

class Worker(override var age: Int, override var name: String) : Person, Runnable {
    override fun sayHello(name: String, age: Int) {
        println("old name: ${this.name}, age: ${this.age}")
        this.name = name
        this.age = age
        println("new name: ${this.name}, age: ${this.age}")
    }

    override fun run() {
        sayHello()
        println("${Thread.currentThread().name}")
        sayHello(Random.nextInt(0, 100).toString(), Random.nextInt(100, 200))
    }
}

fun main() {
    val worker = Worker(25, "John")
    worker.run()
    // 再次记住，直接 run 不会启动新的线程
    Thread(worker).start()
    // 当作 Runnable 传入 Thread 的构造方法启动后，run 里面仍然可以访问自己类的属性和方法

    // 不同线程间可以通过相同的引用访问同一个实例，这里记住了
}
```

- 当然 Kotlin 也提供了更简便的写法，***使用 `thread()` 函数，传入一个 lambda 表达式，这个 lambda 表达式就是线程要执行的任务，并且会立即执行***

> 或者使用 Kotlin 对单方法接口的支持直接写也行，注意 `thread() ` 位于协程里，后面再说，目前推荐下面一的方式

```kt
fun main() {
    println(Thread.currentThread().name)

    Thread {
        println(Thread.currentThread().name)
    }.start()

    Thread {
        println(Thread.currentThread().name)
    }.start()
}
```

```kt
import kotlin.concurrent.thread

// 导入 kotlin.concurrent.thread 才可以使用 thread 函数

fun main() {
    println(Thread.currentThread().name)

    thread {
        println(Thread.currentThread().name)
    }

    thread {
        println(Thread.currentThread().name)
    }
}
```

```kt
// 这是 thread 函数的源码，注意参数即可

public fun thread(
    start: Boolean = true, // 如果不想立即启动，修改此即可
    isDaemon: Boolean = false,
    contextClassLoader: ClassLoader? = null,
    name: String? = null,
    priority: Int = -1,
    block: () -> Unit
): Thread {
    val thread = object : Thread() {
        public override fun run() {
            block()
        }
    }
    if (isDaemon)
        thread.isDaemon = true
    if (priority > 0)
        thread.priority = priority
    if (name != null)
        thread.name = name
    if (contextClassLoader != null)
        thread.contextClassLoader = contextClassLoader
    if (start)
        thread.start()
    return thread
}
```

## 12.3 线程的状态

- 接下来我们看一下***线程的几种状态***

```mermaid
stateDiagram-v2
    [*] --> New（初始状态）: 实例化
    New（初始状态） --> Ready（就绪状态）: start()
    Ready（就绪状态） --> Running（运行中）: 系统调度
    Running（运行中） --> Blocked: 访问带锁的资源
    Blocked --> Ready（就绪状态）: 拿到锁
    Running（运行中） --> Waiting: 等待其他线程
    Waiting --> Ready（就绪状态）: 被其他线程叫醒
    Running（运行中） --> TimedWaiting: 等待
    TimedWaiting --> Ready（就绪状态）: 超时或被通知叫醒
    Running（运行中） --> Terminated: 执行完毕
    Terminated --> [*]
```

1. ***`New`（初始状态）：线程刚被创建，尚未启动***
2. ***`Runnable`（运行）：包括就绪（Ready）和运行中（Running）两种状态***。线程处于 Runnable 状态时，表示线程可以被调度运行，他**可能正在运行，也可能正在等待资源，这个是由操作系统随时决定的**，虚拟机是管不了的
3. ***`Waiting`（等待）***：可以调用指定方法，让一个线程**进入等待状态，直到被其他线程唤醒**
4. ***`Timed Waiting`（定时等待）***：可以让一个线程在指定时间内进入等待状态，在时间到达后自动唤醒，注意***唤醒后他进入的是就绪状态，不会立即执行***，所以**休眠时你给定的时间一定是小于等于（不太可能等于）实际休眠时间的**
5. ***`Blocked`（阻塞）***：这个后面讲互斥锁的时候讲，当多个线程同时访问一个有锁的资源时，会进入此
6. ***`Terminated`（终止）：线程已经执行完毕***，或者被提前终止，这个是看线程的 `run()` 方法是否执行完成，**当一个线程执行完毕后，他就死了永远不能复活**

- **`Thread` 类有很多方法可以为我们使用**

| `Thred` 构造方法|作用|
|---|---|
|`Thread()`|默认构造方法，创建一个线程，但没有指定线程的名字，线程的名字是自动生成的|
|`Thread(Runnable target)`| 创建一个新的线程，并指定该线程的 `Runnable` 对象|
|`Thread(String name)`| 创建一个新的线程，并指定该线程的名字|
|`Thread(Runnable target, String name)`| 创建一个新的线程，并指定该线程的 `Runnable` 对象和名字|
|`Thread(ThreadGroup group, String name)`| 创建一个新的线程，并指定该线程的名字和线程组|
|`Thread(ThreadGroup group, Runnable target, String name)`| 创建一个新的线程，并指定该线程的 `Runnable` 对象、名字和线程组|

| `Thread` 方法|作用|
|---|---|
|`getID`|获取线程的唯一标识符|
|`getName`|获取线程的名字|
|`getState`|获取线程的状态|
|`getPriority`|获取线程的优先级|
|`isAlive`|判断线程是否存活|
|`isDaemon`|判断线程是否为守护线程|

|`Thread` 状态切换|作用|
|---|---|
|`start()`|启动线程|
|`run()`|线程执行体|
|`sleep(long millis)`|线程休眠，让线程进入 `Timed Waiting` 状态，参数为休眠时间，单位为毫秒|
|`yield()`|让出当前线程的执行权进入 `Ready` 状态，让其他线程有机会执行，但是一切都是操作系统说了算|
|`wait()`|等到线程锁的时候再细说|
|`join()`|让自己（也就是声明 `join()` 所在的代码块所在的线程）进入等待状态，直到被调用线程（`join()` 的接收者）执行完毕|
|`interrupt()`|中断线程，后面再说|

- ***使用静态方法 `Thread.currentThread()` 可以获取当前线程的实例***，下面是一个例子说明每个线程状态转换的过程

```kt
import java.time.LocalDateTime


fun main() {
    println("${Thread.currentThread().name} is ${Thread.currentThread().getState()} at ${LocalDateTime.now()}")
    println()

    val t1 = Thread {
        println("${Thread.currentThread().name} is ${Thread.currentThread().getState()} at ${LocalDateTime.now()}")
        Thread.sleep(1000)
        // Java 这里是必须 try 的，之前讲过 Kotlin 没有受检异常
        println("${Thread.currentThread().name} is going to finish at ${LocalDateTime.now()}")
    }

    val t2 = Thread {
        println("${Thread.currentThread().name} is ${Thread.currentThread().getState()} at ${LocalDateTime.now()}")
        Thread.sleep(2000)
        println("${Thread.currentThread().name} is going to finish at ${LocalDateTime.now()}")
    }

    println("${t1.getName()} is ${t1.getState()} at ${LocalDateTime.now()}")
    println("${t2.getName()} is ${t2.getState()} at ${LocalDateTime.now()}")
    println()

    t1.start()
    t2.start()

    println("${Thread.currentThread().name} ID is ${Thread.currentThread().getId()}")
    println("${t1.getName()} ID is ${t1.getId()}")
    println("${t2.getName()} ID is ${t2.getId()}")

    println("${Thread.currentThread().name} is ${Thread.currentThread().getState()} at ${LocalDateTime.now()}")
    t1.join()
    t2.join()
    // 试着去注释掉这两行 join() 看看会发生什么

    println("${Thread.currentThread().name} is ${Thread.currentThread().getState()} at ${LocalDateTime.now()}")

    println("${Thread.currentThread().name} is finished.")
}
```

- ***`yield()` 和 `sleep()` 都是静态的，直接调用的时候是看你声明的位置而不是接收者***，也不建议调用实例上的 `yield()` 和 `sleep()`

- ***`sleep()` 让代码暂停***，位于它的代码不会立即执行，而是等待，***但是实际花费的时间一定是比声明的参数多的***，见上面的流程图

```kt
import kotlin.time.*

fun main() {
    val timeSource = TimeSource.Monotonic
    val startTime = timeSource.markNow()

    val t1 = Thread {
        println("Start a Thread cost ${timeSource.markNow() - startTime} seconds")
        val mark1 = timeSource.markNow()
        Thread.sleep(1000)
        println("Thread sleep 1 second actually cost ${timeSource.markNow() - mark1} seconds")
    }

    t1.start()
}
```

- 对于***单核 CPU ，实际上它每次只在运行同一个线程，通过操作系统不断切换制造出多核心的假象（还有超线程也是同样的道理），也就是并发***

- 但是对于***多核心 CPU ，操作系统会自动分配线程到不同的核心上，让每个核心都有自己的线程，这就是并行***，是真正的物理上的同时运行

- 也就说***同一个进程里的线程是可以存在于不同的 CPU 上的***

> 这里不讨论用户态和内核态的概念，包括讲协程的时候也是，你记住 JVM 的调度是可以把同一进程下的线程调度到不同的 CPU 上的，具体系统的调度和调度策略可以自行了解查阅

> 比如下面这段代码，根据你电脑核心数改变 `repeat()` 的参数，你就会发现你的 CPU 会满负荷运行，如果你再增加线程数的话也不会加快速度，反而**因为连续的调度会降低性能**，如果 Java 不是内核态的话，这段代码是不可以占满 CPU 的

```kt
fun main() {
    repeat(12) { // 输入你电脑的 CPU 物理核心数
        Thread {
            for (i in 1L..100_1000L) {
                test(i)
            }
        }.start()
    }

}

fun test(num: Long): Boolean {
    when {
        num < 2 -> return false
        else -> {
            for (i in 2L..num) {
                if (i == num) {
                    return true
                } else if (num % i == 0L) {
                    return false
                }
            }
        }
    }
    return true
}
```

- 所以说，***一般有两种情况需要多线程：不阻碍前台常驻线程和需要发挥所有 CPU 核心的性能***

> 上面说了线程的调度全看操作系统，那就没什么办法手动干预下？

- ***可以通过 `setPriority()` 设置线程的优先级，通过 `getPriority()` 获取线程的优先级，等级高优先调度***

- ***默认优先级为 5 ，最低是 1 （Thread.MIN_PRIORITY），最高是 10 （Thread.MAX_PRIORITY），不保证百分百灵验***，最多是告诉使用者这个线程的优先级如何

```kt
fun main() {
    val t1 = Thread {
        println("My name is ${Thread.currentThread().name} and my priority is ${Thread.currentThread().getPriority()}")
    }

    val t2 = Thread {
        println("My name is ${Thread.currentThread().name} and my priority is ${Thread.currentThread().getPriority()}")
    }

    val t3 = Thread {
        println("My name is ${Thread.currentThread().name} and my priority is ${Thread.currentThread().getPriority()}")
    }

    t1.setPriority(Thread.MAX_PRIORITY)
    t2.setPriority(Thread.MIN_PRIORITY)
    t3.setPriority(Thread.NORM_PRIORITY)

    t1.start()
    t2.start()
    t3.start()
}
```

## 12.4 守护线程

> 问一下，当 `main()` 方法结束后，虚拟机就结束了吗？

- JVM 虚拟机判断自己结束的依据是：***所有的用户线程（User Thread）执行完毕后便结束自己的进程***

- ***守护线程（Daemon Thread）指的是当其他线程结束后自己便自动退出的线程***，可以通过线程实例的 `setDaemon(true)` 来创建一个守护线程

```kt
fun main() {
    val thread = Thread {
        println("${Thread.currentThread().name} is running")
        Thread.sleep(5000)
        println("${Thread.currentThread().name} is done")
    }

    thread.setDaemon(true) // 可以观察注释掉这里以后的现象
    thread.start()
    println("Main thread is running")
    Thread.sleep(2000)
    println("Main thread is done")
}
```

- ***`main()` 主线程也是用户线程***，他结束后并不影响其他的线程继续工作，虚拟机会等所有的用户线程都执行完后再结束

- **`main()` 不能为守护线程**，因为你没法对一个已经运行的线程设置守护与否，***`setDaemon()` 必须发生在 `start()` 前***，但是我们做不到

```kt
fun main() {
    val main = Thread.currentThread()
    main.setDaemon(false)
}

// Exception in thread "main" java.lang.IllegalThreadStateException
```

## 12.5 线程组

- **线程组可以方便我们管理线程**，可以对线程进行分组，***使用 `ThreadGroup` 类创建一个线程组***

```kt
fun main() {
    println("Thread name: ${Thread.currentThread().getName()}\tThread Group name: ${Thread.currentThread().getThreadGroup().getName()}")

    val group = ThreadGroup("MyThreadGroup")
    val thread1 = Thread(group, MyRunnable(), "MyThread - 1")
    val thread2 = Thread(group, MyRunnable(), "MyThread - 2")

    println(group.getParent())
    group.setMaxPriority(Thread.NORM_PRIORITY)
    // 所有子线程的最大优先级不超过这个
    
    thread1.start()
    thread2.start()

}

class MyRunnable : Runnable {
    override fun run() {
        println("Thread name: ${Thread.currentThread().getName()}\tThread Group name: ${Thread.currentThread().getThreadGroup().getName()}")

        // 线程实例通过 getThreadGroup 获取所在线程组
    }
}
```

- `main()` 方法也有自身的线程组，**每一个线程组实例可以通过 `getParent()` 获取父级的线程组**

```mermaid
---
title: 线程组
---
flowchart LR
System --> MainThreadGroup
MainThreadGroup --> MyThreadGroup
MainThreadGroup --> MainThread
MyThreadGroup --> MyThread1
MyThreadGroup --> MyThread2
```

- 线程组还可以统一管理子线程抛出的异常，***覆写 `uncaughtException()` 方法以处理异常***

```kt
fun main() {
    val group = object : ThreadGroup("MyGroup") {
        override fun uncaughtException(t: Thread, e: Throwable) {
            println("${this.name} caught exception: $e in thread $t")
        }
    }


    val t1 = Thread(group, Runnable {
        throw RuntimeException("Exception in thread 1")
    })
    t1.start()
}
```

## 12.6 线程同步

### 12.6.1 内存模型

- 我们知道，**方法或函数使用的内存区域叫栈（Stack），而创建对象使用的内存区域叫堆（Heap）**
  
- 上面讲过，同一个进程内的所有线程共享同一块内存区域，你可以简单理解为就是堆区，虽然不同的线程使用的栈内存间无法互相访问，但是是可以访问同一块堆区的
  
```kt
fun main() {
    val runnable1 = MyRunnable("Runnable1")
    val runnable2 = MyRunnable("Runnable2")

    Thread(runnable1).start()
    Thread(runnable2).start()
}

const val STR = "Hello, world!"

class MyRunnable (val str: String) : Runnable {
    val obj = Any() // 不同的 Runnable 对象会 new 自己的

    override fun run() {
        println(str) // 可以访问局部变量
        println(obj) // 访问自己的成员变量
        println(STR) // 可以访问静态共享的常量
    }
}
```

```mermaid
---
title: Java 多线程内存模型
---
flowchart LR
    subgraph 内存
        direction LR
        subgraph 栈
            direction TB
            subgraph Main
                direction LR
                t1[Thread]
                ts1[Main Stack]
            end
            subgraph Thread1
                direction LR
                t2[Thread1]
                subgraph 局部变量
                    direction TB
                    val1["val1 指向 obj1"]
                    val2["val2 指向 obj2"]
                end
            end
        end
        subgraph Heap
            direction TB
            o1[成员变量]
            obj1[obj1]
            obj2[obj2]
        end
    end
```

```kt
fun main() {
    val obj = Any()

    val runnable = MyRunnable(obj) // 虽然 Runnable 是两个，但是其内部的成员变量 obj 都指向同一个堆内的对象
    val runnable2 = MyRunnable(obj)

    Thread(runnable).start()
    Thread(runnable2).start()
}


class MyRunnable (val obj: Any) : Runnable {
    // 这里 obj 本身是成员变量位于堆内，不同的对象拥有不同的
    // 但是 obj 指向的堆内对象是同一个，是位于 main 方法里声明的那个，对象的引用可以在不同线程之间传递
    override fun run() {
        val obj = Any()

        println("Local variable: $obj") // 局部变量各自不同
        println("Instance variable: ${this.obj}")
    }
}
```


- **CPU 并不是直接使用内存进行读写，CPU 拥有缓存，每一次在对内存中的数据进行操作的时候，它会把数据传递过一层层缓存递给寄存器，然后对寄存器中的数据进行读写，之后再写回去**

- **每一次线程获取的数据，不一定是缓存上的也不一定是主内存上的，不作保证**

> 还有一个**缓存一致性**，不同寄存器之间也会互相访问，有兴趣的自己查阅吧

```mermaid
flowchart LR
    subgraph CPU 与内存
        direction LR
        subgraph CPU
            direction TB
            subgraph CPU Core 1
                direction LR
                subgraph Thread1
                end
                subgraph 寄存器1
                end
                subgraph L1 L2 L3
                end
            end
            subgraph CPU Core 2
                direction LR
                subgraph Thread2
                end
                subgraph 寄存器2
                end
                subgraph L1 L2 L3
                end
            end
        end
        subgraph RAM
            direction LR
            subgraph 栈
                direction TB
                subgraph Thread Stack 1
                end
                subgraph Thread Stack 2
                end
            end
            subgraph 堆
            end
        end
    end
```

- 那么有些时候 CPU 不会一遍又一遍的访问内存，会省事使用寄存器中的数据，***线程中的竞争问题就发生在 CPU 的数据和内存中的数据不同步的情况下***

- 因为存在的延迟，所以就会导致一些情况下的***线程竞争（race condition）***，比如：

```kt
var count = 0

fun countPlus() {
    count++
}

fun main() {
    val t1 = Thread {
        for (i in 1..1000) {
            countPlus()
            // 如果使用默认的 ++ ，结果是同步的，应该是使用了线程同步
        }
    }

    val t2 = Thread {
        for (i in 1..1000) {
            countPlus()
        }
    }

    t1.start()
    t2.start()

    t1.join()
    t2.join()

    println("Final count is $count")
}

// 最后的结果一定不是 2000
```

> 上面代码里这两个线程都在访问同一个函数，有时候就会导致一个线程刚刚拿到的值，加了一，还没有写回去，另外一个线程拿到了原来的值加一放了进去覆盖了他本来要加一的值，导致加二变为了加一

> 本文不愿意去讲 Java 的底层实现原理，因为毫无意义，这又不是 CPP，这是简化过后的


- 多线程并发有三个特性：***原子性（Atomicity）、可见性（Visibility）、有序性（Ordering）***
    - ***原子性也就指的是不可被拆分的最小执行动作***
  
    > 像是上文里的自增 `count++`，就不是原子性的，因为它需要 `1.拿到值 2.增加值 3.写回值` 三个操作，而 `count == 1` 就是原子性的，因为只有一个操作赋值

    - ***可见性是指一个线程修改了的值会立即在主内存中被其他线程更新到***
    
    > 上文里数据不一致就从堆中加载和保存不同步更新，导致不同的线程之间对于互相的操作没有可见性，这点我们会在后面的 `volatile` 中细讲

    - ***有序性是指程序执行的顺序按照代码的先后顺序执行***，后面再说，这里只是一提

- **多线程中最复杂的就是这些对于线程共享资源的访问和限制**

### 12.6.2 synchronized

#### 12.6.2.1 注解方式

- ***使用 `synchronized` 关键字可以让被修饰的函数拥有线程锁，不同的线程只有拿到锁的才能执行该函数，其他线程必须等待锁被释放后才能执行***

> Kotlin 里面并没有 `synchornized` 这个关键字，取而代之的 `@Synchronized` 注释

```kt
var count = 0

@Synchronized
fun countPlus() {
    count++
}

fun main() {
    val t1 = Thread {
        for (i in 1..1000) {
            countPlus()
        }
    }

    val t2 = Thread {
        for (i in 1..1000) {
            countPlus()
            // 无论有多少个线程，只要他们访问的是同一个方法（这里是静态方法，具体后面讲），谁拿到锁才能用，其他线程必须等待有锁的线程释放锁
        }
    }

    t1.start()
    t2.start()

    t1.join()
    t2.join()

    println("Final count is $count") // 2000
}
```

- 所谓 ***`synchronized` 锁住的是一个对象，如果一个方法是 `synchronized` 的，那么当一个线程拿到这个对象的锁时，他就能访问这个对象的成员，无论是不是 `synchronized` 的***

> ***`synchroized` 是可重入锁***，这个我们还会讲

```kt
fun main() {
    val counter = Counter()

    val t1 = Thread {
        for (i in 1..100_0000) {
            counter.increment()
        }
    }

    val t2 = Thread {
        for (i in 1..100_0000) {
            counter.incrementAndGet()
        }
    }

    t1.start()
    t2.start()

    t1.join()
    t2.join()

    println("Final count: ${counter.incrementAndGet() - 1}")
}

class Counter {

    private var count = 0

    fun increment() {
        synchronized(this) {
            incrementAndGet()
            // 如果 synchronized 不是可重入的，这里线程一获得 Counter 的锁，然后有去获得锁，可是锁已经被拿走了（自己），所以就会一直拿不到锁，卡死在这里
        }
    }

    fun incrementAndGet(): Int {
        synchronized(this) {
            count++
        }

        return count
    }
}
```

- 但因为是对象，所以**不同对象间拥有不同的锁，一个对象一个锁，互不干扰**
  
```kt
fun main() {
    val t1 = Thread {
        for (i in 1..100) {
            Person("John", 25)
        }
    }

    val t2 = Thread {
        for (i in 1..100) {
            Person("Jane", 30)
        }
    }

    t1.start()
    t2.start()

    t1.join()
    t2.join()

    println("Total persons created: ${Person.counter}")
}

class Person {
    val name: String
    var age: Int

    constructor(name: String, age: Int) {
        this.name = name
        this.age = age
        addCounter()
    }
    @Synchronized // 在这加没用，因为都不是一个实例
    fun addCounter() {
        counter++
    }

    fun sayHello() {
        println("Hello, my name is $name and I am $age years old.")
    }

    companion object {
        var counter = 0
    }
}
```

- `synchronized` 除了可以注释方法，还可以***注释静态方法，这样它锁住的是这个类的 `Class` 对象***，就是我们之前在反射讲过的，因为***一个类只有一个 `Class` 对象，所以所有调用这个静态方法的地方都会线程同步***，无论是在相同与否的线程或实例

```kt
class Person {

companion object {
   private var count = 0

   @JvmStatic
   // 因为使用顶层方法不太直观，这里使用 @JvmStatic 注解表示该方法是真静态，这也是一种声明静态方法的手段
   @Synchronized
   fun counter() {
       count++
       println("${Thread.currentThread().name} called counter() $count times.")
       }
   }
}

fun main() {
   for (i in 1..100) {
       Thread {
           for (j in 1..1000) {
               Person.counter()
           }
       }.start()
   }
}
```

#### 12.6.2.2 监视器对象

- 还可以使用 ***`synchronized` 代码块，参数是监视者对象（Monitor Object）***，所谓**监视者监视多个线程同时执行 `synchronized` 代码块的时候，不同的监视者会让自己的线程只有一个可以获取倒锁，不同的监视者管理着不同的线程**

```kt
fun main() {
    val counter = Counter()

    val t1 = Thread {
        for (i in 1..1000) {
            counter.increment1()
            Counter.increment2()
            counter.increment3(counter)
            // counter.increment3(Any())
            // 如果是 Any() 的话就跟没加锁是一样的
        }
    }


    val t2 = Thread {
        for (i in 1..1000) {
            counter.increment1()
            Counter.increment2()
            counter.increment3(counter)
            // counter.increment3(Any())
        }
    }

    t1.start()
    t2.start()

    t1.join()
    t2.join()

    println("Counter value: ${counter.count1}")
    println("Counter value: ${Counter.count2}")
    println("Counter value: ${counter.count3}")

}


class Counter {

    var count1 = 0
    var count3 = 0

    fun increment1() {
        synchronized(this) {
            // 等于 @Synchronized
            count1++
        }
    }


    fun increment3(obj: Any) {
        synchronized(obj) {
            // 如果对象一样则有锁，否则没有锁
            count3++
        }
    }
    
    companion object {
        var count2 = 0
        
        fun increment2() {
            synchronized(this::class.java) {
                // @Synchronized
                // @JvmStatic
                count2++
            }
        }
        
    }
}

```

> 再理解下监视器对象的意义

```mermaid
---
title: Monitor Object
---
flowchart LR
    Object1-- synchroized -->Thread1
    Object1-- synchroized -->Thread2
    Object2-- synchroized -->Thread3
```

> 如果对象不一样，Object2 是管不了 Thread 2 与自己的 Thread 3 有没有锁的

```kt
fun main() {
    val counter = Counter()
    val obj = Any()

    val t1 = Thread {
        for (i in 1..100_0000) {
            counter.increment(obj)
        }
    }


    val t2 = Thread {
        for (i in 1..100_0000) {
            counter.increment(obj)
        }
    }

    val t3 = Thread {
        for (i in 1..100_0000) {
            counter.increment(Any())
        }
    }

    t1.start()
    t2.start()
    // t1 t2 是线程同步的，但是 t3 不是
    t3.start()

    t1.join()
    t2.join()
    t3.join()

    println(counter.getCount())
}

class Counter {
    private var count = 0

    fun increment(obj: Any) {
        synchronized(obj) {
            count++
        }
    }

    fun getCount() = count
}
```

```kt
fun main() {
    val counter = Counter()

    val t1 = Thread {
        for (i in 1..100_0000) {
            counter.increment1()
        }
    }


    val t2 = Thread {
        for (i in 1..100_0000) {
            counter.increment2()
        }
    }

    t1.start()
    t2.start()

    t1.join()
    t2.join()

    println(counter.getCount())
    // 结果并没有线程同步，因为这是两个对象
}

class Counter {
    private var count = 0

    private var obj1 = Any()
    private var obj2 = Any()

    fun increment1() {
        synchronized(obj1) {
            count++
        }
    }

    fun increment2() {
        synchronized(obj2) {
            count++
        }
    }

    fun getCount(): Int {
        return count
    }
}
```

> ***`synchronized` 代码块的参数可以是任意一个对象，比如 `Any()` `Unit` 都可以***，但是**最好不要用字符串，你不知道他会不会复用常量池里的已有的字符串，可能会有隐患**

- 因为 **`synchronized` 锁住的是一个对象，而 `static synchronized` 锁住的是 `Class` 对象**，所以***可以存在两个线程同时访问 `synchronized` 和 `static synchronized` 的情况***
  
> 同时访问 `synchronized` 和 `static synchronized` 锁仍然是生效的

```kt
fun main() {
    val counter = Counter()

    val t1 = Thread {
        for (i in 1..1000) {
            counter.increment()
        }
    }


    val t2 = Thread {
        for (i in 1..1000) {
            counter.getAndIncrement()
        }
    }

    t1.start()
    t2.start()

    t1.join()
    t2.join()

    println("Counter value: ${counter.count}")

}


class Counter {

    var count = 0

    @Synchronized
    fun increment() {
        count++
    }

    fun getAndIncrement() : Int {
        synchronized(this::class.java) {
            count++
            return count
        }
    }
}

// 结果可能会变化，多试几次应该会有不是 2000 的结果
```

- 使用 `synchroized` 的代码块的方式，***只有写在 `synchroized` 里面的才会有锁，外部的不会同步***

```kt

fun main() {
    val counter = Counter()
    val t1 = Thread {
        for (i in 1..10_0000) {
            counter.increment()
        }
    }
    val t2 = Thread {
        for (i in 1..10_0000) {
            counter.increment()
        }
    }
    t1.start()
    t2.start()
    t1.join()
    t2.join()


    counter.print()
}


class Counter {
    private var count = 0
    private var c = 0

    fun increment() {
        synchronized(this) {
            count++
        }
        c++
    }

    fun print() {
        println("Count: $count, c: $c")
    }
}
```

#### 12.6.2.3 wait notify

- ***使用 `wait()` 对拥有锁的对象主动释放锁，`notify()` 唤醒等待的线程去争取锁，`notifyAll()` 唤醒所有等待的线程去争取锁***

- ***当多个线程访问同一个监视器对象的 `synchroized` 锁的时候，争取不到的会进入同步队列（Synchronize Queue），变为阻塞状态直到锁被释放，再去争取，争取不到的继续等***

- ***当调用 `wait()` 的时候，当前执行线程会放弃锁，进入等待队列（Wait Queue），直到其他的线程调用 `notify()` 或者 `notifyAll()`，才会进入同步队列，排队等待获取锁***

> **一定注意 `notify()` 唤醒后进入的是同步队列还要等**

- 注意，***`wait()` `notify()` `notifyAll()` 只能在监视器对象上调用，而这个对象只能是 Java 的 `Object`***，Kotlin 的 `Any` 不行，而且***只能在 `synchroized` 代码块里面调用***，外面是没有意义的

> 相比 `Thread.sleep()` 是一个静态方法，这个 `Object().wait()` 更强调监视器对象的概念

```kt
// 一个例子讲解 wait notify 


fun main() {
    val emails = EMails()

    val t1 = Thread {
        for (i in 1..10) {
            emails.addEmail("email$i@gmail.com")
        }
        println("${Thread.currentThread().name} has added emails done")
    }

    val t2 = Thread {
        for (i in 1..10) {
            println(emails.getEmails())
        }
        println("${Thread.currentThread().name} has fetched emails done")
    }

    t1.start()
    t2.start()
}

class EMails {
    private val inbox = mutableListOf<String>()
    private val maxEmails = 3
    private val lock = Object()

    fun addEmail(email: String) {
        synchronized(lock) {
            while (inbox.size >= maxEmails) {
                println("Inbox is full, waiting for space")
                lock.wait()
            }
            inbox.add(email)
            lock.notifyAll()
        }
    }

    fun getEmails(): String {
        synchronized(lock) {
            while (inbox.isEmpty()) {
                println("Inbox is empty, waiting for emails")
                lock.wait()
            }
            val result = inbox.removeLast()
            lock.notifyAll()
            return result
        }
    }
}
```

- **`wait()` 除了有无参的版本，还有带参的版本，带参的版本是指定等待时间，过了指定时间后自动唤醒**

- 如果***想要中断一个线程，可以使用 `interrupt()` 方法，这个方法不会立即中断线程，但是修改目标线程的 `isInterrupt` 属性***，可以在对应的地方捕获并终止

```kt
fun main() {
    val t1 = Thread {
        var count = 0

        for (i in 1..1_0000_0000) {
            if (Thread.currentThread().isInterrupted) {
                break
            }
            count = i
        }

        println("Thread 1 finished, $count")
    }

    t1.start()
    Thread.sleep(1)
    t1.interrupt()
}

// 也可以这样

fun main() {
    val runnable = object : Runnable {
        var exit = false
        private var count = 0

        override fun run() {
            for (i in 1..1_0000_0000) {
                if (exit) {
                    break
                }

                count = i
            }

            println("Thread finished. Count: $count")
        }
    }

    val t1 = Thread(runnable)
    t1.start()

    Thread.sleep(1)
    runnable.exit = true
}
```

> 不建议使用 `stop` `suspend` `resume` 等等被废弃的方法

- 只有以下几种情况持有锁的线程会释放锁： 
    1. **当前线程的同步方法、代码块执行结束的时候释放**
    2. **当前线程在同步方法、同步代码块中遇到 `break` `return` 终于该代码块或者方法的时候释放**
    3. **当前线程出现未处理的 `error` 或者 `exception` 导致异常结束的时候释放**
    4. ***调用 `obj.wait()` 会立即释放锁，当前线程暂停，释放锁，以便其他线程可以执行 `obj.notify()`，但是 `notify()` 不会立刻立刻释放 `sycronized(obj)`中的 `obj` 锁，必须要等 `notify()` 所在线程执行完 `synchronized(obj)` 块中的所有代码才会释放这把锁。而 `yield()`,`sleep()`不会释放锁***

    > 记住 `sleep` `yield` 不会放锁，虽然线程已不再执行


### 12.6.3 volatile

- `volatile` 关键字是 Java 语言提供的一种**轻量级同步机制**，可以保证***多个线程对某个变量的修改立即可见***，即**一个线程修改了某个变量的值，其他线程立即可以看到这个修改**

> Kotlin 没有 `volatile` 关键字，有 ***`@Volatile` 注解，注意只能用来修饰属性***

```kt
class Counter {
    @Volatile
    var count = 0
}
```

> 可以看上面的内存模型图，**`volatile` 变量的读写操作会立即对主内存同步，保证每一条线程的可见性**，但是***并不保证原子性***，比如 `count++` 不是原子操作，中间有其他线程抢占了 CPU，导致 `count` 不是原来的 `count + 1`

### 12.6.4 指令重排和先行发生

```kt
b = a + c   // 1
c = a + b   // 2

d = e + f   // 3
e = f + d   // 4
```

> 上面的代码，如果正常执行的话是一行行的往下执行，但是编译器看到 2 依赖 1，4 依赖 3，但是 1 并不依赖 3，所以编译后的结果可能是

```kt
b = a + c   // 1
d = e + f   // 3

c = a + b   // 2
e = f + d   // 4
```

- 这就叫***指令重排（Instruction Reorder）***，是编译器为了优化代码而进行的一种优化，**编译器可以对指令进行重排，使得程序的执行顺序与代码顺序不一致**

- 正常情况下这不是事，但是如果指令重排发生在多线程环境下？

- 假设这样一种情况，两个线程自己都有一份数据的备份再缓存上，因为不保证一定会写回或读取主内存，所以会导致可见性问题

```kt
data class Exchanger(
    var name: String?,
    var age: Int?
) {
    fun setExchanger(ex: Exchanger) {
        while (name == null || age == null) {
            // 不保证这里明明是空的，但是自己的内存拷贝是有东西的，导致最后两个线程的数据不统一
        }
        this.name = ex.name
        this.age = ex.age
    }

    fun getExchanger(): Exchanger {
        val result = Exchanger(name, age)
        this.name = null
        this.age = null
        return result
    }
}
```

- 解决办法是可以声明 `volatile`，保证写操作会写入主内存，读操作会使用主内存的

> 可以不声明所以的变量都为 `volatile`，**只要有一个 `volatile` 变量被读写，所有对这个线程可见的变量都会写入或读取到主内存**

```kt
class Message(var str: String?) {
    @Volatile
    var flag: Boolean = false
    
    fun setMeg(s: String) {
        str = s         // 1
        flag = true     // 2
    }
    
    fun getMeg(): String? {
        return if (flag) {
            str
        } else {
            null
        }
    }
}
```

- 问题是如果指令重排发生了，1 和 2 调换，2 的位置会被写入到主内存，但是 1 的位置可不一定，导致 2 之后的线程读取到的数据可能是 1 之前的，导致数据不一致

- 所以 Java 有一个***先行发生（happens-before guarantee）的概念，保证指令重排不会发生在有 `volatile` 和 `synchronized` 的地方***

- 所有**位于 `volatile` 变量读写之前的指令，都不会被重排到后面，位于 `volatile` 变量读写之后的指令，也不会被重排到前面**

```kt
class ValueExchanger {
    private var a = 0
    private var b = 0

    fun exchangeFrom(value: ValueExchanger) {
        // this.a = value.a
        synchronized(this) {
            this.a = value.a
            this.b = value.b
        }
        // this.b = value.b
        // 不会移出外面
    }
    
    fun exchangeTo(value: ValueExchanger) {
        synchronized(this) {
            value.a = this.a
            value.b = this.b
            // println("Success") 也不会发生
        }
        println("Success")
    }
}
```

- 所有**位于 `synchronized` 代码块里面的代码，都不会因为指令重排移到外面，位于 `synchronized` 代码块外面的代码，也不会因为指令重排移到里面**

> 说实话，这个 `volatile` 很多时候是替代不了 `synchronized` 的，它的优点是性能好一些，可能用的比较多的地方是线程安全的单例和禁止指令重排

```kt
class Singlaton {
    private var instance: Singlaton? = null

    fun getInstance(): Singlaton {
        if (instance == null) {
            synchronized(this::class) {
                if (instance == null) {
                    instance = Singlaton()
                }
            }
        }
        
        return instance!!
    }
}
```

### 12.6.5 竞争条件

> 本文不想去分辨静态条件（race condition）和数据竞争（data rece），因为在我看来分辨了也没用，感兴趣的可以自行了解

- 那我们这一节讲了这么多，就是为了一开始的一个问题，下面的输出并不是我们认为的那样

```kt
fun main() {
    val counter = Counter()
    val t1 = Thread {
        for (i in 1..100_0000) {
            counter.increment()
        }
    }

    val t2 = Thread {
        for (i in 1..100_0000) {
            counter.increment()
        }
    }

    t1.start()
    t2.start()

    t1.join()
    t2.join()

    println("Final count: ${counter.getResult()}")
}

class Counter {
    private var count = 0

    fun increment() { count++ }

    fun getResult() = count
}
```

- 通过前面的文章我们知道，这是两个线程不同的可见性和原子性操作导致的

- ***对于多个线程同时读写的情况，就会发生线程间的竞争，解决办法就是使用 `synchronized` 代码块锁住共享资源***

```kt
fun main() {
    val counter = Counter()
    val t1 = Thread {
        for (i in 1..100_0000) {
            counter.increment()
        }
    }

    val t2 = Thread {
        for (i in 1..100_0000) {
            counter.increment()
        }
    }

    t1.start()
    t2.start()

    t1.join()
    t2.join()

    println("Final count: ${counter.getResult()}")
}

class Counter {
    private var count = 0

    fun increment() {
        synchronized(this) {
            count++
        }
    }

    fun getResult() = count
}
```

- 但是***对于一个线程读，一个线程写，是不会发生竞争的***

```kt
fun main() {
    val counter = Counter()
    val t1 = Thread {
        for (i in 1..1_0000) {
            counter.increment()
        }
    }

    val t2 = Thread {
        for (i in 1..100) {
            Thread.sleep(1)
        }
        println("Count: ${counter.getResult()}")
    }

    t1.start()
    t2.start()
}

class Counter {
    private var count = 0

    fun increment() {
        count++
    }

    fun getResult() = count
}
```

> 这是因为常见的竞争发生在两个线程同时写入的时候互相覆盖，导致最后的结果不是期望的结果，但是单线程写入是没有问题的，可能唯一的问题是第二个读取的线程可能可见性有些问题，可以通过 `volatile` 关键字解决

- 两个线程，一读一写，一写一读，同样没问题

```kt
fun main() {
    val counter1 = Counter()
    val counter2 = Counter()

    val t1 = Thread(MyRunnable(counter1, counter2))
    val t2 = Thread(MyRunnable(counter2, counter1))

    t1.start()
    t2.start()

    t1.join()
    t2.join()

    println("Final count 1: ${counter1.getResult()}")
    println("Final count 2: ${counter2.getResult()}")
}

class MyRunnable(
    val writeCounter: Counter,
    val readCounter: Counter
) : Runnable {
    override fun run() {
        for (i in 1..10_0000) {
            writeCounter.increment()
            readCounter.getResult()
        }
    }
}

class Counter {
    private var count = 0

    fun increment() {
        count++
    }

    fun getResult() = count
}
```

### 12.6.6 多线程并发工具类

#### 12.6.6.1 Atomic 类

- Java 中的对象锁其实是有四种状态的，简单来说是：
    1. ***无锁状态，任何线程都可以访问***
    2. ***偏向锁状态，加锁解锁不会带来太多消耗，一般单个线程使用***
    3. ***轻量级锁状态，多个线程不断自旋试图获取锁***
    4. ***重量级锁状，多个线程竞争，会互相阻塞***
   
- 还有悲观锁和乐观锁的概念，***悲观锁指的是每一次都进行加锁，不管有几个线程，而乐观锁是假设没有冲突，每次不加锁，如果有冲突就使用一种叫 CAS（Compare-And-Swap） 的机制来保证线程安全***

- JDK 1.6 以前，`synchroized` 一直是重量锁，导致性能很差，***1.6 以后引入了四种锁状态，只有不断的锁升级才会到重量级***

- **所谓 CAS ，就是一种乐观锁的实现，他在读写值的时候不会加锁，但是在读写之前会先去存储对象的旧值，然后写入的时候比较下旧值和新值是否没变，如果变了，说明有线程在自己读写的过程中访问变量了，他就重新读值，然后再去比较，这也叫自旋（Spinning）**

- Java 为了兼顾性能和原子性可见性操作，为我们提供了 ***原子类，原子类的操作都是原子性（线程安全）*** 的，同时比 `synchroized` 性能好

- 先来看***原子基本类型，有 `AtomicBoolean` `AtomicInteger` `AtomicLong` 三种***，后两者支持算术运算

```java
// 常见操作

public final int get() // 获取当前值
public final int getAndSet(int newValue) // 获取当前值，并设置新值
public final int getAndIncrement()// 获取当前值，并自增
public final int getAndDecrement() // 获取当前值，并自减
public final int getAndAdd(int delta) // 获取当前值，并加上预期值
boolean compareAndSet(int expect, int update) // 如果输入值（update）等于预期值，将该值设置为输入值
public final void lazySet(int newValue) // 最终设置为 newValue，使用 lazySet 设置之后可能导致其他线程在之后的一小段时间内还是可以读到旧的值
```
```kt
import java.util.concurrent.atomic.AtomicInteger

fun main() {
    val atomic = AtomicInteger(0)

    val t1 = Thread {
        for (i in 1..100_0000) {
            atomic.incrementAndGet()
        }
    }

    val t2 = Thread {
        for (i in 1..100_0000) {
            atomic.incrementAndGet()
        }
    }

    t1.start()
    t2.start()

    t1.join()
    t2.join()

    println(atomic.get())
}
```

- 还有 ***引用类型 `AtomicReference` 仅维护对象引用，
`AtomicMarkableReference` 维护对象引用和一个布尔值标记，
`AtomicStampedReference` 维护对象引用和一个整数戳***

- ***`AtomicStampedReference` 就可以解决 CAS 中的 ABA 问题***

> ABA 是指在 CAS 的过程中，另外的线程把旧值改掉了，然后再把新值改回成旧值，虽然 CAS 会认为这个对象没有变，但其实是改变过的

> 要是不好理解的话，我们这么说，线程 T1 读取某个共享变量的值 A，T1 被挂起，线程 T2 将该变量的值从 A 修改为 B，然后又修改回 A，T1 恢复执行，并尝试使用 CAS 操作将变量从 A 修改为新值，CAS 操作成功，因为变量的当前值仍然是 A，但此时变量的状态已经发生了变化

```kt
import java.util.concurrent.atomic.AtomicStampedReference

fun main() {
    val initialRef = "A"
    val initialStamp = 0
    val atomicStampedRef: AtomicStampedReference<String?> = AtomicStampedReference(initialRef, initialStamp)

    // 模拟 ABA 问题
    val t1 = Thread {
        val reference = atomicStampedRef.getReference()
        val stamp = atomicStampedRef.getStamp()

        // 模拟线程挂起
        Thread.sleep(100)

        // 尝试将值从 A 修改为 C，并检查戳
        if (atomicStampedRef.compareAndSet(reference, "C", stamp, stamp + 1)) {
            println("Thread 1: Updated A to C")
        } else {
            println("Thread 1: Failed to update A to C")
        }
    }

    val t2 = Thread {
        // 模拟 ABA 操作
        Thread.sleep(50)
        atomicStampedRef.compareAndSet(atomicStampedRef.getReference(), "B", atomicStampedRef.getStamp(), atomicStampedRef.getStamp() + 1)
        println("Thread 2: Updated A to B")

        atomicStampedRef.compareAndSet(atomicStampedRef.getReference(), "A", atomicStampedRef.getStamp(), atomicStampedRef.getStamp() + 1)
        println("Thread 2: Updated B to A")
    }

    t1.start()
    t2.start()

    t1.join()
    t2.join()

    println("Final reference: ${atomicStampedRef.getReference()}, Final stamp: ${atomicStampedRef.getStamp()}")
}
```

- 还有***原子数组类型***，相比普通的原子基本类型，***他们还保证自己元素的原子性而不仅仅是引用的原子性，有 `AtomicIntegerArray` `AtomicLongArray` `AtmoicReferenceArray` 三种***

- 还有三个用于更新字段的原子类型，`AtomicIntegerFieldUpdater` `AtmoicLongFieldUpdater` `AtomicRefrenceFieldUpdater` ，基于反射实现，限制如下：
    1. 因为对象的属性修改类型原子类都是抽象类，所以每次使用都必须使用静态方法 newUpdater() 创建一个更新器，并且需要设置想要更新的类和属性
    2. 字段必须是 `volatile` 类型的
    3. 不能作用于静态变量
    4. 不能作用于常量

#### 12.6.6.2 并发集合

- Java 为我们提供了线程安全的并发集合，有 `ConcurrentHashMap` `ConcurrentLinkedQueue` `CopyOnWriteArrayList` 等等，这些集合都实现了 `java.util.Collection` 接口，并且都提供了线程安全的操作，包括 `add` `remove` `contains` `size` 等等

```kt
import java.util.concurrent.ConcurrentHashMap

fun main() {
    val sharedMap = ConcurrentHashMap<String, String>()

    val t1 = Thread(MyRunnable(sharedMap))
    val t2 = Thread(MyRunnable(sharedMap))

    t1.start()
    t2.start()
}

class MyRunnable(val sharedMap: ConcurrentHashMap<String, String>) : Runnable {
    override fun run() {
        for (i in 1..100_0000) {
            if (sharedMap.containsKey("key")) {
                val str = sharedMap.remove("key")
                // 这里如果 map 检测到有两个线程访问自己，这个值就会是 null
                if (str == null) {
                    println("Iterator $i key was null")
                }
            }
            sharedMap["key"] = "value$i"
        }
    }
}
```

### 12.6.7 Lock 接口

- Java 还提供了 `Lock` 接口，相比 `synchroized` 这是一个 API，提供了一些更高级的功能和方法

- ***`Lock` 的常用实现类是 `RentrantLock`，这是一个可重入锁，也就是一个线程在加锁的情况下可以再次加锁，想要释放锁只有把自己都加过的锁释放了才行***

- ***在 `Lock` 对象上使用 `lock()` 方法即可加锁，其他线程无法访问，而使用 `unlock()` 即可释放锁，需要注意的是建议把 `lock` 放进 `try finally` 里面，以保证发生异常也可以捕捉并正常释放锁***

> **`unlock` 放在 `finally` 里面，但是 `lock` 放在 `try` 里面的第一行或是放在外面的第一行应该都是可以的**，保证他是第一个就行

```kt
import java.util.concurrent.locks.ReentrantLock

fun main() {
    val counter = Counter()

    val t1 = Thread {
        for (i in 1..100_0000) {
            counter.increment()
        }
    }

    val t2 = Thread {
        for (i in 1..100_0000) {
            counter.increment()
        }
    }


    t1.start()
    t2.start()
    
    t1.join()
    t2.join()

    println("Final count: ${counter.get()}")
}

class Counter {
    private var count = 0
    private val lock = ReentrantLock()
    // private val lock = ReentrantLock(true)
    // 这里的参数可以是布尔值，表示公平锁与否，公平锁意为先来先服务，非公平锁则是按照请求的顺序来处理。默认为非公平锁

    fun increment() {
        try {
            lock.lock()
            count++
        } finally {
            lock.unlock()
        }
    }

    fun get() = count
}
```

- 以下是 `ReentrantLock` 的常用方法

```kt
lock.tryLock()
// 尝试获取锁
// 尝试获取锁，如果锁可用则返回 true，否则返回 false。此方法不会阻塞

lock.tryLock(long time, TimeUnit unit)
// 带超时的尝试获取锁
// 尝试在给定的时间内获取锁，如果在指定时间内锁可用则返回 true，否则返回 false。此方法会阻塞，但有时间限制

lock.lockInterruptibly()
// 可中断的获取锁
// 获取锁，除非当前线程被中断。如果锁可用，则获取锁并立即返回；如果锁不可用，则当前线程将阻塞，直到锁可用或被中断

lock.holdCount
// 获取持有次数
// 查询当前线程持有此锁的次数

lock.isHeldByCurrentThread
// 判断当前线程是否持有锁
// 查询当前线程是否持有此锁

lock.isLocked
// 判断锁是否被任意线程持有
// 查询此锁是否由任何线程持有

lock.isFair
// 判断锁是否为公平锁 
// 查询此锁是否为公平锁
```

- 就像 `synchroized` 的 `wait` `notify` 一样，***`Lock` 也有 `Condition` 接口，可以用来实现等待/通知机制，`Condition` 接口有 `await` `signal` `signalAll` 三个方法，分别表示等待、通知和通知所有线程***，不一样的是它可以实现手动选择唤醒，而不是 `notify()` 的随机唤醒
  
- ***使用 `newCondition()` 创建一个监视者，`await` `signal` `signalAll` 必须在 `lock()` 和 `unlock()` 之间使用，调用 `await()` 会释放锁，并且终止下面代码的执行进入等待队列，调用 `signal()` 唤醒一个等待线程，调用 `signalAll()` 唤醒所有等待线程，不同的监视者对象可以唤醒不同的线程***

```kt
import java.util.concurrent.locks.Condition
import java.util.concurrent.locks.Lock
import java.util.concurrent.locks.ReentrantLock

fun main() {
    val buffer = BoundedBuffer()

    // 生产者线程
    val producer = Thread {
        for (i in 1..10) {
            buffer.put("Item $i")
            Thread.sleep(100) // 模拟生产时间
        }
    }

    // 消费者线程
    val consumer = Thread {
        for (i in 1..10) {
            buffer.take()
            Thread.sleep(150) // 模拟消费时间
        }
    }

    producer.start()
    consumer.start()

    producer.join()
    consumer.join()
}

class BoundedBuffer {
    private val lock: Lock = ReentrantLock() // 创建一个可重入锁
    private val notFull: Condition = lock.newCondition() // 创建一个表示“不满”的条件
    private val notEmpty: Condition = lock.newCondition() // 创建一个表示“不空”的条件

    private val buffer = mutableListOf<String>() // 缓冲区
    private val maxSize = 5 // 缓冲区最大容量

    // 生产者方法：向缓冲区添加元素
    fun put(item: String) {
        lock.lock() // 获取锁
        try {
            while (buffer.size == maxSize) {
                println("Buffer is full, waiting...")
                notFull.await() // 如果缓冲区满，则等待
            }
            buffer.add(item) // 添加元素到缓冲区
            println("Produced: $item")
            notEmpty.signal() // 唤醒一个等待的消费者线程
        } catch (e: InterruptedException) {
            Thread.currentThread().interrupt()
        } finally {
            lock.unlock() // 释放锁
        }
    }

    // 消费者方法：从缓冲区移除元素
    fun take(): String {
        lock.lock() // 获取锁
        return try {
            while (buffer.isEmpty()) {
                println("Buffer is empty, waiting...")
                notEmpty.await() // 如果缓冲区空，则等待
            }
            val item = buffer.removeAt(0) // 移除并获取元素
            println("Consumed: $item")
            notFull.signal() // 唤醒一个等待的生产者线程
            item
        } catch (e: InterruptedException) {
            Thread.currentThread().interrupt()
            ""
        } finally {
            lock.unlock() // 释放锁
        }
    }
}
```

- `synchronized` 和 `lock` 有什么区别你？
    1. `synchronized` 只能修饰一个方法，而 `lock` 可以在不同的函数里调用
    2. `lock` 也拥有跟 `synchronized` 相同的 `happens before guarantee`
    3. `synchronized` 永远是可重入的，而 `lock` 是可以实现一个不可重入的实现类的
    4. `synchronized` 无法保证公平不公平锁，而 `lock` 可以
   
### 12.6.8 线程死锁

- ***如果两个线程同时想要别的资源，可是自己锁着别人的资源，自己又不释放，所以同步控制时请杜绝线程死锁***

```kt
fun main() {
    // 创建两个对象，作为锁
    val lock1 = Object()
    val lock2 = Object()

    // 线程1：先获取 lock1，然后尝试获取 lock2
    val thread1 = Thread {
        synchronized(lock1) {
            println("Thread 1 acquired lock1")
            Thread.sleep(100) // 模拟一些工作
            synchronized(lock2) {
                println("Thread 1 acquired lock2")
                // 这里不会被执行，因为线程2已经持有了 lock2
            }
        }
    }

    // 线程2：先获取 lock2，然后尝试获取 lock1
    val thread2 = Thread {
        synchronized(lock2) {
            println("Thread 2 acquired lock2")
            Thread.sleep(100) // 模拟一些工作
            synchronized(lock1) {
                println("Thread 2 acquired lock1")
                // 这里不会被执行，因为线程1已经持有了 lock1
            }
        }
    }

    // 启动两个线程
    thread1.start()
    thread2.start()

    // 等待两个线程结束
    thread1.join()
    thread2.join()

    println("Main thread finished")
    // 永远不会被打印
}
```

- 上文的这个例子是最简单的死锁，只需要交换下上锁的顺序就能解决，实际上还有很多种复杂的死锁情况，需要我们多加注意

> 介绍一个方便的工具：`jconsole`，如果配置了 JDK 可以直接在命令行打开，位于 `JDK/bin` 下面，可以很方便的查看线程运行情况，类加载和线程是否死锁

## 12.7 线程池

> 因为一个线程死亡后就无法再次利用，如果要使用很多的线程，就只能一个一个的新建，这样不方便管理，并且连续的线程启动和结束很耗内存，有没有办法可以再次利用线程呢？

- Java 为我们提供了***线程池（Thread Pool），这是一个方便集中管理、复用线程的线程框架***，通过使用线程池，我们**指定的任务只会在限定的线程内执行，每一个线程可以执行很多个任务**，相比新建线程来说大大方便了使用

```mermaid
---
title: Java Thread Pool
---
flowchart
    subgraph Thread Pool
        direction TB
        subgraph BlockingQueue
            Task5
            Task4
            Task3
            Task2
            Task1
        end
        Thread1 --> Task1
        Thread2 --> Task2
        Thread3 --> Task3
    end
```

- 通过**线程池的方式，向一个任务队列提交你要执行的任务，线程池里的线程各自领取任务并执行**，线程池主要是使用 Java `java.util.concurrent` 下面的 `Executor` 和它的实现类来实现的

```kt
import java.util.concurrent.Executors

fun main() {
    val threadPool = Executors.newFixedThreadPool(4)
}
```

- **`Executors` 接口和它的实现类继承图如下**：

```mermaid
---
title: Java Executors
---
classDiagram
    class Executor
    <<interface>> Executor
    class ExecutorService
    <<interface>> ExecutorService
    class ThreadPoolExecutor
    class AbstractExecutorService
    <<abstract>> AbstractExecutorService
    class ScheduledExecutorService
    <<interface>> ScheduledExecutorService
    class ScheduledThreadPoolExecutor
    Executor <|-- ExecutorService
    ExecutorService <|-- AbstractExecutorService
    AbstractExecutorService <|-- ThreadPoolExecutor
    ExecutorService <|-- ScheduledExecutorService
    ScheduledExecutorService <|-- ScheduledThreadPoolExecutor
    ThreadPoolExecutor <|-- ScheduledThreadPoolExecutor
```

- **创建一个线程池，可以使用 `ThreadPoolExecutor` 的构造方法**，它的参数如下

```kt
import java.util.concurrent.ArrayBlockingQueue
import java.util.concurrent.ThreadPoolExecutor
import java.util.concurrent.TimeUnit

fun main() {
    val corePoolSize = 10
    // 线程池的核心线程数
    val maximumPoolSize = 20
    // 线程池的最大线程数，如果任务较多可以新增这些数量的线程用于处理
    val keepAliveTime = 3L
    // 最大线程空闲后的存活时间，如果多生成的线程空闲时间超过这个值，线程会被回收
    val timeUnit = TimeUnit.SECONDS
    // 时间单位，指定上一个参数的单位
    val workQueue = ArrayBlockingQueue<Runnable>(128)
    // 任务队列，用于存放等待执行的任务，有多种实现，这里使用的是 `ArrayBlockingQueue`，更多内容可以看 `https://blog.csdn.net/xiaojin21cen/article/details/87363143`

    val threadPool = ThreadPoolExecutor(
        corePoolSize,
        maximumPoolSize,
        keepAliveTime,
        timeUnit,
        workQueue
    )

    threadPool.execute(MyRunnable("Task - 1"))
    threadPool.execute(MyRunnable("Task - 2"))
    threadPool.execute(MyRunnable("Task - 3"))

    threadPool.shutdown()
}

class MyRunnable(val str: String) : Runnable {
    override fun run() {
        println("${Thread.currentThread().name} - $str")
    }
}
```

- 除了使用 `ThreadPoolExecutor`，还有 **`Executors` 的工厂方法 `newFixedThreadPool` `newSingleThreadExecutor`**，前者生成了一个指定线程（corePoolSize 和 maximumPoolSize）的线程池，后者生成了一个单线程的线程

```kt
import java.util.concurrent.Executors
import java.util.concurrent.ThreadPoolExecutor

fun main() {
    val threadPool = Executors.newFixedThreadPool(1) as ThreadPoolExecutor
    //val threadPool = Executors.newSingleThreadExecutor()
    // 这二者的效果都是单线程的

    threadPool.execute(MyRunnable("Task - 1"))
    threadPool.execute(MyRunnable("Task - 2"))
    threadPool.execute(MyRunnable("Task - 3"))

    threadPool.shutdown()
}

class MyRunnable(val str: String) : Runnable {
    override fun run() {
        println("${Thread.currentThread().name} - $str")
    }
}
```

- 还有 ***`ScheduledThreadPoolExecutor` 类，与上面区别是它可以指定任务的执行时间或间隔，而 `ThreadPoolExecutor` 则会尽可能立即执行***，这里先介绍后者

- ***`shotdown()` 方法用于关闭线程池***，如果线程池里的线程还没执行完任务，则会等待线程池里的线程执行完任务，再关闭线程池

> 还有 `shutdownNow()`

- ***使用线程池的 `excute` 方法，参数为 `Runnable` 对象，可以向线程池提交任务***，任务的执行和线程池里的线程没有直接关系

- 还有一个 ***`submit` 方法，也可以接受 `Runnalbe` 对象，但是会返回一个 `Future` 对象，可以用来获取任务的执行结果***，`Future` 对象有 `cancel` `isCancelled` `isDone` `get` `get(long timeout, TimeUnit unit)` 方法，可以对任务进行取消、判断是否完成、获取执行结果，也可以设置超时取消时间

```kt
import java.util.concurrent.ExecutionException
import java.util.concurrent.Executors
import java.util.concurrent.Future


fun main() {
    val threadPool = Executors.newSingleThreadExecutor()

    val future: Future<*> = threadPool.submit(MyRunnable("Task - 1"))

    println(future.isDone())

    try {
        println(future.get())
        // get 能获取任务的返回值，并且获取不到的话会一直阻塞的等待，但是 Runnable 里的 run 方法没有返回值，所以这里是 null
    }
    catch (e: InterruptedException) {
    }
    catch (e: ExecutionException) {
    }

    println(future.isDone())

    threadPool.shutdown()
}

class MyRunnable(val str: String) : Runnable {
    override fun run() {
        println("${Thread.currentThread().name} - $str")
    }
}
```

- 跟 `Runnable` 相对的还有一个 ***`Callable` 接口，它的 `call()` 方法可以返回值***，因此也可以作为参数传递给 `submit()` 方法获取 `Future`

```kt
import java.util.concurrent.Callable
import java.util.concurrent.ExecutionException
import java.util.concurrent.Executors
import java.util.concurrent.Future


fun main() {
    val threadPool = Executors.newSingleThreadExecutor()

    val future: Future<*> = threadPool.submit(MyCallable("Task - 1"))

    println(future.isDone())

    try {
        println(future.get())
    }
    catch (e: InterruptedException) {
    }
    catch (e: ExecutionException) {
    }

    println(future.isDone())

    threadPool.shutdown()
}

class MyCallable(val str: String) : Callable<String> {
    override fun call(): String = "${Thread.currentThread().name} - $str"

    // Callable 方法是泛型的，这里只是省事，实际上可以返回任何类型的值
}

/**
 * ```java
 * public interface Callable<V> {
 *     V call() throws Exception;
 * }
 * ```
 */
```

> 本来这一章还是打算继续写下去的，奈何了，唉，推荐大家可以看一下这位的视频 [Java concurrency and multithreading](https://www.youtube.com/watch?v=mTGdtC9f4EU&list=PLL8woMHwr36EDxjUoCzboZjedsnhLP1j4&pp=iAQB) ，来自 [Jakob Jenkov](https://jenkov.com/)，该讲的都讲了，而且逻辑图很清晰

## 12.8 协程

> 讲了一大堆 Java 的东西，是时候讲一下 Kotlin 的东西了，协程

> 其实 Java 也有这个概念，叫虚拟线程（Virtual Threaded）或者叫轻量级线程（Lightweight Thread），Kotlin 里面的协程不是什么高级的东西，本质上就是一个轻量的线程框架，就是比 Java 的那个方便了些，在逻辑层面并不是什么很高深的东西，这一点请大家记住

> 因此理解协程，用线程的方式最好，不要给自己套上几层迷雾

### 12.8.1 概念

> 待办，crossinline 的另一个用法，线程间间接调用 return ；协程里的异常处理



# 第十三章：其他相关

## 13.0 前文的一些补充

### 13.0.1 空安全

- 当最开始的时候，我就说过 Kotlin 的空安全，在 Kotlin 里面只有以下几种情况会发生 `NullPointerException`

    1. `throw NullPointerException`
    2. `!!`
    3. 父类初始化里调用了可以被继承的成员
    4. 泄露的 `this`
    5. 与 Java 互操作访问了空对象

### 13.0.2 字符串

## 13.1 注解

## 13.2 和 Java 互操作

## 13.3 标准库

### 13.3.1 IO

### 13.3.2 时间
