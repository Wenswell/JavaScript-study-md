# HTML 入门

## 文件相关

- 文件名中应使用连字符 `-`, 谷歌搜索引擎把连字符当作单词的分隔符, 但不会识别下划线.

- 网站最基本、最常见的结构
  1. `index.html` : 一般包含主页内容 (homepage content)
  2. `images` folder : 包含站点中的所有图像
  3. `styles` folder : 包含站点所需样式表
  4. `scripts` folder : 包含提供站点交互功能的 JS 代码

- 文件被浏览器解析的顺序
  1. 解析 HTML 并识别所有 `link` `script` 元素及指向的外部文件的链接
  2. 同时根据链接向服务器发送请求, 获取并解析 `CSS` `JavaScript` 文件
  3. 给解析后的 HTML/CSS 文件生成一个 DOM/CSSOM 树（在内存中）, 并且会编译和执行解析后的 JavaScript 文件
  4. 伴随着构建 DOM 树、应用 CSSOM 树的样式及执行 JavaScript 文件, 在屏幕上绘制出网页的界面
  5. 用户看到网页界面时即可与网页交互

# HTML 基础

> Hypertext Markup Language, HTML (超文本标记语言) 是一种用来结构化 Web 网页及其内容的标记语言

## HTML Element / 元素

- HTML Element 主要部分

  - `Opening tag` + `Content` + `Closing tag` (开始/结束标签 + 内容)

- HTML Attribute / 属性

  - 属性包含元素的一些额外信息
  - 属性主要6部分: ` ` `attribute name` `=` `"` `attribute value` `"`
  - *不建议* : 不含 ASCII 空格（及 `"` `'` ` = < >` ）的简单属性值可不加引号
  - 单双引号不可混用, 可嵌套使用(在字符串中显示)

- Boolean attributes / 布尔属性

  - 没有值的属性, 只能有**与属性名一样**的属性值
  - eg. `disabled` / `disabled="disabled"` (标记表单输入使之变为不可用)

- Nesting elements / 嵌套元素

  - 将一个元素置于其他元素之中称作**嵌套**
  - 注意正确地开始和结束

- Empty elements / 空元素

  - 不包含任何内容的元素称为空元素

- `<a>`元素 / anchor element / 锚元素 

  - `<a>` 可包括属性:
  1. `href=""` 声明超链接地址
  2. `title=""` 悬停时显示的信息
  3. `target=""` 指定如何呈现链接
    - 默认(无`target`属性)当前页面, `target="_blank"`跳转新标签页
  

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

- `<html></html>`: `<html>`元素包裹整个完整的页面, 是一个**根元素**

- `<head></head>`: `<head>`元素是一个**容器**，其内容包含在HTML页面中但不会被显示
  - 如: 在搜索结果中出现的关键字和页面描述, CSS样式, 字符集声明等

- `<meta charset="utf-8">`: 设置文档使用`utf-8字符集`编码(1Byte 8bit)

- `<title></title>`: 设置页面标题, 出现在浏览器标签上, 标记/收藏页面时可用来描述页面

- `<body></body>`: `<body>`元素包含访问页面时所有显示在页面上的内容

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

## HTML head / 头部元素

> 与 `<body>` 元素不同, `<head>`不会在浏览器中显示. 其作用是保存页面的一些元数据

0. `<meta>`元素: 添加元数据
    - 元数据就是描述数据的数据
    - 许多 `<meta>` 元素包含了 `name` 和 `content` 特性
    1. 指定字符编码 `<meta charset="utf-8">`
    2. 增加自定义图标 `<link rel="shortcut icon" href="favicon.ico" type="image/x-icon">`
    2. 添加作者和描述 (搜索引擎搜索结果显示)
        ``` html {.line-numbers}
        <meta name="author" content="Author Name">`
        <meta name="description" content="Description Content">`
        ```
    3. 许多` <meta>` 特性已经不再使用。 例如，keyword `<meta>` 元素
    4. 部分大型网站有专有元数据
<br />
1. `<title>` 元素
    - 是一项元数据，用于表示整个 HTML 文档的标题
    - 显示在标签页的标签中
    - 显示在收藏页面时的建议名称中
    - 显示在搜索结果中 (超链接的文本显示)
<br />
2. 应用 CSS 和 JavaScript
    - 用 `<link>` 元素引入 CSS 文件 
      - `<link rel="stylesheet" href="my-css-file.css">`
    - 用 `<script>` 元素 引入/添加 JavaScript
      - `<script src="my-js-file.js"></script>`
      - `src`引入的脚本会覆盖 `script` 内部的脚本 (同时存在)
