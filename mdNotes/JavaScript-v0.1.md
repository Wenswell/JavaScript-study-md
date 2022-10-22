# 简介

## 手册与规范

1. **ECMA-262 规范** 确地定义了Java这门语言。

2. **MDN (Mozilla) JavaScript 索引** 是一个获取关于个别语言函数、方法等深入信息的很好的信息来源。

3. **兼容性表** eg.[每个功能的支持表](http://caniuse.com)

## 代码编辑器

1. **IDE**(Integrated development environment)

2. **轻量编辑器**

# JavaScript 基础

> *JavaScript 是一门动态类型、面向对象的脚本 (Script) 语言。*

## 引入/使用 JavaScript

1. 内嵌脚本: 使用 `<script>` 标签在 **HTML** 中插入 JavaScript 程序

```html {.line-numbers}
<script>
        alert("Hello World");
</script>
```

2. 外部脚本: 在 `<script>` 中通过 `src` attribute(特性) 引入 JS 文件

- **注意**: 如果设置了 src 特性, **此** script 标签的内容将会被忽略(不能同时生效)

```html {.line-numbers}
<script src="./01.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.11/lodash.js"></script>
```

## 代码结构

### Statements | 语句

> *语句是执行行为 (action) 的语法结构和命令。*

1. 语句之间可以使用`;`分号进行分割

2. *(不建议)* 存在换行符 (line break) 时, 大多数情况下可以省略分号

### "use strict" | 现代模式

> 2009 年 ECMAScript 5 (ES5) 出现。ES5 规范增加了新的语言特性并且 *修改了一些已经存在的特性* 。

1. "use strict"处于脚本文件/函数体的 **最顶部** 时, 整个脚本文件/函数都将以“现代”模式进行工作

2. 没有办法取消 use strict , **没有**指令可以使程序返回默认模式

3. 浏览器开发者控制台运行代码时, 默认不启动 use strict 

## Variables | 变量 

> 变量 是数据的“命名存储”。

0. `let aVariable = "anyValue";`

1. 可以在一行中声明多个变量

2. 一个变量只能被声明一次 (重复声明会 error)

### 变量命名

1. 名称仅能包含 `字母`, `数字`, 符号 `$` 和 `_`

2. 首字符必须非数字(只能以`字母/$/_`开头)

3. *区分大小写*

4. 驼峰式命名法 (camelCase) 

5. 保留字无法用作变量命名

6. use strict 下, 赋值前 *必须先声明*

### 常量 const aConstant = 3.14

1. 使用 const 声明的变量称为“常量/Constant”

2. 常量不能被修改, 否则报错

3. **const命名** 
    - 小写适合计算出来的值
    - 大写适合/仅用作 “硬编码(hard-coded)” 值 (执行之前就已知)
    - eg. 
        ```javascript {.line-numbers}
        const COLOR_ORANGE = "#FF7F00";
        let color = COLOR_ORANGE;
        ```

## 数据类型

> *JavaScript 有 8 种基本的数据类型 (7 种原始类型 `Number、String、Boolean、Null、undefined、symbol、bigInt`, 1 种引用类型 [`object`](##object) ) *

- JS 属于 “动态类型” (dynamically typed) 编程语言: 定义的变量不会被限制为某一数据类型
    ```javascript {.line-numbers}
    num1 = "动态类型";
    num1 = 11.45;
    num1 = 114514n;
    ```

1. Number 类型代表 整数 和 浮点数 

- Number 类型包括 “特殊数值” (special numeric values) 
    - `Infinity` , `-Infinity` , `NaN`
    ```javascript {.line-numbers}
    alert( 1 / 0 );     // Infinity
    alert( Infinity );  // Infinity
    ```

- NaN
    - NaN 代表一个计算错误
    - NaN 是粘性的, 任何对 NaN 的进一步数学运算都会返回 NaN
        - 只有一个例外：NaN ** 0 == 1
    - JS 中数学运算是**安全**的: 可以 除以 0, 将非数字字符串视为数字等
        - 脚本永远不会因一个致命的错误 (“死亡”) 而停止。
        - 最坏的情况下会得到 NaN 的结果

2. BigInt 类型
    - `number` 无法安全表示大于 (2^53-1) 或小于 -(2^53-1) 的整数
        - 超出安全范围会出现精度问题(奇数 -> 偶数)
        - `Number.MAX_SAFE_INTEGER + 1 === Number.MAX_SAFE_INTEGER + 2; //ture`
    - 将 n 附加到整数字段的末尾来创建 BigInt 值 (`114514n`)

3. String 类型 
    - JavaScript 中没有 character 类型
    - 字符串必须被括在引号里
    - 三种包含字符串的方式: 
        - 双引号和单引号都是“简单”引用; 
        - 反引号是 **功能扩展** 引号
        ```javascript {.line-numbers}
        let UserName = "ani";
        alert( `${UserName}'s age is ${18 + 6}` ); 
        ```

4. Boolean 类型 (逻辑类型)  
    - `alert( typeof true );  //"boolean"`

5. “null” 值
    - JavaScript 中的 null 仅仅是一个代表“无”、“空”或“值未知”的特殊值

6. “undefined” 值
    - undefined 的含义是 未被赋值
    - 未进行初始化的事物的默认初始值

7. object 类型和 symbol 类型
    - symbol 用于唯一的标识符; object 用于更复杂的数据结构

- typeof 运算符
    - 例外: 
    - ```javascript {.line-numbers}
        typeof null == "object" // JavaScript 的设计错误
        typeof function(){} == "function" // 函数被特殊对待
        ```
    - `null` 有自己的类型, 不是object
    - function 隶属于 `object`,但在 typeof 中被分为 function


## 交互函数: `alert` / `prompt` / `confirm`

1. `alert ("Hello");`
    - 对 `alert` 的调用没有返回值 / **返回 `undefined`**

2. `Result = prompt (Display [, Default]);`
    - `[...]` 方括号 表示该**参数可选**/非必需
    - 若取消输入, 返回 **null**

3. `IfResult = confirm (Question);`
    - 点击 确定/取消 返回 `true / false`

- `alert/prompt/confirm` 都是模态的：
    1. 暂停脚本的执行, 弹出 **模态窗口** 
    2. 不允许用户与该页面的其余部分进行交互, 直到窗口被解除

- 模态窗 (model window)
    - “modal” 意味着用户不能与页面的其他部分 (例如点击其他按钮等) 进行交互, 直到他们处理完窗口

- 方法的两个**限制**: 模态窗口的 确切位置/确切外观 皆取决于浏览器, JS不能修改

## 类型转换

> *大多数情况下, 运算符和函数会自动将赋予它们的值转换为正确的类型。*

### 字符串转换 String()

- `alert(theValue)` 将 `theValue` 转换为*String类型*
- `String(theValue)` 将 `theValue` 转换为String类型

    ```javascript {.line-numbers}
    let value = true;
    alert(typeof value);    // boolean
    value = String(value);  // 现在值是一个字符串形式的 "true"
    alert(typeof value);    // string
    ```

### 数字型转换 Number()

- 算术函数和表达式中, 会自动进行 `number` 类型转换。
- `Number(theValue)` 将 `theValue` 转换为 `number` 类型。
- 若 `theValue` 不是一个有效的数字, 
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
- 直观上为“空”的值 ( 如 `0`, `""`, `null`, `undefined`, `NaN`) 将变为 `false`
- 其他值 ( 如 **`"0"`, `" "`** ) 变成 `true` ( JS 中, 非空的字符串总是 `true` )

## 基础运算符, 数学

### 术语：“一元 / 二元运算符”, “运算元”

1. **运算元 /** 参数 —— 运算符应用的对象 
    - eg. `左运算元 + 右运算元 = 结果`

2. 一元运算符: 运算符只对应一个运算元
    - eg. 一元负号运算符(unary negation) `-`, 作用是对数字进行正负转换
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

- 只要任意一个运算元是字符串, 另一个运算元也将被转化为字符串
- 运算符从左到右 **按顺序** 工作
    ```javascript {.line-numbers}
    alert( 2 + 2 + "1" + 2 ); // "412"
    alert( "2" + 2 + 1 + 2 ); // "2212"
    ```
- 其他算术运算符 **只对数字** 起作用, 并且总是将其运算元转换为数字
    ```javascript {.line-numbers}
    alert( 6 - '2' );   // 4, 将 '2' 转换为数字
    alert( '6' / '2' ); // 3, 将运算元都转换为数字
    alert( 6 - '2  2'); //NaN
    ```

### 一元运算符 `+` 数字转化

- 一元运算符`+` / `+`应用于单个值, 对数字 **无作用**
- 如果运算元不是数字, `+`则会将其转化为数字

    ```javascript {.line-numbers}
    let y = -2;
    alert( +y );    // -2
    alert( +true ); // 1
    alert( +"" );   // 0
    alert( +"str" );// NaN
    ```

### 运算符优先级

> 参考 [Mozilla 的 优先级表](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence#table)

优先级|符号|Associativity
:-:|-|-
19|`( … )` |N/A
16|`… ++`, `… --`|N/A
15|`+ …`, `- …`, (Unary一元)| right-to-left	
14|`++ …`, `-- …`|N/A
14|`… ** …` | right-to-left	
13|`… * …`, `… / …`, `… % …`| left-to-right 
12|`… + …`, `… - …` | left-to-right	
2|`… = …`, `+=`, `-=`, `*=`, `/=` | **right-to-left**
1|`… , …`|left-to-right	
- 一元运算符优先级 高于 二元运算符
- 链式赋值 (Chaining assignments) 
    - `=` 从右至左计算

### 原地修改

- 所有算术和位运算符都有简短的“修改并赋值”运算符
`… = …` `… += …` `… -= …` `… *= …` `… /= …` `… %= …` `… **= …`
- 其优先级都与 `=` 相同 (`Precedence == 2`)

### 自增/自减

- 自增/自减只能应用于变量。对数值用 (如 `5++`) 会报错
- 运算符置于变量 前/后 , 被称为“ 前/后 置形式”

### 位运算符

- 位运算符把运算元当做 32 位整数, 并在其**二进制**表现形式上操作
- 按位与`&`, 按位或`|`, 按位异或`^`, 按位非`~`, 左移`<<`, 右移`>>`, 无符号右移`>>>`

### 逗号运算符

- 优先级最低(`Precedence == 1`) *低于 `=`* , 是最少见最不常使用的运算符之一
- 每个语句都运行, 但是只有 **最后的语句** 的结果会被返回
    ```javascript {.line-numbers}
    let a = (1 + 2, 3 + 4);
    alert( a ); // 7 (返回3+4, 1+2计算后结果3被舍弃) `
    ```

## 值的比较

- 比较结果为 Boolean 类型, 所有比较运算符 **均返回布尔值**：

### 字符串比较

- 字符串按字符 (母) 逐个进行比较

- 比较算法:
    - 按 Unicode 编码顺序比较同位置的单个字符
    - 未结束 (还有未比较的字符/更长) 的字符串更大

### *不同类型* 间的比较

- `'2' > '123'; // ture!`
- 先转化为数字 (number) 再判定大小
- 忽略首尾空格
- `""` `==` `' 0 '` `==` `0` `==` `false` `!==` `"0"`
    ```javascript {.line-numbers}
    let a = 0;  // Boolean(a)为false
    let b = " 0 ";// Boolean(b)为true
    alert(a == b); // true! (0==0)
    ```

### 严格相等 `===`

- 比较时不会做任何的类型转换 (字符串/数值/布尔值)

### 比较 null / undefined 
- 在相等性检查 `==` 中 `null/underfined` 不会进行任何的类型转换
- 非严格相等时, `null/underfined` 等且只等于 `null/underfined`
    ``` javascript {.line-numbers}
    null == underfined  // ture, 只等于对方
    null !== underfined // ture, 严格不相等
    ```
- 使用数学式或其他比较方法 `< > <= >=` 时, `null/underfined` 被转为数字
    - `null` 被转为 `0`, `undefined` 被转为 `NaN`
    - ``` javascript {.line-numbers}
        alert( null > 0 );  // false , 0 > 0
        alert( null == 0 ); // false , null只与underfined相等
        alert( null >= 0 ); // true  , 0 >= 0
        ```
- `undefined` 不应该被与其他值进行比较
    - 当 `underfined` `> < >= <=` 时转为 `NaN`
- `NaN` 是特殊数值型值, 与任何值 (`包括NaN`) 比较 **都会返回 `false`**

## 条件分支：if 和 '?'

- `if (…)` 语句会计算圆括号内的表达式, 并将计算结果转换为布尔型。
    - 数字 0、空字符串 ""、null、undefined 和 NaN 都会被转换成 `false`, 它们被称为“假值 (falsy) ”值。
    - 其他值被转换为 `true`, 所以它们被称为“真值 (truthy) ”。

### 条件/三元运算符 '?'

- 可嵌套使用
- 需要执行不同的代码分支时应该使用 `if`
``` javascript {.line-numbers}
let result = (condition1) ? value1 : 
             (condition2) ? value2 : 
             ...
             End-Value;
```

## 逻辑运算符 (新增 `??` ) 

- JS 有四个逻辑运算符：`||` `&&` `!` `??`(空值合并运算符)
- 运算符可 被应用于/输出 **任意类型的值**, 不仅是布尔值

1. `result = value1 || value2 || value3;`
    - 从左到右依次计算操作数
    - 返回 第一个**真值** / 该链的最后一个值
    - 短路求值 Short-circuit evaluation
        `条件 || 命令  //条件为假时命令才会执行` 
    - `||` **无法区分** `false` `0` `""` `null`/`undefined` `NaN` (见`??`)
    
2. `result = value1 && value2 && value3;`
    - 从左到右依次计算操作数
    - 返回 第一个**假值** / 该链的最后一个值

3. `!!"non-empty string" // true`
    - `!` 将操作数转化为布尔类型`true/false`并返回相反的值
    - `!!…` 作用相当于 `Boolean(…)`

4. 空值合并运算符 `??` (新增) 
    - 返回 第一个 **`已定义的(defined)`** 值
    - 将 `非null` `非undefined` 的表达式称为 `已定义的(defined)`
    - 用于为变量分配默认值 (对`||`的优化)

6. JS 禁止将 `??` 与 `&&` / `||` 一起使用, 除非 `()` 明确指定了优先级
5. 优先级 `!` > `&&`  > `||` = `??`

## 循环: `[do] while` `for`

1. `while` 与 `do…while`
    - `while (condition) { // 所谓的"循环体", 放有代码 }`
    - 循环体的 单次执行 叫作 *一次迭代(an iteration)*
    - 循环条件被计算并转化为布尔值 (可为任何表达式或变量)
    <br />
    
2. `for (;;) { // 无限循环 }`
    - "内联"变量声明: 变量**只在**循环中可见
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
        case 'value2':  // case1 和 case2 执行同样的代码
            ...    [break]
        [default:]
            ...    [break]
        }
        ```
- 这里的相等是 **严格相等**
- `switch` 换成 `else-if` 时应使用 `===` 来判定条件
- 如果没有 `break`, 程序不检查, 继续执行下一个 `case`
- `switch` 和 `case` 都允许任意表达式
- 共享同一段代码的几个 `case` 分支可以被分为一组

## 函数 (函数声明)

- 使用 **函数声明** 创建函数。
-   ``` javascript {.line-numbers}
    function name(parameters, delimited, by, comma) {
        ...body... /* 函数体 */ 
    }
    ```
- 在代码块` {...} `后以及有代码块的语法结构 (例如循环) 后**不需要**加分号`;`
- 局部变量: 在函数中声明的变量只在该函数内部可见
    - 若函数内部声明了同名变量, 则 *优先使用* 内部变量
        - 此时函数内部的操作不改变全局变量 (只改变内部的变量副本)
-  **全局** 变量: 任何函数之外声明的变量
- 默认值
    - 若被调用函数的参数未提供, 相应的值默认为 `undefined`
    - 用 `parameter="..."` 为函数声明中的参数指定"默认"值
    - 在函数中检查设置默认值: 使用 `??` , eg.`alert(num ?? "empty");`
- 返回值
    - 单纯的 `return` 会导致函数**立即退出**
    - 空值的 `return` 或 无`return` 的函数返回 **`undefined`**
    - 不要随意换行 / 跨行前先加 `(` : JS 默认会在 `return` 之后加上分号 `;`
- 函数 == 注释
    - 函数应该 简短 + 只有一个功能 + 只包含函数名所指定的功能
    - **自描述** 通过函数名就可以看出函数的行为, 而不用通过代码

## 函数表达式

- 仅当函数声明不适合对应的任务时, 才应使用函数表达式
- 函数创建发生在赋值表达式的上下文中 (如在 `=` 的右侧) 
- 函数表达式允许省略函数名 `function() {...}`
- 函数是一个**表示 "行为" 的值**
    - `func1()` 指代函数调用后 `return `的**结果**
    - `func1` 指代函数 **本身** , 可用 `=` 复制给另一个值
    - 对 `func1` 处理 **不会**导致函数被执行
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
    - JS 准备运行脚本时, **首先寻找**全局函数声明, 并创建这些函数 (可将其视为“初始化阶段”)
    - 在处理完所有函数声明后, 代码才被执行。所以运行时能够使用这些函数
    - *函数表达式是在代码**执行到达时被创建**, 并且仅从那一刻起可用*

- 函数声明功能: **块级作用域**
    - 严格模式下, 当一个函数声明在一个代码块内(如`if`中)时, 它在该代码块内的任何位置都是可见的。但在代码**块外不可见**

## 箭头函数基础

``` javascript {.line-numbers}
let func = ( [arg1, arg2, ..., argN] ) => expression;
let sum = (a, b) => {  // 花括号表示开始一个多行函数
  ...
  return result; // 若使用了 {} , 则需要一个显式 “return”
};
```

# 代码质量


## 在浏览器中调试

> 调试 指在一个脚本中找出并修复错误的过程

### JS 补充

1. `debugger;` 写在脚本中, 在调试器中暂停代码

2. `console.log( )` 日志记录

### `Sources` 资源面板

1. `File Navigator` 区域

    - 依附于此页面的文件, 包括 Chrome 扩展程序

2. `Code Editor` 区域

    - `Breakpoints` 断点 / `Conditional Breakpoints` 条件断点
    - `Continue to here` 右键的 `context menu` (关联菜单) 中

3. `JavaScript Debugging` 区域

    - `Resume script execution` 恢复: 继续执行, 直到结束/下一个断点
    - `Step`: 运行下一条指令 (会忽略异步行为如 `setTimeout`) 
    - `Step over next function call`: 后台执行函数调用, 跳过函数内部
    - `Step into next function call`: 单步执行函数
    - `Step out of current function`: 执行到当前函数最后一行
    - `Pause on exceptions`: 开/关 出现错误时自动暂停脚本执行

4. `JavaScript Debugging` 查看

    - `Watch` 监视: 显示任意表达式的当前值

    - `Call Stack` 调用栈: 显示嵌套的调用链

    - `Scope` 作用域: 显示当前的局部/全局变量


## 代码风格

- 单行中不用 `{...}`
- indent 水平缩进 / 垂直缩进
- `;` 每一个语句后面都应该有一个分号
- **反引号 `** 允许将字符串拆分为多行
- 避免嵌套
    - 循环中可使用 `(!...) continue;` `if/else` `return` 避免嵌套
- 函数位置
    - 建议: 先写调用代码, 再写函数 (命名准确)
- 风格指南
- 自动检查器

- 注释这些
    - 整体架构, 高层次的观点。
    - 函数的用法。
    - 重要的解决方案, 特别是在不是很明显时。
- 避免注释
    - 描述“代码如何工作”和“代码做了什么”
    - 在代码足够简单或有很好的自描述性时还写没必要的注释


## 使用 Mocha 进行自动化测试

- waiting...


## Polyfill & Transpilers 


- Transpilers 转译器

    - 使用旧的语法结构 **重写** 现代语法或运算符

- Polyfills 垫片

    - 更新/添加 **新函数** 的脚本


# Object 基础知识

## Object / plain object

> [JS 有八种数据类型](##数据类型)

- 7 种原始类型: 值只包含一种 (字符串, 数字 ...)

- 1 种引用类型: 用来存储键值对和更复杂的实体

-  `literal` 字面量
    - Literals represent values in JavaScript. These are **fixed values**—not variables—that you literally provide in your script.
    - `literal` 字面量是用于表达一个固定值的表示法 (或用来为变量赋值时的常数量), 又叫常量
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
    - 其中 键 `key` **只能**是 ***`String` / `Symbol`*** 类型 , 值 `value` 可以是任何值
        - 若 `key` 中有空格则需加 `""`, 如 `"a key": ture,` 
    - 列表中的最后一个属性应以**逗号结尾**, 称尾随或悬挂逗号 (trailing/hanging comma)

2. 访问属性值
    - 使用 `.`点符号**访问**属性值(value)  `ObjectName.keyName` 
        - `.`要求`key`是有效的变量标识符: 不含空格&不以数字开头&不含特殊字符(可用`$_`)
    - 使用 `delete`操作符 **删除** 属性值 `delete Object1.key2`
    - 使用方括号 `ObjectName[keyName]` 访问属性值 `value`
        - `[]`中的 `KeyName` 可以是 **任意**表达式 , 比如变量

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
    - 少用: 若属性值为`undefined`, `in` 判断为 `ture`, 直接访问显示`undefined`

7. `"for…in"` 循环
    - 所有的 `"for"` 结构体都允许在循环中**定义变量**
        - 如 `let key in user`, `let prop in obj`
    - ``` javascript {.line-numbers}
        for ( [let] key in obj) {
        alert( key );
        alert( user[key] );
        } 
        ```

8. 遍历时的顺序
    - 规范中 ownPropertyKeys 方法定义了一个对象的遍历顺序
        1. 先将 整数属性 按 升序 排列。
        2. 再将 字符串属性 按 定义顺序 排列。
        3. 最后将 Symbol 符号属性 按 定义顺序 排列。
    - **整数属性** 指可在不做任何更改下与 *整数* 相互转换的*字符串*
        - `+0 <= parseFloat(key) < 2^32 - 1` (最大安全整数)
        - eg. `"+49" -> 49 -> "49" != "+49"`
            - `"1.2" -> 1  -> "1" != "1.2"`


## Object 引用和复制

- 赋值了对象的变量存储该对象**在内存中的地址**, 而非对象本身
    - 字符串, 布尔值等原始类型始终以"整体值"的形式被复制
    - 相比对象的根本区别之一是其"通过引用"被存储和复制的
- 使用 `const` 声明的对象**可被修改**
    - 引用对象的地址不可改(将对象作为整体), 对象的属性可以改
<br />

- 比较对象
    - 仅当两个对象为同一对象时两者才相等
    - 两个独立的对象不相等, 即使都为`{}`
    -   ``` javascript {.line-numbers}
        let a = {};
        let b = a;
        let c = {};
        alert ( a === b ); // ture
        alert ( a !== c ); // ture
        ```
- 克隆与合并, **浅拷贝** `Object.assign`
    - ``` javascript {.line-numbers}
        for(let key in user) clone[key] = user[key];
        
        Object.assign(dest, [src1, src2, src3...]) //返回dest
        ```
    - `Object.assign(目标对象, [源对象1, 源对象2...])`
        - 结果返回目标对象
        - 目标对象的相同属性会被源对象覆盖
        - 可用来合并多个对象

- 深层克隆 **深拷贝** 
    - 若对象的属性引用了其他对象, 浅拷贝不完全
    - 递归实现, 如 `lodash` 库的 `_.cloneDeep(obj)`

## 垃圾回收

- 垃圾回收是自动完成的, 不能强制/阻止执行
- Reachability 可达性
0. 当对象是可达状态时一定存在于内存中
1. 固有可达值(roots)不能被释放
    - 如: 当前执行的和嵌套调用链上的函数及其局部变量和参数, 全局变量, 等
2. 若值可通过引用/引用链从根访问任何其他值, 认为该值是可达的
    - 对外引用不重要, 只有**传入引用**才可以使对象可达(指向该对象)
    - 无**外部引用**的孤立对象(群)也视为不可达


## Object 方法, `"this"`

> 参考[You-Dont-Know-JS/this & object prototypes](https://github.com/getify/You-Dont-Know-JS/tree/1ed-zh-CN/this%20%26%20object%20prototypes)

- 作为对象属性的 函数 被称为 ***`method`*** (方法)
    - 方法简写 (首选较短的语法)
       ``` javascript {.line-numbers}
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
    - ***`"use strict"`, `this == undefined`***
    - 非严格模式的情况下, `this` 将会是 全局对象
    <br />

- 箭头函数**没有**自己的 `"this"`
    - 若箭头函数中引用 `this`, 则其值取决于外部 "正常的" 函数

## 构造器和操作符 "new"

1. 构造函数
    - 构造函数在技术上是常规函数
    1. 约定: 命名以大写字母开头
    2. **只能**由 `"new"` 操作符来执行
    <br />

2. 当函数用 `new` 操作符执行时
    1. ***`this = {};`*** (隐式创建) 
    2. 函数体执行: 通常修改 `this`, 添加新的属性等
    3. **`return this;`** (隐式返回) 
    - 立即&单次调用`new function()`
        - 创建单个复杂对象
        `let obj = new function() { ... }`
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

> `?.` 能够安全地访问嵌套属性

- `?.` 前的变量必须已声明/定义, 否则报错
- 若 `?.` 前的值为 `undefined/null` (不存在), 立即停止并返回`undefined` ("短路效应")
- `?.` 使其**前**的值成为可选值
- 其它变体：`?.()`, `?.[]`, `delete user?.name; //user存在则删除user.name`
- 可使用 `?.` 来安全地读取或删除, 但 **不能写入** (不能用在赋值语句的左侧)


## Symbol 类型

> Object 的属性 key 只能是 `String` / `Symbol` 类型

 
- `"Symbol"` 值表示唯一的标识符
    ``` javascript {.line-numbers}
    let id = Symbol(["描述/Symbol名"]);// id 是 symbol 的一个实例化对象, 是描述为 "描述 / Symbol名" 的 Symbol
    ```
- `Symbol` 保证是 **唯一** 的
    - 描述完全相同的Symbol的值也是不同
    - 描述只是一个标签, 无任何影响

- `Symbol` 不会被自动转换为字符串
    ``` javascript {.line-numbers}
    let id = Symbol("id");
    alert(id); // TypeError: Cannot convert a Symbol value to a string
    alert(id.toString()); // Symbol(id), 现在它有效了
    alert(id.description); // id, 只显示 description/描述
    ```



## Object — 原始值转换

> 所有的对象在布尔上下文（context中均为`true`

- JavaScript 运算符处理对象的方式不允许自定义
- 数学运算下对象会被自动转换为原始值进行运算并得到一个原始值



# 数据类型

- 原始类型 和 对象 之间的关键区别
    - A primitive
        - 7 种原始类型中的一种
        - `string, number, bigint, boolean, symbol, null, undefined`
    - An object
        - 能够存储多个值(包括对象, 函数)作为属性
        - 还有其他种类的对象, 如函数是对象



## 原始类型的方法

> 作为对象属性的 *函数* 被称为 ***`method`*** (方法)

- `null/undefined` 没有任何方法/属性 (访问报错)
- JS allows access to _methods and properties_ of `strings, numbers, booleans, symbols`
- 为此创建 "object wrapper" 对象包装器, 使用后即被销毁
    - 对象包装器创建包含原始数据字面量的暂时对象
    - 对象包装器使用后即被销毁
    - 对象包装器对每种原始类型都不同, 提供了不同的方法, 包括 `String, Number, Boolean, Symbol, BigInt`


## 数字类型

- 常规数字以 64-bit 的格式 IEEE-754 储存, 也称 _双精度浮点数_
- 常规整数不能安全地超过 (2^53-1) 或小于 -(2^53-1)

1. 表示数字
    - JS会忽略数字 *之间* 的 `_`(下划线)
    - 科学计数法
        ``` javascript {line-numbers}
        1.23e-6  === 1.23/1_000_000
        1.234e-3 === 1.234     //小数点移动3次
        0xff === 255           //只支持2,8,16进制
        // 0b1111 === 0o17 === 15 **不能连等!!!**
        ```
2. `.toString` 方法基础
    - 方法 `num.toString(base)` 返回在给定 _base进制_ 数字系统中 num 的 _字符串_ 表示
    ``` javascript {line-numbers}
    123456..toString(36) === '2n9c' //JS默认第一个点 . 后为小数部分
    (123456).toString(36) === '2n9c'//↑↑否则报错↑↑
    ```
3. rounding 舍入

    -  |    &nbsp;        | &nbsp;  |       `2.1 2.7 -1.2 -1.6`
        --- | --- | ---
        1. `Math.floor(num)` | 向下、小 | &nbsp;` 2 / 2 / -2 / -2 ` |
        2. `Math.ceil(num)`  | 向上/大  | &nbsp;` 3 / 3 / -1 / -1 ` |
        3. `Math.round(num)` | 四舍五入 | &nbsp;` 2 / 3 / -1 / -2 ` |
        4. `Math.trunc(num)` | 取整数   | &nbsp;` 2 / 2 / -1 / -1 ` |
    - 5. **`.toFixed(n)`** 将数字四舍五入到 n位 小数并以 string 返回
        - `12.34.toFixed(5) === '12.34000'`

4. 计算的不精确

    > 使用小数时会损失精度
    > 处理小数时避免相等性检查
    - 溢出 64位 : `1e`±`309 === `±`Infinity`
    - 二进制数字系统无法 精确 存储 0.1 (1/10) `0.1.toString(2) === '0.0001100110011001100110011001100110011001100110011001101'`
    1. 用 `.toFixed(n)` 对结果舍入
    2. 先 * 1000 再 除回 (仍有误差)

5. 检测 `isFinite()`  `isNaN()`

    - NaN 不等于**任何**事物
    - isNaN(value) 将参数转换为数字测试是否为 NaN :
        `true === isNaN(NaN) === isNaN("str")`
    - isFinite(value) 将参数转换为数字
        若不是 NaN/Infinity/-Infinity(包括string) 则返回 true
        `false == isFinite("str") == isFinite(Infinity) == isFinite(NaN)`
        可用 isFinite(value) 验证字符串
    - 在**所有**数字函数中 空字符串或仅有空格的字符串 均被视为 **`0`**

5. 补: `Object.is()` 完全相等检查内建方法
    - 适用于 NaN: `Object.is(NaN，NaN) === true`
    -  0 和 -0 不同: `Object.is(0，-0) === false`
    - 其他情况 `Object.is(a，b)` 与 `a === b` 相同

6. `pressInt()`  `pressFloat()`
    - 从字符串中"读取"数字直到无法读取, 发生 error 则返回收集到的数字
    - `parseInt` 返回一个整数, `parseFloat` 返回一个浮点数
    - 若无数字可读(参数开头非数字)则返回 `NaN`


## 字符串

### Quotes 引号

1. 字符串可以包含在 '单引号' , "双引号" , &#96;反引号&#96; 中
2. &#96;反引号&#96;
    - 反引号允许通过 `${…}` 将 _任何表达式_ 嵌入到字符串中
    - 反引号允许字符串**跨行**
    - 使用换行符 (newline character) `\n` 与 `反引号和普通换行` 创建的字符串相等(==)
3. 特殊字符/转义字符
    - 特殊字符都以反斜杠字符 `\` (backslash) 开始
    - `\'` , `\"` , `\n` , `\t` , 

### 字符串属性、方法

1. `str.length` 表示字符串长度
    ``` javascript {line-numbers}
    `\n`.length === 1; //ture, \n 是一个单独的特殊字符
    ```
2. 访问/遍历字符
    - `str[0]` 如果未找到字符则返回 `undefined`
    - `str.charAt(1)` 未找到则返回 `''` (空字符串)
    - 遍历字符串 `for..of`
    ``` javascript {.line-numbers}
    for (let char of "Hello") {
    alert(char); // H,e,l,l,o(char 变为 "H", 然后是 "e"...)
    }
    ```
3. 字符串创建后不可修改只可替换
    `TypeError: Cannot assign to read only property '0' of string 'Hi'`

4. 改变大小写
    - `str1.toLowerCase()`
    - `str2[0].toUpperCase() `

5. 查找子字符串
    
    1. `str.indexOf(substr, pos)` 
        - 从给定位置 `pos` 开始在 `str` 中查找 `substr`
        - 成功则返回匹配的位置
        - 若未找到则返回 `-1`
            - 在 `if` 中使用应检查 `-1`
        - 旧: bitwise NOT `~` 运算符 简写indexOf 检查
            - 对于 32-bit 整数，`~n === -(n+1)`

    2. `str.includes(substr, pos)` 
        - 根据 `str` 中是否包含 `substr` 来返回 `true/false`
    3. `str.startsWith()` 返回 `true/false`
    4. `str.endsWith()` 返回 `true/false`

6. 获取子字符串

    1. **`str.slice(start [, end])`**
        - 返回字符串从 `start` 到(但**不包括**)`end` 的部分
        - 若无第二个参数则运行到字符串末尾
        - `start/end` 可`<0`(为负值)
            - 起始位置从字符串结尾算起
            - 按原顺序返回
        - `start` _不能_ 大于 `end`, 否则返回 `''` (空字符串)


    2. `str.substring(start [, end])`
        - 与 `str.slice` 类似
        - `start/end` _不能_ `<0` (负值被视为 `0`)
        - `start` 可大于 `end`
            - `str.substring(2, 6) === str.substring(6, 2)`

    3. `str.substr(start [, length])
        - 返回字符串从 `start` 开始的给定 `length` 的部分
        - `start` 可为负数
            - 起始位置从字符串结尾算起
            - 按原顺序返回

7. 比较字符串

    0. `str.codePointAt(pos)` 与 `String.fromCodePoint(code)`
        1. 返回在 `pos` 位置的ASCII码
        2. 通过十进制 ASCII码 `code` 创建字符
    ``` text {line-numbers}
        字符:    0   1...8  9 ... A   B...Y  Z ... a   b...y  z
        ASCII码: 48  ....   57 .. 65  ....   90 .. 97  ....   122
    ```
    1. 调用 `str.localeCompare(str2)` 会根据语言规则返回一个整数
        - 若 `str` 在前则为负, 若 `str2` 在前则为正, 相同则为 `0` 
        - 比较按照国际化标准 ECMA-402 

8. 其他方法

    1. `str.trim()` 删除字符串前后的空格 (trims)
    2. `str.repeat(n)` 重复字符串 `n` 次


## 数组 Array

> 数组可以存储**任何**类型的元素(包括数组)

1. 声明

    - `let arr = [];` 
        - 可以在方括号中添加初始元素
        - 以逗号分隔元素、结尾 (所有行一致)
    - 少用: let arr = new Array(); (使用数字调用会创建指定长度的全`undefined`数组)

5. 数组内部

    - 数组 Array 是一种特殊的 **对象 Object**
        - `Arr[n]` 与 `obj[key]` 相同
        - 数组 Array 通过**引用**来复制
    - 判断数组
        - `Array.isArray(value)` 判断 `value` 是否为数组
        - `typeof {} === 'object'`
    - 不按照 '有序集合' 使用数组会取消针对数组的优化
        - 如添加一个非数字的属性, 存在空缺/不连续值, 以倒序填充数组

2. `length` 属性的值是数组中元素的总个数
7. 关于 `length`

    - 数组的 `length` 属性值为`最大的数字索引值+1`
    - 手动增加 `length` 增加 `undefined` 项
    - 手动减小 `length` 截断数组
    - 清空数组 `arr.length = 0;`

6. 数组循环

    1. `for`循环: arr[0] ~ arr[arr.length-1]
    2. `for..of` 只能获取元素值, 无索引
    3. 不应使用 for..in (无对应优化速度慢10-100倍!)

10. 不要使用 `==` 比较数组

    - `==` 不会对数组进行特殊处理(处理参考Object)

8. 多维数组 Multidimensional arrays 储存矩阵 matrix


## 数组方法

### 添加/移除数组元素

4. `pop`/`push`, `shift`/`unshift` 方法
    - 队列 queue 是最常见的使用数组的方法之一
    - JS 中的 Array 属于 双端队列 deque, 既可用作队列也可用作栈(允许从首/末端来添加/删除元素)
        1. 队列queue: FIFO (First-In-First-Out)
            - push shift
        2. 栈stack: LIFO (Last-In-First-Out)
            - push pop
    - 作用于数组末端的方法 (运行快速)
        1. `arr.pop()` 取出并返回数组的最后一个元素
        2. `arr.push()` 在数组末端添加(一个或*多个*)元素
    - 作用于数组首端的方法 (运行缓慢)
        1. `arr.shift()` 取出并返回数组的第一个元素
        2. `arr.unshift()` 在数组开头添加(一个或*多个*)元素

0. **`arr.splice(start[, deleteCount, elem1, ..., elemN])`**

    - 从索引 `start` 开始修改 `arr`
        1. 删除 `deleteCount` 个元素
        2. 在当前位置插入 `elem1, ..., elemN`
        3. 返回**被删除**的元素所组成的数组。
    - `deleteCount = 0` 时插入元素
    - 支持 *负向* 索引

1. `arr.slice([start], [end])`

    - 返回新**数组**, 由索引 `start` 到但*不包括* `end` 的数组项构成
    - 不带参数 `arr.slice()` 创建 `arr` 的*副本*
    - 支持 *负向* 索引

2. `arr.concat(arg1, arg2...argN)`

    - 返回一个包含来自于 `arr` 然后是 `arg1`, `arg2` 的元素的新数组
    - 若 `argN` 非数组则复制 `argN`**其自身**
        - 例外: 若类数组对象具有 `Symbol.isConcatSpreadable` 属性则当作数组来处理

### 遍历运行 forEach
``` javascript {.line-numbers}
arr.forEach(function(item, index, array) {
    // ... do something with item
    //箭头函数简化 (参数) => { 函数体 }
});
```

- 为数组的每个元素都运行一个函数
- 该函数的结果(如有返回)会被抛弃和忽略


### 在数组中搜索

- 从索引 `from` 开始搜索 `item`
    - `arr.indexOf (item, from)` 返回 `索引` | `-1`
    - `arr.includes(item, from)` 返回 `true` | `false`
    - `arr.lastIndexOf(item, from)` 除顺序从右到左外与 `arr.indexOf()` 相同 
    注意
    1. 一般只传入参数 `item` 从头开始搜索
    1. `indexOf` `includes` 都使用严格相等 `===` 进行比较
    2. `includes` 可以正确处理 `NaN` (`indexOf`查找不到)

- 寻找首个特定对象 (依次对数组中的每个元素调用函数)

    ``` javascript {.line-numbers}
    let result = arr.find(function(item, index, array) {
        // 如果返回 true，则返回 item 并停止迭代
        // 对于假值（falsy）的情况，则返回 undefined
    });
    ```
    - `arr.find()` 若函数返回 `true` 则返回 `item`, 否则返回 `undefined`
    - `arr.findIndex()` 返回找到元素的`索引值`, 否则返回 `-1`
    - `arr.findLastIndex()` 除顺序从右到左外与 `arr.find()` 相同 

- 寻找所有匹配对象(过滤数组)

    ``` javascript {.line-numbers}
    let results = arr.filter(function(item, index, array) {
        // 返回包含所有匹配元素的新数组
        // 若无匹配则返回空数组''
    });
    ```

3. 新: `arr.at(i)` 获取最后一个元素(`i`取`-1`)
    - 若 i >= 0 则与 `arr[i]` 等同
    - 若 i 为负 则从数组的尾部向前数
        - `arr[i]` 中 `i` 不能为负, 否则返回 `undefined`


### 转换/排序 数组

- `map`

    - 最有效最常用
    - 对数组的每个元素都调用函数并返回 结果数组
    ``` javascript {.line-numbers}
    let result = arr.map(function(item, index, array) {
     // 返回新值而不是当前元素
     // eg. arr.map(item => item.length);
    })
    ```

- `reduce` / `reduceRight`

    ``` javascript {.line-numbers}
    let value = arr.reduce(function(accumulator, item, index, array) {
        //eg. arr.reduce((sum, current) => sum + current, 0);
    }, [initial]);
    ```
    1. 对数组的每个元素都调用函数
    2. 其结果作为 `accumulator` 传递给下个函数
    3. 返回最后的结果
    - 第一次调用 `accumulator` 等于 `initial`
        - 若未提供 `initial` 则将首个元素作为初始值并从第二个元素开始迭代
        - 若未提供 `initial` 且数组为空则*报错*
    - `arr.reduceRight()` 除顺序从右到左外与 `arr.reduce()` 相同 

- `sort(fn)`
    - 遍历 并对数组进行 **原位 in-place** 排序 (通常忽略返回的原数组)
    - 若无参数 `fn` 则元素默认被按 _字符串_ 进行排序
    - 提供 排序函数 `fn()` 用于比较
        - 需要返回 正数 表示 大于 , 负数 表示 小于 
        - `arr.sort( (a, b) => a - b );`
    - 使用 `localeCompare` 比较特殊字符 *for strings*

- `arr.reverse();` 颠倒并返回颠倒后的数组 `arr`

- `split` `join`

    - `str.split(delim)` 
        - 通过分隔符 `delim` 将字符串分割成一个数组
        - 提供空字符串 `''` 将`str`拆分为 单字符 数组
        - 不常用: 提供第二个数字参数限制数组长度(忽略剩余字符)
    - `arr.join(glue)`
        - 使用 `glue` 将数组粘合成字符串
        - 传入 `undefined` 时效果与 `String(arr)` 相同 (以分号`;`分隔)

- 数组 `toString` 方法

    1. `String(arr)` 返回以逗号隔开的元素列表
    0. 数组没有 Symbol.toPrimitive 也没有 valueOf , 只能执行 toString 进行转换

### 方法补充: `thisArg`

- 几乎所有调用函数的数组方法都接受一个 可选的附加参数 `thisArg`
    - 如 `find`, `filter`, `map`, 除了 *sort* 是一个特例

- `thisArg` 参数的值在 `func` 中变为 `this`

    ``` javascript {.line-numbers}
    arr.find(func, thisArg);
    arr.filter(func, thisArg);
    arr.map(func, thisArg);
    // ...
    // thisArg 是可选的最后一个参数
    ```

- 常用: 可使用 *箭头函数* 替换便于理解


## Iterable object 可迭代对象

1. 迭代器 iterator

    - 迭代器的原理类似指针, 可以移动并获取其指向的元素

    0. JS规定迭代器必须实现 `next()` 接口,其返回当前元素 并 将迭代器指向下一元素
    1. 返回的格式必须为 `{done: Boolean, value: any}`
    2. 当 `done=true` 时循环结束(忽略 `value`), 否则 `value` 是下一个值
    3. `done:false` | `value:undifined` 可省略(只返回 `value: any` | `done: true`)

2. 可迭代对象 iterable object

    - 一个实现了迭代接口的对象即为可迭代对象

    1. JS的默认迭代接口/**方法**是 **`[Symbol.iterator]`**
    2. `[Symbol.iterator]` 是一个特殊的 `Symbol` 属性, 用于 _检测&制造_ 可迭代对象
    3. `[Symbol.iterator]` 是一个函数, 这个方法返回一个迭代器(包含 `next()` 的对象)
    4. 注意: 可迭代对象自身**没有** `next()` 方法 (调用 `iter[Symbol.iterator]()` 创建的 迭代器对象 包含 `next()` 方法)

3. `for..of`

    1. `for..of` 循环启动时调用 迭代方法 `[Symbol.iterator]`
    2. `[Symbol.iterator]` 返回一个 迭代器
    3. 至此 `for..of` 仅适用于这个被返回的迭代器
    4. 当`for..of` 循环需获取下一值时调用迭代器的 `next()` 方法
        5. 若 `next()` 方法返回 `done: ture` 则循环结束(忽略 `value`)
        6. 否则(代表 `done: false`) `value` 为下一个值 



## Map and Set 映射和集合

> `Map` 对象保存键值对, 任何值(**包括对象**)都可以作为 `key / value`
- 普通的 `Object` 会将 key 转成字符串
- `Map` 会保留 `key` 的类型(包括 `NaN`)
    - `Map` 比较键是否相等类似 `===`(区别是 `NaN` 视作与 `NaN` 相等)

### Map 方法和属性

0. 禁止通过 map[key] 使用 Map (会被视为 plain object 并有限制)

1. `new Map()` 创建 map

    - 可传入带有键值对的数组(或其它可迭代对象)进行初始化
        ``` javascript {.line-numbers}
        // 键值对 [key, value] 数组
        let map = new Map([
        [ '1', 'str1'],
        [   1, 'num1'],
        [true, 'boo1']
        ]);
        ```

2. `map.set(key, value)` 根据 key 存储 value
    - key 值唯一, 重设同一 key 会覆盖原 value
    - 链式调用: 每次 `map.set` 调用都会返回 map 本身

3. `map.get(key)` 根据 key 返回 value, 不存在则返回 undefined

4. `map.has(key)` 根据 key 存在与否 返回 true/false 

5. `map.delete(key)`根据 key 删除对应的键值对

6. `map.clear()` 清空 map 内的键值对

7. `map.size` —— 返回当前元素个数

### Map 迭代

0. 迭代的顺序与插入值的顺序相同 (保留顺序)
1. `map.keys()` 遍历并返回一个包含所有 key 的可迭代对象
2. `map.values()` 遍历并返回一个包含所有 value 的可迭代对象
3. `map.entries()` 遍历并返回一个包含所有实体 [key, value] 的可迭代对象
    - `for..of` 在默认情况下使用的方法

4. `forEach` 遍历调用
    ``` javascript {.line-numbers}
    // 对每个键值对 (key, value) 运行 forEach 函数
    recipeMap.forEach( (value, key, map) => {
    alert(`${key}: ${value}`); // cucumber: 500 etc
    });
    ```

### Map 与 plain object 

1. `Object.entries(plain_obj)` 返回对象的 键/值对(`[key, value]`) 数组 
    - 将其作为参数传入 `new Map()` 即从 `plain_obj` 创建 `Map`
    - 调用 `map.entries()` 将返回一个可迭代的 键/值对

2. `Object.fromEntries()` 根据给定的具有 `[key, value]` 键值对的数组创建对象
    - 根据 `map` 创建一个 `plain_obj`: `Object.fromEntries(map.entries())` `==` `Object.fromEntries(map)`
        - `Object.fromEntries` 期望参数为一个可迭代对象, 不一定是数组
        - `map` 的标准迭代会返回跟 `map.entries()` 一样的键/值对

### Set

> `Set` 是值的集合(没有键), 其每一个值只能出现一次

### Set 方法

1. `new Set(iterable)` 创建 `set`
    - 若提供了一个 iterable 对象(通常是数组) 则从数组里面复制值到 `set` 

2. `set.add(value)` 向 `set` 添加值 并 返回 `set` 自身
    - 使用**同一个** `value` 调用 set.add(value) 无作用
    - `Set` 内部对唯一性检查进行了更好的优化(优于 arr.find 的遍历)

3. `set.delete(value)` 删除值 且根据方法调用的时候是否存在 `value` 返回 `true`|`false`

4. `set.has(value)` 根据 `value` 是否在 `set` 中返回 `true`|`false`

5. `set.clear()` 清空 `set`

6. `set.size` 返回元素个数

### Set 迭代

- 可以使用 `for..of` 或 `forEach` 来遍历 `Set`

``` javascript {.line-numbers}
let set = new Set(["oranges", "apples", "bananas"]);

for (let value of set) alert(value);

// 与 forEach 相同：
set.forEach((value, valueAgain, set) => { // 三个参数: value,同一个value,目标对象
  alert(value);
});
```
- `forEach` 的回调函数有三个参数，是为了与 `Map` 兼容

- 用于迭代 `Map` 的方法同样适用于 `Set` 

1. `set.keys()` —— 遍历并返回一个包含所有值的可迭代对象，

2. `set.values()` —— 与 `set.keys()` 作用相同，这是为了兼容 `Map`

3. `set.entries()` —— 遍历并返回一个包含所有的实体 `[value, value]` 的可迭代对象，它的存在也是为了兼容 Map。















<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
<hr>
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>










## 字符串





## 数组





## 数组方法





## Iterable object（可迭代对象）





## Map and Set（映射和集合）





## WeakMap and WeakSet（弱映射和弱集合）





## Object.keys, values, entries





## 解构赋值





## 日期和时间





## JSON 方法, toJSON


























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