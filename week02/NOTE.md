# 第二周总结
## 编程语言通识
### 语言的分类
语言根据语法分为非形式语言（自然语言）和形式语言（社会科学用的语言）
- 非形式语言：个人理解为自然语言，如中文，英文等
- 形式语言（Formal Language）：个人理解为计算机或者数学等使用的语言，比如编程语言，数学公式语言。

#### 图灵机
图灵机是英国数学家 Alan Mathison Turing 抽象的一种数学逻辑机。通过将人类所有的计算行为简化为两个步骤，来模拟人类全部的计算过程和结果
1. 在纸上书写或者擦除一个符号
2. 将注意力从纸的一个位置转移到另外一个位置  

在这个过程中，人的任何下一步行为均由两个因素决定：
- 人当前关注的符号
- 人当前的思维

#### 形式语言
Avram Noam Chomsky的谱系是计算机科学中刻画形式文法表达能力的一个分类谱系，包括四个层次
#####  0型文法（无限制文法或者短语结构文法）：
- 包含所有可以被图灵机识别的语法
- 识别的意思是可以使图灵机停机，即计算为有限步骤。这类语言又被称为递归可枚举语言

##### 1型文法（上下文相关文法）：
- 不同的上下文表示不同的意思

##### 2型文法（上下文无关文法）：
- 表示的意思和放的位置无关

##### 3型文法（正则文法）：
- 严格按照正则表示的语法

> 正则语言类包含于上下文无关语言类，上下文无关语言类包含于上下文相关语言类，上下文相关语言类包含于递归可枚举语言类。这里的包含都是集合的真包含关系，也就是说：存在递归可枚举语言不属于上下文相关语言类，存在上下文相关语言不属于上下文无关语言类，存在上下文无关语言不属于正则语言类。

#### BNF产生式
巴科斯范式（英语：Backus Normal Form，缩写为 BNF），是一种用于表示上下文无关文法的语言  
形式： <复合结构>::=<单一结构>
> <句子>::=<主语><谓语><宾语>    
// 左边的<句子>是复合结构，由三种单一结构组成，分别是<主语> <谓语> <宾语>    

| 表示或
> <代词>::=<我>|<你>|<他>  
// 代词由我你他三者当中的任意一者组成

 \* 表示重复
> <结巴>::=<我>*  
// 结巴说话，说了很多的我

\+ 表示至少一次
> <坐火车>::=<买票>+  
// 坐火车至少买一次票

单一结构叫终结符，用引号和中间的字符表示
> <句子>::="我"|"你"|"他"

练习：若一门语言包含"a"，"b"则：
> <Program>::="a"+ | "b"+  
// program 由 至少一个a或者至少一个b组成，但是不能表示由ab混合组成，通过递归表示由ab混合组成  

> <Program>::="a"+ | "b"+
<Program>::=<Program> "a"+ | <Program> "b"+

练习：定义加法
1. 定义一个数字<Number>::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"
2. 定义一个十进制数<DecimalNumber>::= "0" | (("1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9") <Number>*)
3. 定义一个加法<Expression>::= <DecimalNumber> "+" <DecimalNumber>
4. 定义一个连加<AdditionExpression>::=<Expression> "+" <DecimalNumber>
5. 合并上式：<AdditionExpression>::=(<AdditionExpression> "+" <DecimalNumber>) | <DecimalNumber>

练习：定义四则运算
1. 定义乘除法表达式<MultiplicativeExpression>::= <MultiplicativeExpression> "*" <DecimalNumber> | <DecimalNumber> | <MultiplicativeExpression> "/" <DecimalNumber>
2. 定义加减法表达式：<AdditionExpression>::= <MultiplicativeExpression> | (<AdditionExpression> "+" <MultiplicativeExpression>) | (<AdditionExpression> "-" <MultiplicativeExpression>)  

==3. <LogcalExpression> = <AdditionExpression> | <LogcalExpression> "||" <AdditionExpression> | <LogcalExpression> "&&" <AdditionExpression>==


## 作业
#### 1： 写一个正则表达式 匹配所有 Number 直接量

```
/^(\.\d+|(0|[1-9]\d*)\.?\d*?)([eE][-\+]?\d+)?$|^0[bB][01]+$|^0[oO][0-7]+$|^0[xX][0-9a-fA-F]+$/
```
#### 2： 写一个 UTF-8 Encoding 的函数

```
function utf8Encoding(str) {
    return str.split('').map((s) => `\\u${s.charCodeAt().toString(16)}`).join('');
}
```

#### 3： 写一个正则表达式，匹配所有的字符串直接量，单引号和双引号

```
/^['"\\bfnrtv/dxu]$|^u[0-9a-fA-F]{4}$|^u(10|0?[0-9a-fA-F])[0-9a-fA-F]{0,4}$/
```

