---
layout: blog 
istop: true
lasted: true
code: true
title: "形式化方法课程中章节总结、知识点"
background-image: "../img/2017-11-10.jpg"
date: 2017-11-10 20:26:00
category: 形式化方法 
tags: 
- 形式化方法
- 软件工程
- 形式化方法相关知识点
- 总结
---

# 形式化方法课程知识点分章节总结

# 前言

>  - 集合相关理论
>  - 对数学逻辑基本的理解

## 目标

- 学习使用最广泛的形式化表达方式  
- 掌握形式化语言
- 对形式化验证方法有基本的了解
- 对于什么问题可以用形式化方法解决有一个大致的概念

## 形式化描述和验证

### 内容

- 集合理论和数学逻辑（经典命题演算和经典谓词、微积分）
- Z语言

# 1.介绍

## 1.1 软件工程的主要目标

- 开发更可靠的系统

## 1.2 形式化方法

- 数学化的语言，技术和工具
- 用来制定和验证系统
- 目标：帮助软件工程师开发更可靠的系统

## 1.2.1 一种检查整个状态空间的平均值设计（硬件或者软件）

- 对于所有可能的输入建立一个正确的安全的属性

## 1.2.2 在开发过程中形式化方法可以应用不同的地方

## 1.2.3 提前制定规范的优点

- 一个规范的定义时一个开发过程的起点
- 改变一个定义好的规范比改变已经实现的系统付出的代价要小得多
- 即使开发已经完成，定义好的规范也是非常有用的，因为维护一个没有规范的系统是非常困难的。要想修改一程序，首相必须要知道它时做什么用。

## 1.2.4 规范的验证

- 检查一个规范是否满足用户提出的需求的过程叫做验证（validation）。  
- 验证基本上包括说明规范的属性，并说明规范满足这些属性。描述的属性越多，我们对规范有效性的信心就越高。
- 验证是一个经验的过程。规范一直被认为是有效的，知道被找到一个不满足的属性。


必须能够以某种方式证明实现满足系统的规范，以显示对系统用户的信任。

## 1.3 形式化方法 

- 逐步细化规范直到被实现
- 如果每次细化的规范都能被数学方法证明时满足规范的，我们称这样的开发过程是规范（normal）。

## 1.3.1 非正式的测试方法

- 首先要实现规范，然后进行测试。测试用例来自于规范。

## 1.3.2 正式符号和非正式符号

- 一个符号如果有语法(syntax)和语意(semantics)就是正式符号
- 如果一个符号只有语法，那么它就是非正式符号

# 1.4 集合的相关概念

- 子集于超集

    - 子集： 如果集合A的任意一个元素都是集合B的元素，那么集合A称为集合B的子集。
    - 超集：如果一个集合S2中的每一个元素都在集合S1中，且集合S1中可能包含S2中没有的元素，则集合S1就是S2的一个超集。

    > A集合如果是B集合的子集，那么B集合就是A集合的 超集。

- 集合中的元素也可以是一个集合

- 集合的基数：集合中不同元素的个数

- 集合的几个操作，以及操作符，交集、并集

- 互斥，两个集合没有任何相同的元素

- 集合差，A-B，意思为，属于A集合且不属于B集合的元素组成的集合。

- 集合的补集。

- 集合的对称差分，即A、B集的并集的元素除去交集的元素之后组成的元素。

- 集合的幂集：就是原集合的所有的子集构成的集合。
    > 如果原集合有k个元素，则它的幂集的元素个数为k的2次方

- 集合的笛卡儿积(cartesian product)：A×B＝ {(x,y)|x∈A ∧ y∈B}

- 集合的二元关系定义(binary relation)

- 集合的关系
    - 逆
    - 反
    - 恒等
    - n 元关系

- 集合关系的自反性
     例如：the relation ≥ :≡ {(a,b) | a≥b} is reflexive.

