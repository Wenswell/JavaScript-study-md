# 简介

## 手册与规范

1. **ECMA-262 规范** 确地定义了Java这门语言。

2. **MDN（Mozilla）JavaScript 索引** 是一个获取关于个别语言函数、方法等深入信息的很好的信息来源。

3. **兼容性表** eg.[每个功能的支持表](http://caniuse.com)

## 代码编辑器

1. **IDE**(Integrated development environment)

2. **轻量编辑器**

# JavaScript 基础知识

> *JavaScript 是一门动态类型、面向对象的脚本 (Script) 语言。*

## 引入/使用 JavaScript

1. 内嵌脚本: 使用 `<script>` 标签在 **HTML** 中插入 JavaScript 程序

```html {.line-numbers}
<script>
        alert("Hello World");
</script>
```

2. 外部脚本: 在 `<script>` 中通过 `src` attribute(特性) 引入 JS 文件

- **注意**: 如果设置了 src 特性，script 标签内容将会被忽略

```html {.line-numbers}
<script src="./01.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.11/lodash.js"></script>
```

## 代码结构

### 语句

> *语句是执行行为（action）的语法结构和命令。*

1. 语句之间可以使用分号进行分割

2. (不建议) 存在换行符（line break）时，大多数情况下可以省略分号

### 现代模式，"use strict"

> 2009 年 ECMAScript 5 (ES5) 出现。ES5 规范增加了新的语言特性并且 *修改了一些已经存在的特性* 。

1. "use strict"处于脚本文件/函数体的 **最顶部** 时，整个脚本文件/函数都将以“现代”模式进行工作。

2. 没有办法取消 use strict , **没有** 指令可以使程序返回默认模式。

3. 浏览器开发者控制台运行代码时，默认不启动 use strict 。

### 变量 let aVariable = "UserName"

> 变量 是数据的“命名存储”。

1. 可以在一行中声明多个变量

2. 一个变量应该只被声明一次。(重复声明会触发 error)

### 变量命名

1. 变量名称必须仅包含 字母，数字，符号 $ 和 _

2. 首字符必须非数字

3. *区分大小写*

4. 驼峰式命名法（camelCase）

5. 保留字无法用作变量命名

6. use strict 下, 赋值前 *必须先声明*

### 常量 const aConstant = 3.14

1. 使用 const 声明的变量称为“常量/Constant”

2. 常量不能被修改，否则报错

3. **const命名** 
    - 小写适合计算出来的值
    - 大写适合/仅用作 “硬编码(hard-coded)” 值 (执行之前就已知)
    - eg. 
        ```javascript {.line-numbers}
        const COLOR_ORANGE = "#FF7F00";
        let color = COLOR_ORANGE;
        ```

## 数据类型

> *JavaScript 有 8 种基本的数据类型（7 种原始类型 `Number、String、Boolean、Null、undefined、symbol、bigInt`, 1 种引用类型 [`object`](##object) ）*

- JS 属于 “动态类型”（dynamically typed）编程语言: 定义的变量并不会在定义后被限制为某一数据类型
    ```javascript {.line-numbers}
    num1 = "动态类型";
    num1 = 11.45;
    num1 = 114514n;
    ```

1. Number 类型代表 整数 和 浮点数 

- Number 类型包括“特殊数值（“special numeric values”）
    - Infinity、-Infinity 和 NaN
    ```javascript {.line-numbers}
    alert( 1 / 0 );     // Infinity
    alert( Infinity );  // Infinity
    ```

2. BigInt 类型
    - “number” 类型无法表示大于 (2^53-1) 或小于 -(2^53-1) 的整数
    - 通过将 n 附加到整数字段的末尾来创建 BigInt 值 (114514n)

- NaN
    - NaN 代表一个计算错误
    - NaN 是粘性的, 任何对 NaN 的进一步数学运算都会返回 NaN
        - (只有一个例外：NaN ** 0 结果为 1)
    - JS 中数学运算是**安全**的: 可以 除以 0，将非数字字符串视为数字等
        - 脚本永远不会因一个致命的错误（“死亡”）而停止。
    - 最坏的情况下，我们会得到 NaN 的结果

3. String 类型 
    - 字符串必须被括在引号里
    - JavaScript 中没有 character 类型
    - 三种包含字符串的方式: 
        - 双引号和单引号都是“简单”引用; 
        - 反引号是 **功能扩展** 引号
        ```javascript {.line-numbers}
        let UserName = "ani";
        alert( `${UserName}'s age is ${18 + 6}` ); 
        ```

4. Boolean 类型（逻辑类型） 
    - typeof true // "boolean"

5. “null” 值
    - JavaScript 中的 null 仅仅是一个代表“无”、“空”或“值未知”的特殊值。

6. “undefined” 值
    - undefined 的含义是 未被赋值

7. object 类型和 symbol 类型
    - symbol 用于唯一的标识符; object 用于更复杂的数据结构

9. typeof 运算符
    - 例外: 
    - ```javascript {.line-numbers}
        typeof null == "object" // JavaScript 编程语言的设计错误
        typeof function(){} == "function" // 函数被特殊对待
        ```
## 交互函数: `alert` / `prompt` / `confirm`

1. `alert ("Hello");`
    - 对 `alert` 的调用没有返回值 / **返回 `undefined`**

2. `Result = prompt Display [, Default]);`
    - `[...]` 方括号 表示该**参数可选**/非必需
    - 若取消输入, 返回 **null**

3. `IfResult = confirm (Question);`
    - 点击 确定/取消 返回 `true / false`

- `alert/prompt/confirm` 都是模态的：
    1. 暂停脚本的执行，弹出 **模态窗口** 
    2. 不允许用户与该页面的其余部分进行交互，直到窗口被解除

- 模态窗 (model window)
    - “modal” 意味着用户不能与页面的其他部分（例如点击其他按钮等）进行交互，直到他们处理完窗口

- 方法的两个**限制**: 模态窗口的 确切位置/确切外观 皆取决于浏览器, JS不能修改

## 类型转换

> *大多数情况下，运算符和函数会自动将赋予它们的值转换为正确的类型。*

### 字符串转换 String()

- `alert(theValue)` 将 `theValue` 转换为*字符串类型*
- `String(theValue)` 将 `theValue` 转换为字符串类型

    ```javascript {.line-numbers}
    let value = true;
    alert(typeof value);    // boolean
    value = String(value);  // 现在值是一个字符串形式的 "true"
    alert(typeof value);    // string
    ```

### 数字型转换 Number()

- 算术函数和表达式中，会自动进行 `number` 类型转换。
- `Number(theValue)` 将 `theValue` 转换为 `number` 类型。
- 若 `theValue` 不是一个有效的数字，
    - `null / ""` -> `0` ; `true/false` -> `1/0`
    - **`undefined` -> `NaN`** ; `string` -> `去除首尾空格后的数字` / `NaN`
    ```javascript {.line-numbers}
    alert( Number("\t \n 123  ") ); // 123 (number)
    alert( Number("  1 23  ") ); // NaN
    alert( Number("        ") ); // 0
    ```

### 布尔型转换 Boolean()

- 发生在逻辑运算中
- 也可显式地调用 `Boolean(value)` 进行转换
- 直观上为“空”的值（ 如 `0`, `""`, `null`, `undefined`, `NaN`）将变为 `false`
- 其他值 ( 如 **`"0"`, `" "`** ) 变成 `true` ( JS 中，非空的字符串总是 `true` )

## 基础运算符，数学

### 术语：“一元 / 二元运算符”，“运算元”

1. **运算元 /** 参数 —— 运算符应用的对象 
    - eg. `左运算元 + 右运算元 = 结果`

2. 一元运算符: 运算符只对应一个运算元
    - eg. 一元负号运算符(unary negation) `-`，作用是对数字进行正负转换
    - `x = -x; // -1`
3. 二元运算符: 一个运算符拥有两个运算元
    - eg. 二元运算符减号 `-`
    - 相同的符号 `-` 表征了两个不同的运算符: 负号运算符, 减法运算符

### 数学运算

- 加减乘除 `+, -, *, /`
- 取余 `%`
    - `a % b` 结果是 `a / b` 的 **余数**
- 求幂 `**`
    - 求幂运算 `a ** b` 相当于数学中的 *`a^b`*
    - 幂运算也适用于非整数:` 1/2次方`与`平方根`相同

### 二元运算符 `+` 连接/合并字符串

- 只要任意一个运算元是字符串，另一个运算元也将被转化为字符串
- 运算符从左到右 **按顺序** 工作
    ```javascript {.line-numbers}
    alert( 2 + 2 + "1" + 2 ); // "412"
    alert( "2" + 2 + 1 + 2 ); // "2212"
    ```
- 其他算术运算符 **只对数字** 起作用，并且总是将其运算元转换为数字
    ```javascript {.line-numbers}
    alert( 6 - '2' );   // 4，将 '2' 转换为数字
    alert( '6' / '2' ); // 3，将运算元都转换为数字
    alert( 6 - '2  2'); //NaN
    ```

### 一元运算符 `+` 数字转化

- 一元运算符`+` / `+`应用于单个值，对数字 **无作用**
- 如果运算元不是数字，`+`则会将其转化为数字

    ```javascript {.line-numbers}
    let y = -2;
    alert( +y ); // -2
    alert( +true ); // 1
    alert( +"" );   // 0
    ```

### 运算符优先级

> 参考 [Mozilla 的 优先级表](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence#table)

优先级|符号|Associativity
:-:|-|-
19|`( … )` |N/A
15|`+ …`, `- …`, (Unary一元)| right-to-left	
16|`… ++`, `… --`|N/A
14|`… ** …` | right-to-left	
13|`… * …`, `… / …`, `… % …`| left-to-right 
12|`… + …`, `… - …` | left-to-right	
2|`… = …`, `+=`, `-=`, `*=`, `/=` | **right-to-left**
1|`… , …`|left-to-right	
- 链式赋值（Chaining assignments）
    - `=` 从右至左计算

### 自增/自减

- 自增/自减只能应用于变量。对数值用（如 `5++`）会报错
- 运算符置于变量 前/后 ，被称为“ 前/后 置形式”

### 位运算符

- 位运算符把运算元当做 32 位整数，并在其**二进制**表现形式上操作
- 按位与`&`, 按位或`|`, 按位异或`^`, 按位非`~`, 左移`<<`, 右移`>>`, 无符号右移`>>>`

### 逗号运算符

- 优先级最低(1), 是最少见最不常使用的运算符之一
- 每个语句都运行，但是只有 **最后的语句** 的结果会被返回
    ```javascript {.line-numbers}
    let a = (1 + 2, 3 + 4);
    alert( a ); // 7（返回3+4, 1+2被舍弃）`
    ```

## 值的比较

- 比较结果为 Boolean 类型, 所有比较运算符 **均返回布尔值**：

### 字符串比较

- 字符串按字符（母）逐个进行比较

- 比较算法:
    - 按 Unicode 编码顺序比较同位置的单个字符
    - 未结束（还有未比较的字符/更长）的字符串更大

### 不同类型间的比较

- 先转化为数字（number）再判定大小
- 忽略首位空格
- `""` `==` `0` `==` `false` `!==` `"0"`
    ```javascript {.line-numbers}
    let a = 0;  // Boolean(a)为false
    let b = "0";// Boolean(b)为true
    alert(a == b); // true! (0=0)
    ```

### 严格相等

- 比较时不会做任何的类型转换 (字符串/数值/布尔值)

### 比较 null / undefined 
- 在相等性检查 `==` 中 `null/underfined` 不会进行任何的类型转换
- 非严格相等时, `null/underfined` 等且只等于 `null/underfined`
    ``` javascript {.line-numbers}
    null == underfined  // ture, 只等于对方
    null !== underfined // ture, 严格不相等
    ```
- 使用数学式或其他比较方法 `< > <= >=` 时, `null/underfined` 被转为数字
    - `null` 被转为 `0`，`undefined` 被转为 `NaN`
    - ``` javascript {.line-numbers}
        alert( null > 0 );  // false , 0 > 0
        alert( null == 0 ); // false , null只与underfined相等
        alert( null >= 0 ); // true  , 0 >= 0
        ```
- `undefined` 不应该被与其他值进行比较
    - 当 `underfined` `> < >= <=` 时转为 `NaN`
    - `NaN` 是特殊数值型值, 与任何值 (`包括NaN`) 比较 **都会返回 `false`**

## 条件分支：if 和 '?'

- `if (…)` 语句会计算圆括号内的表达式，并将计算结果转换为布尔型。
    - 数字 0、空字符串 ""、null、undefined 和 NaN 都会被转换成 `false`, 它们被称为“假值（falsy）”值。
    - 其他值被转换为 `true`, 所以它们被称为“真值（truthy）”。

### 条件 / 三元运算符 '?'

- 可嵌套使用
- 需要执行不同的代码分支时应该使用 `if`
``` javascript {.line-numbers}
let result = (condition1) ? value1 : 
             (condition2) ? value2 : 
             ...
             End-Value;
```

## 逻辑运算符（新增 `??` ）

- JS 有四个逻辑运算符：`||` `&&` `!` `??`(空值合并运算符)
- 运算符可 被应用于/输出 **任意类型的值**，而不仅仅是布尔值

1. `result = value1 || value2 || value3;`
    - 从左到右依次计算操作数
    - 返回 第一个**真值** / 该链的最后一个值
    - `||` **无法区分** `false` `0` `""` `null`/`undefined` (见`??`)

2. `result = value1 && value2 && value3;`
    - 从左到右依次计算操作数。
    - 返回 *第一个假值* / 该链的最后一个值

3. `!!"non-empty string" // true`
    - `!` 将操作数转化为布尔类型`true/false`并返回相反的值
    - `!!…` 作用相当于 `Boolean(…)`

4. 空值合并运算符 `??`（新增）
    - 返回 第一个 **`已定义的(defined)`** 值
    - 将 `非null` `非undefined` 的表达式称为 `已定义的(defined)`
    - 用于为变量分配默认值 (对`||`的优化)

6. JS 禁止将 `??` 与 `&&` / `||` 一起使用, 除非 `()` 明确指定了优先级
5. 优先级 `!` > `&&`  > `||` = `??`

## 循环: `[do] while` `for`

1. `while` 与 `do…while`
    - `while (condition) { // 所谓的"循环体", 放有代码 }`
    - 循环体的 单次执行 叫作 *一次迭代*
    - 循环条件被计算并转化为布尔值 (可为任何表达式或变量)
    <br />
    
2. `for (;;) { // 无限循环 }`
    - "内联"变量声明: 变量在循环中声明
    <br />

3. 跳出循环 `break` / 继续下一次迭代 `continue`
    - `continue` 不会停掉整个循环, 而 `break` 会
    - `continue`停止当前这一次迭代并强制启动新一轮循环(条件允许时)
    - **禁止** `break/continue` 在 `?` 的右边, 否则报错
    <br />
    
4. `break/continue` 标签
    - **标签** 是在循环之前带有冒号的标识符：
    1. `labelName: for (...) { ... }`
    - 标签是 `break/continue` 跳出 **嵌套循环** 以转到外部的唯一方法
    2. `break <labelName>` **向上**寻找至标签处并跳出此循环
    3. `continue <labelName>` 向上跳转到标记循环并执行下一次迭代
    - 标签并不允许“跳到”所有位置
        - `break` 指令必须在 代码块 (任何被标记的代码块)内
        - `continue` 只有在 循环 内部才可行

## `switch` 语句

- `switch` 语句有至少一个 `case` 代码块和一个可选的 `default` 代码块
    - ``` javascript {.line-numbers}
        switch(x) {
        case 'value1':  // if (x === 'value1')
            ...    [break]
        default:
            ...    [break]
        }
        ```
- 这里的相等是 **严格相等**
- `switch` 换成 `else-if` 时应使用 `===` 来判定条件
- 如果没有 `break`, 程序将不经任何检查继续执行下一个 `case`
- `switch` 和 `case` 都允许任意表达式
- 共享同一段代码的几个 `case` 分支可以被分为一组

## 函数 (函数声明)

- 使用 **函数声明** 创建函数。
-   ``` javascript {.line-numbers}
    function name(parameters, delimited, by, comma) {
    ...body... /* 函数体 */ }
    ```
- 在代码块` {...} `后以及有代码块的语法结构（例如循环）后不需要加分号`;`
- 局部变量: 在函数中声明的变量只在该函数内部可见
    - 若函数内部声明了同名变量，则 *优先使用* 内部变量
-  **全局** 变量: 任何函数之外声明的变量
- 默认值
    - 若被调用函数的参数未提供，相应的值默认为 `undefined`
    - 用 `parameter="..."` 为函数声明中的参数指定"默认"值
- 后备默认参数
    - 可先声明再设置默认值(放在函数执行中)
    - 可使用 `??` , eg.`alert(count ?? "unknown");`
- 返回值
    - 单纯的 `return` 会导致函数**立即退出**
    - 空值的 `return` 或无 `return` 的函数返回值为 **`undefined`**
    - 不要随意换行 / 跨行先加 `()` : JS 默认会在 `return` 之后加上分号 `;`
- 函数 == 注释
    - 函数应该 简短 + 只有一个功能 + 只包含函数名所指定的功能
    - **自描述** 通过函数名就可以看出函数的行为，而不用通过代码

## 函数表达式

- 仅当函数声明不适合对应的任务时，才应使用函数表达式
- 函数创建发生在赋值表达式的上下文中（如在 `=` 的右侧）
- 函数表达式允许省略函数名 `function() {...}`
- 函数是一个**表示 "行为" 的值**
    - `func1()` 指代函数调用后 `return `的结果
    - `func1` 指代函数 **本身** , 可用 `=` 复制给另一个值
- **回调**函数 / 回调
    - ``` javascript {.line-numbers}
        function func1(){}
        func1 ("...", func2, func3...)// func2, func3为*回调函数*
        ```
- 匿名函数
    - 匿名函数在调用外无法访问 (未分配变量) 
    - ``` javascript {.line-numbers}
        function func1(){}
        func1 ("...", 
                function() {...},       // 匿名函数1
                function() {...} ...)   // 匿名函数2
        ```
- 函数表达式 vs 函数声明
    - **函数声明**: 在主代码流中声明为单独的语句的函数
    - **函数表达式**: 在一个表达式/另一个语法结构中创建的函数
- 运行顺序
    - JS 准备运行脚本时，**首先寻找**全局函数声明，并创建这些函数 (可将其视为“初始化阶段”)
    - 在处理完所有函数声明后，代码才被执行。所以运行时能够使用这些函数
    - *函数表达式是在代码**执行到达时被创建**，并且仅从那一刻起可用*

- 函数声明功能: **块级作用域**
    - 严格模式下，当一个函数声明在一个代码块内(如`if`中)时，它在该代码块内的任何位置都是可见的。但在代码**块外不可见**

## 箭头函数基础

``` javascript {.line-numbers}
let func = (arg1, arg2, ..., argN) => expression;
let sum = (a, b) => {  // 花括号表示开始一个多行函数
  ...
  return result; // 若使用了 {} ，则需要一个显式 “return”
};
```

# 代码质量


## 在浏览器中调试

> 调试 指在一个脚本中找出并修复错误的过程

### JS 补充

1. `debugger;` 写在脚本中, 在调试器中暂停代码

2. `console.log( )` 日志记录

### `Sources` 资源面板

1. `File Navigator` 

    - 依附于此页面的文件, 包括 Chrome 扩展程序

2. `Code Editor` 

    - `Breakpoints` 断点 / `Conditional Breakpoints` 条件断点
    - `Continue to here` 右键的 `context menu` (关联菜单) 中



3. `JavaScript Debugging` 操作

    - `Resume script execution` 恢复: 继续执行, 直到结束/下一个断点
    - `Step`: 运行下一条指令 (会忽略异步行为如 `setTimeout`) 
    - `Step over next function call`: 后台执行函数调用, 跳过函数内部
    - `Step into next function call`: 单步执行函数
    - `Step out of current function`: 执行到当前函数最后一行
    - `Pause on exceptions`: 开/关 出现错误时自动暂停脚本执行

4. `JavaScript Debugging` 查看

    - `Watch` 察看: 显示任意表达式的当前值

    - `Call Stack` 调用栈: 显示嵌套的调用链

    - `Scope` 作用域: 显示当前的局部/全局变量


## 代码风格

- 单行中不用 `{...}`
- indent 水平缩进 / 垂直缩进
- `;` 每一个语句后面都应该有一个分号
- 避免嵌套
    - 循环中可使用 `(!...) continue;` `if/else` `return` 避免嵌套
- 函数位置
    - 建议: 先写调用代码, 再写函数 (命名准确)
- 风格指南
- 自动检查器

- 注释这些
    - 整体架构，高层次的观点。
    - 函数的用法。
    - 重要的解决方案，特别是在不是很明显时。
- 避免注释
    - 描述“代码如何工作”和“代码做了什么”
    - 在代码足够简单或有很好的自描述性时还写没必要的注释


## 使用 Mocha 进行自动化测试

- waiting...


## Polyfill Transpilers 


- Transpilers 转译器

    - 使用旧的语法结构重写现代**语法或运算符**

- Polyfills 垫片

    - 更新/添加 **新函数** 的脚本


# Object 基础知识

## Object / plain object

> [JS 有八种数据类型](##数据类型)

- 7 种原始类型: 值只包含一种东西 (字符串, 数字或其他)

- 1 种引用类型: 用来存储键值对和更复杂的实体

-  `literal` 字面量
    - `literal` 字面量是用于表达一个固定值的表示法 (或用来为变量赋值时的常数量)，又叫常量
    - 字面量分为 字符串/数组/对象/函数 字面量( `string/array/object/function` `literal` )等
        - eg. `let str1 = "a str";` `"a str"` 是数字字面量, `str1` 是变量
    - 判断自变量    
        1. 这个量可以作为一个合格的表达式
        2. 执行结果等于其自身

1. `Object` 创建
    - 通过使用带有可选 **属性列表** 的花括号 {…} 来创建对象
        ``` javascript {.line-numbers}
        let Object1 = new Object(); //一 “构造函数” 的语法
        let Object2 = {
            [key1:value1, 
            key2:value2, 
            ...]
            }; //二 “object literal 对象字面量” 的语法
        ```
    - 一个属性 `property` 就是一个键值对: ( 属性的`key/name/identifier(键/名字/标识符)` `:` 属性的 `value(值)` )
    - 其中 键 `key` 只能是字符串 / `Symbol` 类型, 值 `value` 可以是任何值
        - 若 `key` 中有空格则需加 `""`, 如 `"a key": ture,` 
    - 列表中的最后一个属性应以**逗号结尾**, 称尾随或悬挂逗号 (trailing/hanging comma)

2. 访问属性值
    - 使用 `delete`操作符 **删除** 属性值
    - 使用点符号 `ObjectName.keyName` 访问属性值 `value`
    - 使用方括号 `ObjectName[keyName]` 访问属性值 `value`
        - 若 `key` 中有空格, 可使用 `ObjectName["a key"]` 访问值
        - `KeyName` 可以是 **任意表达式** , 比如变量

3. 计算属性
    - 创建对象可在对象字面量中使用方括号 `[ObjectName] : value`
    - 此处 `ObjectName` 可为变量, 表达式

4. 属性值简写
    - 属性名简写方式可以与正常方式混用
    ```javascript {.line-numbers}
    function makeUser(name, age) {
    return {
        name: name, // 1
        name,       // 2, 1 2 等效
        age: age,   //3
        age,        //4 , 3 4 等效
        // ……其他的属性
    };
    }
    let user = makeUser("John", 30);
    alert(user.name); // John
    ```

5. 属性名称限制
    - 属性命名**无限制**, 属性名可以是任何字符串或者 symbol
    - 其他类型会被自动地转换为字符串 (如 `0` -> `"0"`)
    - 例外: 名为 `__proto__` 的属性, 不能将它设置为一个非对象的值

6. 属性存在性测试, `"in"` 操作符
    - JS 的 Object 能够被访问**任何**属性, 若不存在则返回 `undefined`
    - `"ObjectKey1"` `in` `ObjectName` 检查属性是否*存在*
        - `in` 左边的 `属性名` 省略引号则表示一个变量
    - 若属性值为`undefined`, `in` 判断为 `ture`, 直接访问显示`undefined`

7. `"for…in"` 循环
    - 所有的 `"for"` 结构体都允许在循环中**定义变量**
        - 如 `let key in user` `let prop in obj`
    - ``` javascript {.line-numbers}
        for ( [let] key in obj) {
        [alert( key );]// 对此对象属性中的每个键执行的代码
        } 
        ```

8. 遍历时的顺序
    - **整数属性** 会被排序, 其他属性则按照**创建的顺序**显示
        - `整数属性`指可在不做任何更改下与 *整数* 相互转换的*字符串*
        - eg.`"+49" -> 49 -> "49" != "+49"`, `"1.2" -> 1 ->"1" != "1.2"`


## Object 引用和复制

- 赋值对象的变量存储该对象**在内存中的地址**, 而非对象本身
    - 字符串, 布尔值等原始类型始终以"整体值"的形式被复制
    - 相比对象的根本区别之一是其"通过引用"被存储和复制的
- 使用 `const` 声明的对象**可被修改**
<br />

- 比较对象
    - 仅当两个对象为同一对象时两者才相等
    - 两个独立的对象不相等, 即使都为空
    -   ``` javascript {.line-numbers}
        let a = {};
        let b = a;
        let c = {};

        alert ( a === b ); // ture
        alert ( a !== c ); // ture
        ```
- 克隆与合并, `Object.assign`
    - ``` javascript {.line-numbers}
        for (let key in user) {
            clone[key] = user[key];
        }

        Object.assign(dest, [src1, src2, src3...])
        ```
    - `Object.assign(目标对象, [源对象1, 源对象2...])`
        - 目标对象的相同属性会被源对象覆盖
        - 可用来合并多个对象

- 深层克隆 (属性引用其他对象)
    - 递归实现, 如 `lodash` 库的 `_.cloneDeep(obj)`

## 垃圾回收

- Reachability 可达性

1. 固有可达值(roots)明显不能被释放
    - 如: 当前执行的和嵌套调用链上的函数及其局部变量和参数, 全局变量, 等
2. 若值可通过引用/引用链从根访问任何其他值, 认为该值是可达的
    - 对外引用不重要, 只有**传入引用**才可以使对象可达(指向该对象)
    - 无**外部引用**的孤立对象(群)也视为不可达

- garbage collector 垃圾回收器 
    - JS引擎后台运行
    - 监控所有对象状态并删除已经不可达的

- 内部算法
    - 垃圾回收的基本算法被称为 "mark-and-sweep"

## Object 方法，`"this"`

- 作为对象属性的函数被称为 *method* (方法)
    - 方法简写 (首选较短的语法)
    -  ``` javascript {.line-numbers}
        user = {
        sayHi: function() { alert("Hello"); }
        };

        // 方法简写
        let user = {
        sayHi() { alert("Hello"); } // 与 "sayHi: function(){...}" 一样
        };
        ```

- 方法中的 `"this"`
    - `user.func1()`
    - `this` 的值就是点之前的这个对象`user`, 即调用该方法的对象
    <br />

- `this` 不受限制
    - JS 中的 `this` 可以用于任何函数, 即使它不是对象的方法
    - `this` 的值在代码运行时计算出来, 取决于代码上下文
    <br />

- 没有对象的情况下调用含有 this 的函数
    - `"use strict"` , `this == undefined` 
    - 非严格模式的情况下, `this` 将会是 全局对象
    <br />

- 箭头函数没有自己的 `"this"`
    - 若箭头函数中引用 `this`, 则其值取决于外部 "正常的" 函数

## 构造器和操作符 "new"

1. 构造函数
    - 构造函数在技术上是常规函数
    1. 命名以大写字母开头
    2. 只能由 `"new"` 操作符来执行
    <br />

2. 当函数用 new 操作符执行时
    1. **`this = {};`**（隐式创建）
    2. 函数体执行, 通常修改 `this`, 添加新的属性等
    3. **`return this;`**（隐式返回）
    - 不建议: 若无参数, 可以省略 `new` 后的 `()`
    <br />

3. (少用) 构造器模式测试：`new.target`
    - 检查函数是否被使用 `new` 进行调用
    <br />

4. 构造器的 `return`
    - 通常构造器 无 `return` 语句
    1. 若 `return` 返回一个对象, 则返回这个对象
    2. 若 `return` 返回原始类型/无返回, 忽略并返回 `this`
    <br />

5. 构造器中的方法
    - 不仅是属性, 也可将 方法 添加到 `this` 中

## 可选链 `?.`

> `?.` 链使我们能够安全地访问嵌套属性

- `?.` 前的变量必须已声明/定义, 否则报错
- 若 `?.` 前的值为 `undefined/null` (不存在), 立即停止并返回`undefined` ("短路效应")
- `?.` 使其前的值成为可选值, 但不对其后的起作用
- 不要过度使用可选链
- 其它变体：`?.()`, `?.[]`, `delete user?.name;`
- 可使用 `?.` 来安全地读取或删除，但 **不能写入**






## Symbol 类型

> Object 的属性 key 只能是 `String` / `Symbol` 类型

 
- `"Symbol"` 值表示唯一的标识符
    ``` javascript {.line-numbers}
    let id = Symbol(["描述 / Symbol名"]);// id 是 symbol 的一个实例化对象, 是描述为 "描述 / Symbol名" 的 Symbol
    ```
- `Symbol` 保证是 **唯一** 的
    - 即使 Symbol 的描述完全相同, 它们的值也是不同
    - 描述只是一个标签, 无任何影响

- `Symbol` 不会被自动转换为字符串
    ``` javascript {.line-numbers}
    let id = Symbol("id");
    alert(id); // TypeError: Cannot convert a Symbol value to a string
    alert(id.toString()); // Symbol(id), 现在它有效了
    alert(id.description); // id, 只显示 description/描述
    ```











## Object — 原始值转换






























``` javascript {.line-numbers}


```






``` javascript {.line-numbers}


```




``` javascript {.line-numbers}


```



































1. 
    - 
2. 
3. 
4.
5.





```javascript {.line-numbers}

```

1. 
    - 
2. 
3. 
4.
5.


```javascript {.line-numbers}
```