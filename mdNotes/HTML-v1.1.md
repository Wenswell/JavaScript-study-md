> [Web 前端开发者 - 学习 Web 开发 | MDN](https://developer.mozilla.org/zh-CN/docs/Learn/Front-end_web_developer)

# HTMLing

> Hypertext Markup Language, HTML (超文本标记语言) 是一种用来结构化 Web 网页及其内容的标记语言

## HTML 入门 文件相关

> HTML标签对 大小写 不敏感, **但**多数计算机(服务器)区分大小写 (`<!DOCTYPE html>`之外**全部小写**)

> 文件名中应使用**连字符 `-`**, 搜索引擎把连字符当作单词的分隔符, 但不会识别下划线

### 网站最基本、最常见的结构
  1. `index.html` : 一般包含主页内容 (homepage content)
  2. `images` folder : 包含站点中的所有图像
  3. `styles` folder : 包含站点所需样式表
  4. `scripts` folder : 包含提供站点交互功能的 JS 代码

### 文件被浏览器解析的顺序
  1. 解析 HTML 并识别所有 `link` `script` 元素及指向的外部文件的链接
  2. 同时根据链接向服务器发送请求, 获取并解析 `CSS` `JavaScript` 文件
  3. 给解析后的 HTML/CSS 文件生成一个 DOM/CSSOM 树（在内存中）, 并且会编译和执行解析后的 JavaScript 文件
  4. 伴随着构建 DOM 树、应用 CSSOM 树的样式及执行 JavaScript 文件, 在屏幕上绘制出网页的界面
  5. 用户看到网页界面时即可与网页交互


## URL 入门

> HTTP中, `URL` 被称为 `Web address` 或 `link`

### `URL`: Uniform Resource Locator, 统一资源定位器

> `URL` 可指向可在网络上保存的任何内容, 若浏览器不知道如何显示或处理文件, 则会询问是否要打开/下载文件
- URL 基本结构
    **`协议`** `://` **`主机名`** `/` **`路径`**
1. 协议： 包括 https, ftp, mailto(mailto后只接`:`) 等
2. 主机名
3. 路径: 包含可选的 (n个)目录 / (1个)文件名
    - 若URL只以 目录结尾, 则指向该目录中的默认文件
    - 通常服务器的默认文件为 `index.html`


### absolute URL versus relative URL

1. `absolute URL` 绝对链接: 
    - 指向由其在Web上的绝对位置定义的位置
    - 包括 protocol(协议), domain name(域名)
2. `relative URL` 相对链接: 
    - 指向与所链接文件相关的位置 
- 用 相对URL 指向工作目录:
    - 无前缀 默认指向当前目录
    - 无前缀 直接索引下级目录
    - 前缀 `../` 指向上一级目录
    - 前缀 **`/`** 指向 **根目录** (根相对 URL)


### URL 使用注意点:

- **补全**末尾的正斜杠 `/`
    - `href="` `http://www.example.com` `"` 会产生二次HTTP请求
    - `href="` `http://www.example.com` `/` `"` 末尾需补上 `/` 
- 简洁: 链接的显示文本中不要包含 URL, 链接(到) 等字样
- 保持链接尽可能*短*
- 尽可能使用**相对链接**
    - 使用 相对URL 更有效率
    - 访问 绝对URL 时需先通过 DNS 查找 IP地址
- 链接到 非HTML资源 时留下清晰的指示
    - 如 `(PDF, 10MB)`


## HTML Element / 元素概览

- HTML 元素指 `开始/开放标签 + 元素内容 + 结束/闭合标签` 的所有代码
    - (`start/Opening tag` + `Element Content` + `end/Closing tag` )

- Nesting elements / 嵌套元素
    - 将一个元素置于其他元素之中称作**嵌套**
    - 注意正确地开始和结束

- Empty elements / 空元素
    - 不包含任何内容的元素称为空元素

- Metadata: the meta element 
    - metadata 元数据是用来描述数据的数据


- `<a>`元素 / anchor element / 锚元素 
    - `<a>` 可包括属性:
    1. `href=""` 声明超链接地址
    2. `title=""` 悬停时显示的信息
    3. `target=""` 指定如何呈现链接
    - 默认(无`target`属性)当前页面, `target="_blank"`跳转新标签页


## HTML Attribute / 属性

- 属性包含 HTML 元素的一些额外信息
- 属性总在元素的开始标签(start tag)中规定
- 属性主要6部分: ` ` `attribute name` `=` `"` `attribute value` `"`
    - 单双引号不可混用, 可嵌套使用(在字符串中显示引号)
    - *不建议* : 不含 ASCII 空格（及 `"` `'` ` = < >` ）的简单属性值可不加引号

### 常用属性
Attribute|Value|description
--|--|--
`class`|*classname*|规定元素的类名(classname)
`id`|*id_value*|规定元素的唯一 id (区分大小写)
`style`|*style_definition*|规定元素的行内样式(inline style)
`title`|*text*|规定元素的额外信息(可在工具提示中显示)


### Boolean attributes / 布尔属性
- 没有值的属性, 只能有**与属性名一样**的属性值
- eg. 
    - `disabled` / `disabled="disabled"` (标记表单输入使之变为不可用)
    - `required` 设置表单为必填项

### Deprecated 废弃属性 

- 在 HTML 4 中, 有若干的标签和属性是被废弃的。被废弃(Deprecated)的意思是在未来版本的 HTML 和 XHTML 中将不支持这些标签和属性

-使用 `<style>` 代替: ~~align, bgcolor, color~~



# HTML 文档

## HTML 文档概述

``` html {.line-numbers}
<!DOCTYPE html>
<html>

  <head>
    <meta charset="utf-8">
    <title>测试页面</title>
  </head>

  <body>
    <img src="images/firefox-icon.png" alt="测试图片">
  </body>

</html>
```

- `<!DOCTYPE html>` 是最短有效的文档声明

- `<html></html>`: `<html>`之间的文本描述网页, 是一个**根元素**

- `<head></head>`: `<head>`元素是一个**容器**, 其内容包含在HTML页面中但不会被显示
  - 如: 在搜索结果中出现的关键字和页面描述, CSS样式, 字符集声明等

- `<meta charset="utf-8">`: 设置文档使用`utf-8字符集`编码(1Byte 8bit)

- `<title></title>`: 设置页面标题, 出现在浏览器标签上, 标记/收藏页面时可用来描述页面

- `<body></body>`: `<body>`之间的文本是可见的页面内容


### 文档编写注意

1. HTML中的空白

    - 当渲染代码时HTML解释器会将连续出现的空白字符减少为一个单独的空格符

2. 实体引用 / Entity references: 在HTML中包含特殊字符

    - Character reference 每个字符引用以符号`&`开始, 以分号`;`结束.
    -   原义字符 | 等价字符引用
        --------|-----------
          `<`   | `&lt;`
          `>`   |	`&gt;`
          `"`   |	`&quot;`
          `'`   |	`&apos;`
          `&`   |	`&amp;`
    - 参考: [HTML字符实体引用的列表](https://en.wikipedia.org/wiki/List_of_XML_and_HTML_character_entity_references)

3. HTML comments / 注释
  `<!--  -->`



## HTML `CSS` 

1. 外部样式表 
``` html {.line-numbers}
<head>
    <link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

2. 内部样式表
``` html {.line-numbers}
<head>
    <style type="text/css">

        body {background-color: blue}

    </style>
</head>
```

3. 内联样式
<p style="color: red; margin-left: 80px">This is a paragraph</p>
``` html {.line-numbers}
<p style="color: red; margin-left: 80px">
This is a paragraph
</p>
```

- 用 `<link>` 元素 引入 CSS 文件 
    - `<link rel="stylesheet" href="my-css-file.css">`


## HTML `JavaScript`
-  用 `<script>` 元素 引入/添加 JavaScript
    - `<script src="my-js-file.js"> </script>`
    - `src`引入的脚本会覆盖 `script` 内部的脚本 (同时存在)
- `<noscript>` 标签定义了替代内容 在浏览器中禁用了脚本或浏览器不支持脚本 时会显示



## HTML `<head>` / 头部元素

> 与 `<body>` 元素不同, `<head>`不会在浏览器中显示. 其作用是保存页面的一些元数据


### `<* lang="">` 设定主语言

1. 总体: `<html lang="zh-CN">`
2. 局部: 用`<span lang="jp"> </span>` 包裹要设定的部分


### `<meta>` : 添加元数据

- 元数据就是描述数据的数据
- 许多 `<meta>` 元素包含了 `name` 和 `content` 特性

1. 指定字符编码 `<meta charset="utf-8">`

2. 增加自定义图标 `<link rel="shortcut icon" href="favicon.ico" type="image/x-icon">`

3. 添加作者和描述 (搜索引擎搜索结果显示)
    ``` html {.line-numbers}
    <meta name="author" content="Author Name">`
    <meta name="description" content="Description Content">`
    ```

4. 许多` <meta>` 特性已经不再使用。 例如, keyword `<meta>` 元素
5. 部分大型网站有专有元数据


### `<title>` : HTML文档标题
- 不可或缺
- 是一项*元数据*, 用于表示整个 HTML 文档的标题
    - 显示在标签页的标签中
    - 显示在收藏页面时的建议名称中
    - 显示在搜索结果中 (超链接的文本显示)

### `<base>` : 规定默认地址/目标

- `<base />`标签为页面上的所有链接规定默认地址或默认目标(target)
- 属性 `href=""` 规定默认链接
- 属性 `target="_blank"` 规定链接默认在另一标签页打开


### `<link>` : 定义外部资源

- `<link />`最常用于连接样式表
    ``` html {.line-numbers}
    <head>
        <link rel="stylesheet" type="text/css" href="mystyle.css" />
    </head>
    ```


### 引入/添加 CSS / JavaScript

1. `<style>` 添加 CSS **语句**
2. `<script>` 引入/添加 JavaScript


## HTML `<body>` 容器

> 全球色盲患者比例: 4%, 视力受损人口比例: 9.4亿 / 13% (2015)

> [HTML 验证](https://validator.w3.org/)


### `<header>` 页眉

- 简介形式的内容
- 若为 `<body>`子元素, 则是网站的全局页眉
- 若为 `<article>` `<section>`子元素, 则为这些部分特有的页眉


### `<nav>` 导航栏

- 包含页面主导航功能
- 通常使用列表构建


### `<main>` 主内容

- 可包括子内容区段如`<article>` `<section>` `<div>` 等
- 存放每个页面独有的内容, 单页面单个 `<main>`
- `<main>` 应直接位于 `<body>` 中 (无嵌套)


### `<article>` 创建'文章'

- `<article>` 元素表示文档、页面、应用或网站中一个独立的容器, 
- 原则上是可独立分配或可再用的
- 一个`<article>`可以包含一个或多个`<section>`元素

- eg. 帖子、文章、一则用户提交的评论、一个交互式的小部件或小工具, 或者任何其他独立的内容项


### `<section>` 定义区块

- 适用于组织页面使其按功能分块 (节是有主题的内容组, 通常具有标题)
- 若只为添加样式而对内容添加一个容器, 应使用 `<div>` 而不是 `<section>`
- 区别: `<section>` 在本质上组织性和结构性更强, 而 `<article>` 代表自包含的容器


### `<aside>` 附注栏

- 包含一些间接信息 (侧栏, 术语条目, 作者简介, 相关链接, nav元素组(如博客的友情链接), 广告, 相关产品列表等)
- `<aside>` 常放在 `<main>` 之后 ? (重点排前)
- 与内容有关的图像使用 `<figure>`而非 `<aside>` 
- HTML5不允许将aside嵌套在address元素内

### `<footer>` 页脚

- 代表嵌套其最近的元素的页脚 (若是 body 则为全局页脚)

-  `<footer>` 中不能嵌套 `<header>` 或另一个 `<footer>`
-  `<footer>` 不能被嵌套在 `<header>` 或 `<address>` 元素中


### `<figure>` 图片标题

- `<figure>` 组合图片和标题
- `<img>` 定义图像, `<figcaption>` 定义标题。
- `<figcaption>` 非必需, 如果包含则必须是figure元素内嵌的第一个或最后一个元素
``` html {.line-numbers}
<figure>
    <img src="pic_mountain.jpg" alt="The Pulpit Rock">
    <figcaption>Fig1. - The Pulpit Pock, Norway.</figcaption>
</figure> 
```

### 通用容器 / 无语义(Non-semantic)元素
- `<div>` 块级(block)无语义元素, 定义文档中的分区或节(division/section)
- `<span>` 内联的(inline)无语义元素, 用来组合文档中的行内元素


## 其他元素

### 进度条 meter process

1. `<meter>` 元素

    - 可以用meter元素表示分数的值或已知范围的测量结果
    - 浏览器会自动显示测量值, 并根据属性值进行着色
    - meter 并**不用于**标记没有范围的普通测量值如高度、宽度、距离、周长等
    
    ``` html {.line-numbers}
    <p>Project completion status: <meter value="0.80">80% completed</meter> </p>
    <p>Car brake pad wear: <meter low= "0.25" high="0.75" optimum="0" value="0.5">21% worn</meter></p>
    <p>Miles walked during half-marathon: <meter min="0" max="13.1" value="5.5" title="Miles">4.5</meter></p>
    ```
    <p>Project completion status: <meter value="0.80">80% completed</meter> </p>
    <p>Car brake pad wear: <meter low= "0.25" high="0.75" optimum="0" value="0.5">21% worn</meter></p>
    <p>Miles walked during half-marathon: <meter min="0" max="13.1" value="5.5" title="Miles">4.5</meter>

    1. `value` 是唯一必需包含的属性
    2. 默认 `min="0"` `max="1.0"` 
    3. `low` `high` `optimum` 
        - 三个属性通常共同作用, 将范围划分为低、中、高三个区间(颜色不同)
        - `optimum` 代表范围内的最优位置

2. `<progress>` 元素

    - `<progress>` 用来表示 "任务的完成进度"
    - `progress` 支持三个可选的属性: `max` `value` `form`
        1. max 属性指定任务的总工作量, 其值必须 > 0
        2. value 是任务已完成的量
        3. 如果progress没有嵌套在form元素里面, 又需要将它们联系起来, 可以添加form属性并将其值设为该form的id


### 旁注标记 ruby annotation

> 旁注标记通常用于表示生僻字的发音, 这些小的注解字符出现在它们标注的字符的上方或右方. 它们常简称为旁注 (ruby或rubi)

- `ruby` 及其子元素 `rt` `rp` 是HTML5中为内容添加旁注标记的机制
- `rt` 指明对基准字符进行注解的旁注字符. 
- 可选的`rp`元素用于在不支持 ruby 的浏览器中的旁注文本周围显示括号. 
``` html {.line-numbers}
<ruby>
北      <rp>(</rp>   <rt>ㄅㄟˇ</rt>      <rp>) </rp>
京      <rp>(</rp>   <rt>ㄐㄧㄥ</rt>     <rp>) </rp>
</ruby>
```


### 书写顺序  bdi bdo

> 除非在html元素中添加dir属性并将属性值设为rtl, 否则内容的基准方向都默认为从左至右。



## 添加额外属性

### 地标角色 role

1. role="banner" (横幅) 
    - 面向全站, 添加到页面级的`header`, 每个页面只用一次
2. role="navigation" (导航) 
    - 文档内不同部分或相关文档的导航性元素 (通常为链接) 的集合
    - 与`nav`元素是对应关系. 应将其添加到每个nav元素, 或其他包含导航性链接的容器. 
    - 这个角色可在每个页面上使用多次, 但是同 `nav` 一样, 不要过度使用该属性
3. role="main" (主体) 
    - 与`main`元素是对应关系. 最好将其添加到main元素, 也可以添加到其他表示主体内容的元素 (可能是div) . 在每个页面仅使用一次
4. role="complementary" (补充性内容) 
    - 与`aside`元素是对应关系. 应将其添加到aside或div元素 (前提是该div仅包含补充性内容) . 可以在一个页面里包含多个complementary角色, 但不要过度使用
5. role="contentinfo" (内容信息) 
    - 包含关于文档的信息的大块可感知区域
    - 这类信息的例子包括版权声明和指向隐私权声明的链接等
    - 将其添加至整个页面的页脚 (通常为`footer`元素) . 每个页面仅使用一次


### class / id

- 添加在元素的开始标签中 `id="name"`
    - `name`是唯一标识该元素的名称
    - `name`几乎可以是任何字符, 只要不以数字开头且不包含空格

- 添加在元素的开始标签中 `class="name"`
    - 其中name是类别的名称
    - 用空格将不同的类别名称分开, 指定多个类别 `class="name1 name2"`

- 注意
    - 通常使用短横线分隔多个单词



### title 属性

- 使用 title**属性** (非`<title>`) 为网站上任何部分加上提示标签
- 鼠标指向加了说明标签的元素时, 就会显示 title
    - 使用title可以提升无障碍访问功能


## HTML内容 - text

> HTML 的主要工作是编辑文本结构和文本内容 (也称为[语义 semantics](https://developer.mozilla.org/zh-CN/docs/Glossary/Semantics))


### 换行与水平分割线

1. `<br />` 换行 line break
2. `<wbr>` 代表  "一个可换行处"
2. `<hr />` 水平分隔线 Horizontal Rule
    - 表示段落级元素之间的主题转换


### 标题/段落 heading/paragraph

> 搜索引擎使用标题为网页的结构和内容编制索引

1. `<p>` paragraph content `</p>` : 定义单个段落 

2. `<h1>` the main heading `</h1>` : 定义标题

    - `<h1>` the main heading, `<h2>` subheadings, `<h3>` sub-subheadings

3. 使用注意点: 
    1. 单页面 **单个`<h1>`**
    2. 层次结构的顺序正确 (不逃过某一级)
    3. 尽量只使用 `<h1>` `<h2>` `<h3>`
    4. 副标题不使用 <h*> 标记


### 列表 Lists

0. `<li>`: list items

1. 无序 Unordered lists
    - 可使用属性 `type=""` 改变项目符号
    - disc实心圆, circle空心圆, square实心正方
    ``` html {.line-numbers}
    <ul>
        <li>lists items1</li>
        <li>lists items2</li>
    </ul>
    ```

2. 有序 Ordered lists 
    - 可使用属性 `type=""` 改变项目符号
    - A/a 字母顺序, I/i 罗马字母顺序
    ``` html {.line-numbers}
    <ol>
        <li>lists items1</li>
        <li>lists items2</li>
    </ol>
    ```
- 无序/有序 列表之间可以嵌套

3. 描述 Description lists

    - 用于标记一组项目及其相关描述. 如术语&定义, 问题&答案等
    - 默认会在描述列表的描述部分(description definition)和描述术语(description terms)之间产生缩进
    - 
        ``` html {.line-numbers}
        <dl>
            <dt>description term1</dt>
                <dd>description definition1</dd>
            <dt>description term2</dt>
                <dd>description definition2</dd>
                <dd>description definition3</dd>
        </dl>
        ```

### 表格 table

> 表格table, 单元格cell, 行row, 列column
``` html {.line-numbers}
<table border="1">
    <caption>Table Caption</caption>
    <tr>
        <td>row 1, cell 1</td> <td>row 1, cell 2</td>
    </tr>
    <tr>
        <td>row 2, cell 1</td> <td>row 2, cell 2</td>
    </tr>
</table>
```
<table border="1">
    <caption>Table Caption</caption>
    <tr>
        <td>row 1, cell 1</td> <td>row 1, cell 2</td>
    </tr>
    <tr>
        <td>row 2, cell 1</td> <td>row 2, cell 2</td>
    </tr>
</table>
1. 表格标签

    1. `<table>` 标签 定义表格
        - 使用属性 `border=""` 添加边框
    2. `<tr>` 定义单行 
        - The Table Row element
    3. `<th>` 定义表头(行或列)
        - `<th>`与`<td>` 平级
        - 默认加粗居中
    4. `<td>` 定义一行中单个单元格 
        - The Table Data Cell element
    5. `<caption>` 定义表格的标题
        - **无关**代码位置, 都居中显示在整个表格上方
        - The Table Caption element

    - 注意点: 若单元格为空, 部分浏览器无法显示其边框, 可用占位符 `&nbsp;` 填充 (默认忽略单元格首位空字符)
<br />

2. 表格属性 for `<td>` / `<th>`
    1. 跨(span)行或跨列
        - 添加属性 `colspan="num"` / `rowspan="num"` 
        - `num` 即为需要 跨行 / 跨列 的数量
        ``` html {.line-numbers}
        <table border="1">
            <tr>
                            <th> 姓名 </th> <td> Bill Gates </td>
            </tr>
            <tr>
                <td rowspan="2"> 电话 </td> <td> 555 77 854 </td>
            </tr>
            <tr>
                /*此处上方的单元格跨列占用*/  <td> 555 77 855 </td>
            </tr>
        </table>
        ```
    2. 文字排列
        - 添加属性 `align="way"`
        - `way` 可为: left / center / right

<br />
3. 表格属性 for `<table>`


### 重点 / 强调 / 突出显示

1. Emphasis / 强调

    - 在口语表达中强调某些字
    - 用 `<em>`(emphasis) 元素 标记
    - 默认风格为*斜体*

2. Strong importance / 非常重要

    - 强调重要的词
    - 用 `<strong>`(strong importance) 元素标记
    - 默认风格为**粗体**

- 强调之间可嵌套 (***加粗倾斜***)

3. `<mark>`

    - mark最常见的使用场合是在搜索结果页面
    - 默认加上黄色背景


### 插入 / 删除

1. 插入内容 `<ins>` 默认添加下划线样式

2. 删除内容 `<del>` 默认添加删除线样式



### 展示代码

- `<code>` 标记 通用代码 **不保留**多余的空格和折行

- `<pre>` 保留空白字符+等宽字体 (通常用于代码块)

    - 如要显示包含HTML元素的内容, 应将包围元素名称的`<`,`>`分别改为其对应的字符实体`&lt;`,`&gt;`(&lt;`,`&gt;)

- 其他计算机相关元素：kbd、samp和var
    - `<var>` 用于标记具体变量名
    - `<kbd>`: 用于标记输入电脑的键盘(或其他类型的)输入
    - `<samp>`: 用于标记计算机程序的输出


### old - 表象元素 presentational elements

- 不建议: 表象元素: 仅影响表象而 **没有语义**
- 已不使用: 如 ~~`<b>, <i>, <u>, <s>`~~



## HTML 标注、引用和定义元素

### 引用 quote

1. 块引用 `<blockquotes>`
2. Inline quotation `<q>`
    ``` html {.line-numbers}
    <blockquote cite=""> </blockquote>
    <q cite="" lang="xx" > </q>
    ```
- 引用元素中的 `cite=""` 属性内容 **不**被浏览器显示, **不**屏幕阅读器阅读
    - 只可借助 JS 或 CSS 显示出来
    - 搜索引擎可以通过此属性获取关于引文的更多信息
- 可使用 `<a href="">` `<cite></cite>` `</a>` 标注引用来源及链接
    - `<cite>` 元素默认 *斜体* 显示
- `lang="xx"` 用于判断需要使用的引号的类型(英语为“”, 而很多欧洲语言则为«»), 但浏览器对引号的呈现方式可能不同

### 引用标题 `<cite>`  

- `<cite>` 元素定义著作的标题
- 默认斜体显示
- 区分 引用中的属性 `cite=""` 


### 标记时间日期

- 将时间和日期标记为可供机器识别的格式
- 若`<time>`标签中格式正确,可不使用`datetime`属性
- 不可相互嵌套(两个`<time>`)
- 若无`datetime`, `<time>`标签中只能包含文本

- 有效的时间格式
    - **必须** 补全位数(补`0`) `2022-03-04T00:01+08:00`
    - 时间: `YYYY-MM-DDThh:mm:ss`
    - 时间段: `nh nm ns`
    - 全球时间及时差: `1985-11-03T17:19:10Z`/`1985-11-03T17:19:10-03:30`
-   ``` html {.line-numbers}
    <time datetime="2016-01-20T19:30+01:00">7.30pm, 20 January 2016 is 8.30pm in France</time>
    ```


### 缩略语 Abbreviation

- 括号提供缩写词的全称(第一次出现)是解释缩写词最直接的方式
- 移动设备可能无法移到abbr元素上查看title的提示框

``` html {.line-numbers}
<abbr title=""> </abbr>
```
1. 只在添加 `title=""` 之后, `<abbr>` 元素才有 点下划线 效果
2. 鼠标悬停时显示 `title=""` 中的内容
3. `title=""` 中的 非首位 空白字符可被识别并显示


### 定义术语 dfn
- dfn元素及其定义必须挨在一起, 否则便是错误的用法
- 通常, dfn元素默认以斜体显示, 与cite一样


### 标记联系信息 `<address>`

- 用以定义与 HTML 页面或页面一部分(如一篇报告或新文章)有关的作者、相关人士或组织的联系信息
- 包括电子邮件地址、指向联系信息页的链接等信息
- 默认 ***斜体***
    ``` html {.line-numbers}
    <address> </address>
    ```


### 上下标 Superscript subscript

1. 上标 `<sup> </sup>` 
2. 下标 `<sub> </sub>`



## HTML内容 -- 图片

### 常用图片类型
格式|支持色彩|索引色透明|alpha透明
--|--|--|--
JPEG|>1600万|—|—
PNG-8|256|支持|支持
PNG-24|>1600万|支持|—
PNG-32|>1600万|—|支持
GIF|256|支持|—
- **动画**可借助 CSS动画、JavaScript、HTML5 Canvas、SVG 等来实现(而非GIF)
- 图标类应选择 `PNG-8` 而非GIF (非动图)
- 索引色透明: `0 / 1` ; α透明: `[0,1]`


### `<img />` 标签定义 HTML 图像
1. `<img>`为空标签(自闭合)
2. 基础语法:  `<img` `src=""` `alt=""` `/>`
 - `<map>` 定义图像地图

### `<img>` 标签属性
- 包括: src alt align 
1. 源属性 `src` 的值是图像的 URL 地址
2. 替换文本属性 `alt` 为图像定义一串预备的可替换的文本
    - 当浏览器无法载入图像时显示 `alt` 中的内容
4. `align` 定义 图片 相对于 文字 的位置

### 图像尺寸

- `width` `height` 属性值定义图片高宽(应该添加)
1. 始终定义图像尺寸: 这样做会减少闪烁, 因为浏览器会在图像加载之前为图像预留空间
2. PC设备使用原始分辨率(不拉伸), 移动设备适当缩小图片(屏幕分辨率更高)

### 网站图标 favicon

- 各个地方(选项卡,历史记录,书签..)显示的小图标为favicon,即 favorites icon (收藏夹图标) 的简称
- 通常保存为 `ICO` 格式, 文件名为 `favicon.ico`
- 图标尺寸至少为 16*16
- 苹果规定: iPhone 图标大小为 57×57 或 114×114, iPad 图标大小为 72×72 或 144×144 (对于Retina显示屏)
- 将(一个或多个)图标图像放在网站的**根目录**里, 浏览器会自动寻找并显示
- 若不在根目录, 则需要用 `<link>` 元素引入


## HTML 超链接 / hyperlinks

- 链接主要包括目标(destination)和标签(label)
- 目标(destination)指定点击链接时发生什么
    - 最常见的是连接到其他网页的链接
    - 其次是连接到其他网页特定位置 (称为锚anchor) 的链接
- 标签(label)即在浏览器中看/听到的内容, 激活标签即到达链接目标

### `<a>` 超链接元素

``` html {.line-numbers}
<a href="" title="" rel=""> </a>
```
1. 用 `<a> </a>`元素包裹内容(包括**块级**元素)创建链接
2. 用 `href=""`属性(Hypertext Reference) 添加指向的地址
3. 用 `title=""`属性添加支持信息(悬停显示)
    - 注意: title仅当悬停时才显示, 只用于补充信息
4. [`rel` 属性](http://microformats.org/wiki/existing-rel-values)指定当前文档与链接文档之间的关系
    - 仅在存在`href`属性时使用`rel`
    - 搜索引擎使用此属性获取有关链接的更多信息
    - eg. `rel="external"` 指示所引用的文档与当前文档不在同一站点


### 创建并链接到锚anchor

- 跳至(当前或特定)网页的特定区域
- 先给元素分配 `id` 属性 eg. `id="id_Name"`
``` html {.line-numbers}
<a href = "[tagDOC.html]#id_Name">...
```
- 注: 旧版本可/只可使用 `name` (旧版 `id`)



### 电子邮件链接
``` html {.line-numbers}
<a href = "mailto:[example@abc.com][?]">...
<a href = "mailto:exp@abc.com?cc=a1@b.com&cc=a2.b.com&subject=The%20subject%20of%20the%20email&body=The%20body%20of%20the%20email">...
```
- 若无邮件地址, 邮件窗口仍会被打开
- 使用 `?` 分隔 主URL 与 参数值 
- 使用 `&` 分隔 `mailto:` 后的各个参数
- 常用: 主题(`subject`)、抄送(`cc`)和主体(`body`)
- 每个字段的值**必须**是URL编码的, 不能有非打印字符 (如制表符、换行符、分页符) 和空格


### 电话号码链接
`<a href="tel:+18001234567">1 (800) 123-4567</a>`



### 下载链接 `download` 属性

- 使用 `download = ""`提供一个默认的保存文件名
- `download`属性仅适用于**同源URL**
    - 同源(Same-origin)URL  的 protocol、port(若指定)和 host 都相同




## HTML 响应式 Web 设计

- RWD, Responsive Web Design, 指的是响应式 Web 设计
- RWD 能够以 **可变尺寸** 传递网页
- RWD 对于平板和移动设备是必需的



## BackToEnd


<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
<br />
``` html {.line-numbers}
```



``` html {.line-numbers}




```


``` html {.line-numbers}





```


``` html {.line-numbers}








```