- 对称性和反对称性(Symmetry & Antisymmetry)
    - 例如：is married to 是对称的，likes不是对称的
    - 例如：＜是反对称的

- 传递性(transitivity)

- 等效关系(equivalence relation)

- 次序关系(order relation)

- 选择公理(axiom of choice)/AC

- f(A -> B)：f(x) = y，x属于B，y属于A。

# 2. Z 语言

## 2.1 类型/types

### 2.1.1 
- 内置类型，Interger，整数类型。
    - 使用整数类型时不需要引入
    - 操作符有：+，-，*，div，mod
- Natural，是Integer的子集，元素是非负数
    - N1不包括0的自然数
- 数量关系，＝，≠，＜，＞，≤，≥

### 2.1.2 基本类型

- 定义 ，例如： [PERSON] the set of all persons
- free type.  
    - freeType::= element1|element2|...element n

## 2.2 Z语言中的变量

- 每个变量名必须声明变量值
- 必须被引入并且所引用的值类型必须被声明
- v:类型，读作“v是一组type类型的值”或者“v是属于type类型”或者“v是TPYE类型”
- 例如： chauffeur：PERSON，  标明司机的类型是人。

## 2.3 Z 语言中的集合（set）

- 一个集合的值可以通过在括号内(花括号)中列出它的值来编写。
- 要对成员进行测试的值必须是该集合的底层类型的一个元素，否则，测试既不是真也不是假的，而是非法的。
- 集合中的元素的数量称为其大小(基数)，并由散列符号表示。例如：# ○/ = 0.
- 幂集。写作PS。例如：#PS = 2 #s
- 两个集合的相除在于包含了第一个集合中没有在第二个集合中的所有元素的集合。S\T，在S中且不在T中的元素组成的集合。
- 集合的并集（union）是包含至少在一个组件集中出现的那些元素的集合。
- 集合的交集（intersection）是包含在两个集合中的元素组成的集合。

##  2.4 例子，描述飞机上的乘客

情景: 乘客登机  
约束条件：没有座位号，先到先得，固定的容量  
假设：可以唯一性的识别不同的人
基本类型：[PERSON] the set of all possible uniquely identified persons 
变量：cacpacity：N the seating capacity of the aircraft  
    onboard:P PERSON the state of the aircraft system  
不变关系：#onboa ≤ capacity  
初始化操作：onboard' = 空集（○/）  
登机操作：
> p: PERSON
> p≮ （不属于）onboard
> /#onboard < capacity
> onboard' =  onboard ∪ {p}  

下机操作：  
> p:PERSON
> p 属于 onboard
> onboard' = onboard \ {p}  

查询：  
- 登机数量
> numOnboard: N
> numOnboard = #onboard
> onboard' = onboard

- 飞机上的人
> RESPONSE::= yes|no
> p:PERSON
> reply:RESPONSE
> ((p属于onboard and reply = yes) or (p不属于onboard and reply = no))
> onboard ' = onboard
> RESPONSE :: = OK | twoErrors | onBoard | full | notOnBoard  