<br />
3. 设定主语言

    1. `<html lang="zh-CN">`
    2. 用`<span lang="jp"></span>` 包裹要设定的部分

## HTML 内容 | text

> HTML 的主要工作是编辑文本结构和文本内容 (也称为[语义 semantics](https://developer.mozilla.org/zh-CN/docs/Glossary/Semantics))

### 标题/段落 heading/paragraph

1. `<p>` paragraph content `</p>` : 定义单个段落 

2. `<h1>` the main heading `</h1>` : 定义标题
    - `<h1>` the main heading, `<h2>` subheadings, `<h3>` sub-subheadings
    1. 单页面**单个`<h1>`**
    2. 层次结构的顺序正确 
    3. 尽量只使用 `<h1>` `<h2>` `<h3>`

### 列表 Lists

0. `<li>`: list items

1. 无序 Unordered lists
    ``` html {.line-numbers}
    <ul>
      <li>lists items1</li>
      <li>lists items2</li>
    </ul>
    ```

2. 有序 Ordered lists 
    ``` html {.line-numbers}
    <ol>
      <li>lists items1</li>
      <li>lists items2</li>
    </ol>
    ```
- 列表之间可以嵌套

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




### 重点强调

1. Emphasis / 强调

    - 在口语表达中强调某些字
    - 用 `<em>`(emphasis) 元素 标记
    - 默认风格为斜体

2. Strong importance / 非常重要

    - 强调重要的词
    - 用 `<strong>`(strong importance) 元素标记
    - 默认风格为粗体

- 强调之间可嵌套

### 表象元素 / presentational elements

- 表象元素: 仅影响表象而**没有语义**, 不建议使用
- 已不使用: 如`<b>, <i>, <u>`

## 建立超链接 / hyperlinks


1. 链接构成: `<a href="" title=""> </a>`
    1. 用 `<a> </a>`元素包裹内容(包括块级元素)创建链接
    2. 用 `href=""`属性(Hypertext Reference) 添加指向的地址
    3. 用 `title=""`属性添加支持信息(悬停显示)
        - 注意: title仅当悬停时才显示, 只用于补充信息
<br />

2. `URL`: Uniform Resource Locator, 统一资源定位器
    - HTTP中, `URL` 被称为 `Web address` 或 `link`
    - `URL` 可指向可在网络上保存的任何内容, 若浏览器不知道如何显示或处理文件, 则会询问是否要打开/下载文件
    - 指向工作目录:
        - 默认指向当前目录
        - 直接索引下级目录 
        - 用 `../` 指向上一级目录
<br />

3. 链接当前文档片段
    - 先给元素分配 `id` 属性 eg. `id="id_Name"`
    ``` html {.line-numbers}
    <a href = "[tagDOC.html]#id_Name">...
    ```

4. absolute URL versus relative URL
    - 绝对链接 `absolute URL`: 指向由其在Web上的绝对位置定义的位置, 包括 protocol(协议), domain name(域名)
    - 相对链接 `relative URL`: 指向与所链接文件相关的位置 

5. 注意点:

    - 链接文本中不要包含 URL, 链接(到)
    - 保持链接尽可能*短*
    - 尽可能使用**相对链接**
        - 使用 相对URL 更有效率
        - 访问 绝对URL 时需先通过 DNS 查找 IP地址
    - 链接到 非HTML资源 时留下清晰的指示
        - 如 `(PDF, 10MB)`

6. 下载链接使用 `download` 属性

    - 使用 `download = ""`提供一个默认的保存文件名
    - `download`属性仅适用于**同源URL**
        - 同源(Same-origin)URL  的 protocol、port(若指定)和 host 都相同

7. 电子邮件链接
    ``` html {.line-numbers}
    <a href = "mailto:[example@abc.com][?]">...
    <a href = "mailto:exp@abc.com?cc=a1@b.com&cc=a2.b.com&subject=The%20subject%20of%20the%20email&body=The%20body%20of%20the%20email">...
    ```
    - 若无邮件地址, 窗口仍会被打开
    - 使用 `?` 分隔 主URL 与 参数值 
    - 使用 `&` 分隔 `mailto:` 中的各个参数
    - 常用: 主题(`subject`)、抄送(`cc`)和主体(`body`)
    - 每个字段的值**必须**是URL编码的, 不能有非打印字符 (如制表符、换行符、分页符) 和空格



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