Onboard operation
> p:PERSON
> reply: RESPONSE
> (p不属于onboard 且 #onboard < capacity 且 onboard'=onboad ∪ {p} 且 reply = OK)
> 并
> (p 属于 onboard 且 # onboard = capacity 且
> onboard’ = onboard 且 reply = twoErrors)
> 并
> (p 属于 onboard 且 # onboard < capacity 且
> onboard’ = onboard 且 reply = onBoard)
> 并
> (p 不属于 onboard 且 # onboard = capacity 且
> onboard’ = onboard 且 reply = full)  

Disembark operation
> p: PERSON
> reply: RESPONSE
> (p 属于 onboard 且 onboard’ = onboard \ {p} 且
> reply = OK)
> 并
> (p 不属于 onboard 且  onboard’ = onboard 并
> reply = notOnBoard)


## 2.5  结构

### 2.5.1 结构的一般形式

+---------结构名字------------------
|
|         变量生明
|
+----------------------------------
|
|         谓词关系
|
+----------------------------------  

- 每一行声明都被认为是被分号终止的。
- 一个序列由多行组成
- 剩下几行是由生明和谓词一起构成的
- 结构可以省略结构体的名字
- 没有谓词部分的模式仅声明一个新的变量或变量，而不需要应用约束谓词。
- 由模式引入的变量是该模式的局部变量，并且可能仅通过显式地包含变量s定义模式来引用另一个模式。
- 全局变量

### 2.5.2 结构的运算

- 模式可以被看作是单元，并由与逻辑运算符类似的各种操作符操作。
- 结构操作符包括：
    - Decoration
        - 用素数修饰的模式名被定义为与模式S相同，它的所有变量都是用素数装饰的。
        - 它用于表示在执行某些操作之后结构的值。
    - Inclusion 包含
        - 模式S的名称可以包含在另一个模式的声明中。其作用是对包含的模式进行文本导入:其声明与包含模式的内容合并，其断言部分与包含模式的内容相结合。
    - Conjunction联合
        - 两个模式和T可以由一个模式连接操作符连接起来，就像逻辑连接操作符一样。其效果是，通过合并两个结构模式的声明和它们的运算连接，来创建一个新的结构。
    - Disjunction分离
        - 两个模式S和T可以由一个模式析取操作符连接起来，就像逻辑分离操作符一样。其效果是使用合并的两个组件模式的声明和它们的谓词分离，从而创建一个新的模式。
    - Delta convention
        - 说明结构做了某种运算，△
    - Xi convention xi公约
        - 带有希腊字符capital xi()的模式作为其名称的第一个字符，如 ≡S，定义为与S相同，但是有一个约束，即每个变量的新值都与旧的值相同
    - Renaming重命名
        - newSchemaName == oldSchemaName[newName1/oldName1,newName2/oldname2,...]
        - 例如：T==S[c/b]
    - Hiding隐藏
        - 模式隐藏操作符隐藏了指定的变量，使它们不再是模式的变量，而是成为模式谓词部分中存在操作符的局部变量
        - newSchemaName == oldSchemaName \ (varName1, varName2, …)
    - Projection投射
        - 模式投影类似于隐藏，但除了括号中的变量名其余的所有的命名变量都是隐藏的。
        - newSchemaName == oldSchemaName ↑ (varName1, varName2, …)
    - Composition合成
        - 与模式T的模式S的组成被写成S;T表示先执行S，然后执行T。
        - 它等价于将描述S的后状态的变量重新命名为一些临时名称，以及用相同的临时名称描述T之前状态的等价变量，然后隐藏这些临时名称。
        - 例如：
            - PressRight == CursorControlKey [key?: KEY | key? = right]
            - PressRight ; PressLeft ==(PressRight [tempCol/column’, tempLine/line’ ]且PressLeft [tempCol/colimn, tempLine/line]) \ (tempCol, tempLine)
### 2.5.3 输入输出变量

- 输入变量：用问号(?)来结束变量s名，表示该变量是系统的输入。
- 输出变量：用感叹号(！)完成变量s名，表示变量是模式的输出。（在变量后边加）

### 2.5.4 注意

Z规范文档由Z表示法中的数学文本组成，用自然语言进行解释性文本。解释性文本应以问题的形式表达，不应直接引用数学公式。

# 3. 逻辑

## 3.1 概念

- 逻辑处理的是，什么是什么，目的是确定一个给定的前提的正确结论。例如，确定哪些参数是有效的
- 这是一种评估各种论证的规范性科学。
- 人们认为，数学逻辑主要是在正式思维中进行，这是一种常见的误解。重要的一点是要精确地定义正式的概念，从而能够用数学的方法来解释正式的系统。个i他这为数学增加了一个新的维度。