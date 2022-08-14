# 基础知识
1. 策略: 渐进增强 (progressive enhancement)

    - 厂商前缀: -webkit-transform, -moz-transform, -ms-transform, transform
    - 条件规则与检测脚本:
        - @supports 
        - JS检测

2. 基础: 创建结构化、语义化富HTML

    - ID 和 class 属性
        - 提倡使用 ID 来标识特定模块的特定实例(已有class)
        - ID 可以用于在文档中标识元素，但通常不用于添加样式
    
    - div 和 span
        - 确保只在额外提供样式接入的情况下才使用 div
        
    - 扩展 HTML 语义
        1. ARIA 的 role 属性
            - banner form main search complementary...
            - ARIA支持指定更复杂的内容片段和界面元素
        2. 微格式
            - 目前最广泛采用的扩展 HTML 语义的方式
            - 一组标准的命名约定和标记模式，可用于表示特定的数据类型
            - 其命名约定基于 vCard 和 iCalendar 等巳有的数据格式制定
        3. 微数据
            - 微数据是给 HTML 添加结构化数据的另一种方式

    - 验证 HTML / CSS
        - 只要把验证当作事先帮我们发现一些低级错误的手段即可

## CSS 基础概念

- css, Cascading Style Sheets, 层叠样式表
    - 用户最终所见为 最上层 的样式
- 使用css修改元素样式

### 应用 CSS

1.  内联/行内样式 
    - 一般不使用 
    - 在标签内部通过style属性设置样式

2. 将css样式编写到 `<head>` 中的 `<style>` 中
    - 仅限于单一页面

3. 外部样式表 推荐使用!
    - 可通过浏览器缓存, 加快网页加载
    1. 推荐:`<link href="/c/base.css"rel="stylesheet"/>`
    2. `<style>
        @import url("/c/modules.css");
        </style>`

### CSS加载与性能

注意点:
1. 浏览器加载完**所有**CSS后才有最佳响应(一次性绘制页面)
    - 不要将CSS放到 body 或页面底部

2. 文件数量
    - 一个文件 -> 一次 HTTP请求 -> 发送(cookie,请求首部等) + 服务器响应 + 服务器返回(响应首部,文件等) + 接收(下载) -> 应用css
    - <= 2个文件
    - 使用 `@import` **不能**减少请求数量

3. 压缩与缓存
    - 压缩: Gzip
    - 缓存: 通过HTTP首部告诉浏览器

4. 防止 JS 阻塞 CSS
    - 若 head 中有 script 元素, 则浏览器会**先**加载/下载并执行JS, 然后继续解析 HTML 与 CSS
    - 防止渲染阻塞
        1. 将 `<script>` 放在HTML页面底部的`</body>` 之前
        2.  `<script>` 添加属性 `async` / `defer`
            - async: 异步加载, 加载完后暂停HTML解析先执行JS
            - defer: 异步加载, 等待HTML解析完毕后执行JS
        ``` html {.line-numbers}
        <head>
        <！--异步加载, 但加载后立即执行-->
        <script src="/scripts/core.js"async></script>

        <！--异步加载, 但在HTML解析后执行-->
        <script src="/scripts/deferred.js"defer></script>
        </head>

        <！-最后加载JavaScript-->
        <script src="/scripts/core.js"></script>
        </body>
        ```


### HTML标签/元素

HTML 标签: HTML 标记标签通常被称为 HTML 标签 (HTML tag)
HTML 元素: 指从 start tag 到 end tag 的所有代码


### 元素关系

1. 父/子 元素：**直接** 包含子/被父包含 的元素

2. 祖先/后代 元素：**直接或间接** 包含后代/被祖先包含 的元素，
    - 父/子元素也是祖先/后代元素

3. 兄弟元素：拥有**相同父**元素的元素


## CSS 选择器


### 基本选择器
    
1. 类型/元素 选择器: `tag_name{}`
2. id 选择器: `#id_value{}`
3. 类选择器: `.class_name{}`
4. 属性选择器: 
    - `tagName/* attributeName[(^/$/*/~/|)(=attributeValue)]`
    - 指定/所有元素中 有属性名\[/属性名为/属性名开头/结尾/包含字符/包含单词(以空格分开)/包含字符或字符加连字符-]
5. 通配选择器 `*{}`


### 交集/并集 选择器

1. 交集选择器  
    - 选择器1 选择器2 选择器n{}
    - 注意: 若存在则必须使用元素选择器开头
    
2. 并集选择器/选择器分组
    - 选择器1, 选择器2, 选择器n{}


### 按元素关系选择

0. 组合器(combinator):描述两侧选择符组合的方式(`>` `+` `~`)
1. 子元素选择器: `父元素 > 子元素{}`
2. 后代元素选择器: `祖先元素 后代元素{}`
3. 兄弟元素选择: 
    `前一个 + 下一个{}` :选择**紧邻**的下一个兄弟元素(若非紧邻则无效)
    `兄 ~ 弟元素{}` :选择之后的所有的弟元素


### ::伪元素 pseudo-elements

- 伪元素: 页面中特殊的 非真实/单独 存在的元素
- 伪元素选择器:
    - 一般以 `::` 开头 (`::` 前可加元素限定)
    1. `::first-letter/::first-line{}` 
    2. `::selection{}` 
    3. `::before/after{content: ""; }` 
        - 元素开始前/结束后(非内容部分)
        - 需要结合 `content` 添加显示内容
        - `content` 内容**无法**被选中


### :伪类 pseudo-classes

- 伪类: 不存在/特殊的类, 描述一个元素的特殊状态
- 伪类选择器: 
- 一般以 `:` 开头 (`:` 前可加元素限定)
    1. `:first/last-child` 
    2. `:nth-child(n)` 选中第n个(n为自然数)
        - 若只填 n/(2n|even)/(2n+1|odd)/(-n+3) 选中 所有(0~+∞)/偶数/奇数/前3个 元素
        - 以上3个child伪类皆根据所有相同子元素排序(若被占位(如首位非同元素)则**跳过**(无效果))

    3. `:first/last-of-type`
    4. `:nth-of-type()`
        - 以上3个of-type伪类在同类型元素中排序, 功能与child伪类相似

- 特殊伪类

    6. `:not()` 否定伪类 去除选择中符合条件的元素 可与上述伪类嵌套使用
        - 伪元素和它自身除外

    5. `:target` 目标伪类, 所匹配元素的 id值 为当前页面 URL 末尾的井号 # 之后的值
        - 如 `https://example.com/blog/1/#thecomment`

    7. `:required` 选择带有 required 属性的表单元素

    8. `:valid`/`:invalid` 输入框中当前内容有效/无效时
        - eg. `input[type="email"] :valid{}` 

- 超链接伪类

    6. `a:link` 未访问/正常连接
        - 超链接伪类 !**a专属**! 超链接状态4: 未访问/已访问

    7. `a:visited` 访问过链接  :visited 只能修改颜色, 出于隐私原因
        - 超链接伪类 !**a专属**! 超链接状态4: 未访问/已访问

    8. `:hover / :focus`     鼠标移入 / 键盘焦点
        - 触摸屏和键盘等输入方式下不一定真的有悬停状态

    9. `:active`     鼠标点击/活动状态

    10. 链接伪类**优先级**: 排序爱恨原则 **L**o**V**e and **HA**te
        - a:active 在 a:hover 之后; a:hover 在 a:link 和 a:visited 之后，才能生效！

## 样式优先级

> 1.层叠机制; 2.选择符的特殊性


### 层叠机制:

- 层叠机制的原理是为规则赋予不同的重要程度 

1. 标注为 `!important` 的用户样式 
2. 标注为 `!important` 的作者样式 
3. 作者样式 
4. 用户样式 
5. 浏览器(或用户代码)的默认样式


### 特殊性

- 在层叠机制基础上再按选择符的特殊性排序

选择符|特殊性|十进制特殊性
-----|-----|------
`inline`内联样式|1,0,0,0|100
`id`选择器|0,1,0,0|100
`class`类, *(id)属性*, 伪类选择器|0,0,1,0|10
`elements`类型/元素, 伪元素选择器|0,0,0,1|1
`*`通配选择器|0,0,0,0|0
继承样式(一定被覆盖,包括通配选择)|.无优先级|-

6. 特殊性高的选择符覆盖低的
7. 若特殊性相等则**后定义**的规则优先
1. 权重**不能**跨数量级(不会溢出)
2. 比较时将所有选择器优先级相加再排序
    eg. `div#id1 .class1 .class2` -> `0,1,2,1`
3. 分组则单独计算各组(`… , … , …`)


## 盒模型

> 所有元素都被看作一个矩形盒子, 包含元素的内容+内边距+边框+外边距

`content`
`padding`
`border` 
`margin` 
`outline`: border外围的一条线, 不影响布局(不占位)


### 盒子大小

- `box-sizing` 属性可以改变计算盒子大小的方式
    - box-sizing: `content-box` | `border-box` | `inherit`

1. `box-sizing: content-box`
    - width height 属性应用给 `content`
    - 添加的 padding border margin 会增加元素盒子的大小

2. `box-sizing: border-box`
    - width height 属性包含 `padding + border`
    - 添加的 margin 会增加元素盒子的大小

- 最大最小值

1. `min-width` `max-width` 响应式布局中常用

2. `height` 值慎重设置(元素高度取决于其内容)
    - 只设置 `min-height` , 避免使用 max-height

### 可见格式化模型

1. 块级盒子 (block box) :由块级元素生成

2. 行内盒子 (inline box) :由行内元素生成
    - 行内盒子的高度`height`**不受**垂直方向上的内外边距与边框的影响

3. 行盒子 (line box) :由一行文本形成的水平盒子
    - 行盒子的高度`height`由所含的行内盒子决定
    - 修改行盒子大小:
        1. 修改行高 `line-height`
        2. 修改所含行内盒子的水平内外边距与边框

4. 匿名盒子: 由不与任何特定元素相关的元素生成
    - 匿名块盒子(anonymous block box)
    - 匿名行盒子(anonymous line box)
    - 只能使用某些伪元素添加样式如`:first-line`

- `display` 属性: 改变生成的盒子类型
    - `display: none;` 不生成盒子 -> 不显示,不占位
    - `display: inline-block;` 元素水平排列(inline)而且盒子能够设置高宽与垂直内外边距(block)

### 外边距折叠 margin collapsing

- 垂直方向上两个相邻外边距会折叠成一个, 其高度值为两者中较大的一个
    - 范围: 数量`>=2`个的垂直`margin` 直接接触(之间无`border`)
    - 限定: 只发生在文档常规文本流中**块级盒子**的垂直方向上(行内,浮动或绝对定位盒子的外边距不会折叠)

### 包含块 containing block

> 当内外边距数值的单位为 `%` 时, 包含块为其计算依据

- 确定元素的包含块要看元素是如何定位的
- `position:` `static` | `fixed` | `relative` | `absolute` `;`

0. 静态定位 `position:static;` / 不指定 `position` 的值
    - 支持position属性的html对象的默认值
    - 表示块保留在原本应该在的位置，不会重新定位
    - 一般不需要使用
    - 包含块的边界就计算到最近的父元素(该元素的 `display` 需能提供块级上下文如` block inline-block table-cell list-item `)

1. 相对定位 `position:relative;`
    - 元素待在原始位置
    - 原始位置一直被占用(即使元素位置变动)
    - 修改上下左右值使元素相对原始位置移动
    - 包含块的边界就计算到最近的父元素(同静态定位)

2. 绝对定位 `position:absolute;`
    - 元素不占用原始位置(离开文档流)
    - 其他元素各自重新定位
    - 绝对定位元素的包含块:
        1. 距离它最近的定位祖先(`position: relative|absolute|fixed;`)
        2. 根元素(`<html>`也称起始包含块 initial containing block)
    - 整体布局上不使用(z-index控制层叠次序)

3. 固定定位 `position:fixed`
    - 包含块是视口 viewport ,即屏幕上能用来显示网页的区域, 不局限于浏览器可视区域的大小
    - 可用来创建始终停留在窗口相同位置的浮动元素 如导航区,侧栏,顶栏

### 浮动 float

- `float:` `left` | `right` `;`
1. 浮动元素脱离常规文档流, 进入浮动流
2. 对块级元素不可见
3. 对行内元素inline及文本**可见**

- 清除 clear
    - `clear:` `left` | `right` | `both` | `none` `;`
    - 用于指定盒子的哪一侧不该紧挨着浮动盒子
    - 清除元素后, 会为该元素上方添加margin将其上边沿在浮动元素下方
        - 实现原理是隐式地添加一个足够大的上外边距, 来"躲开"浮动元素
    - 使父元素包含浮动的子元素:(只包含浮动元素的父元素高度为`0`)
        1. 添加额外的空元素,设置 `clear:left;`
        2. 用父元素的`::after`伪元素模拟
            ``` css {.line-numbers}
            .box::after {
                content: "";
                display: block;
                clear: both;
            }
            ```
### 格式化上下文 formatting context 

> 文档流分为 定位流, 浮动流, 普通流 三种

1. FC 是页面中的一块渲染区域，有一套渲染规则，决定了其子元素如何布局，以及和其他元素之间的关系和作用

2. 常见的FC: BFC块级, IFC行级, GFC网格布局, FFC自适应

- 块级格式化上下文 **BFC** block formatting context

    - BFC是CSS布局的一个概念, 是一块区域, 一个环境, 包含创建它的元素内部的所有内容

    - 满足下列CSS声明之一的元素便会生成BFC
        - 根元素, 即`<HTML>`
        - 浮动元素: `float:` `left | right ;`
        - `overflow:` `auto | scroll | hidden ;` (即`!=visible`)  
        - `display:` `inline-block | table-cell | table-caption | table | inline-table | flex | inline-flex | grid | inline-grid ;`
        - `position:` `absolute | fixed ;`

    - BFC 布局规则: 在 1个 **BFC 内部**,
        - 内部的盒子在*垂直*方向一个个放置
        - 相邻盒子的垂直外边距会发生折叠(BFC之间不折叠)
        - 每个元素的 margin box 的左边与包含块的 border box 的左边相接触 (从左到右排列时, 反之同理) , 浮动元素也一样
        - BFC 的区域**不会**与浮动的盒子重叠(左右分栏)
        - 浮动元素也参与计算 BFC 的高度 (包裹浮动元素)
        - BFC 是页面上的一个隔离的独立容器, **不会**影响到外部, 同样, 外部也不会影响到 BFC 内部

    - BFC 作用：
        - 包含浮动内容
            - 让浮动内容和周围的内容等高
            - `display: flow-root //父元素使用`
        - 自适应多栏布局
            - `overflow: hidden; /* required by resize:both */`
            `resize: both;`
            - 注意，flexbox 是在现代 CSS 中实现多列布局的更有效的方法。
        - 避免外边距重叠


# 基本排版

## 文本相关

0. 名词区分字体字型字形
    - `typeface` 字体
        - 一种字体风格设计的抽象概念
        - `typeface` `==` `font family` 
        - eg. `Helvetica` 
    - `font` 字型
        - 某一字体设计的具体样式 `font∈typeface`
        - eg. `Helvetica Regular 12pt` 
    - `glyph` 字形
        - 文字中字母 (character) 的视觉表现
        - ~~同一 `character` 可以有不同字形(文字的形状)~~

1. 字体族 `font-family`
    - [web safe CSS font](https://www.cssfontstack.com/)
    - 通用字体族: `Serif`衬线 `Sans-serif`无衬线 `Monospace`等宽 `Cursive`手写 `Fantasy`花式
    - 若字体族名称包含 空格 或 非标准符号 时应当加引号

1. Web字体
    1. 引入Web字体 `@font-face`
    ``` css {.line-numbers}
    @font-face { 
        font-family: customizeName;
        src: url("/font/font1.woff") format('woff'),
             url("/font/font1.woff2") format('woff2'),  /*跨浏览器支持*/
             url("/font/font1.tff") format('truetype'); /*跨浏览器支持*/
        font-weight: bold;                              /*可选, 默认normal*/
        font-style: bold;                               /*可选, 默认normal*/
    }
    ```

    2. 注意点
    - 以上声明不是属性, 而是字体描述符 (font descriptor) (不改变字体)
    - 若在 `@font-face` 中声明 `font-weight: normal` 而在使用时设置 `font-weight: bold;` 会导致浏览器将字体 **模拟 加粗**

    3. 加载&渲染Web字体
        1. 闪烁一 FOIT(flash of invisible text) 字体加载完成后才显示文本
            - 若网速慢 则体验不佳
        2. 闪烁二 FOUT(flash of unstyled text) 先使用后备字体显示, 加载完成后替换
            - 若两种字体差距较多 则影响页面排布
        3. 使用 JavaScript 加载字体 
            - Web Font Loader
            - 可同一 x高度
    
2. 字体样式 font-style
    - `font-style:` `normal` | `italic` 
    - 若不存在相应的倾斜变体，浏览器会模拟倾斜效果

3. 大小写 text-transform
    - `text-transform:` `uppercase` | `lowercase` | `capitalize` | `none` 
        - uppercase全大写, lowercase全小写 , capitalize首字母大写 , none不改变
    - `font-variant:` `small-caps` 小型大写字母(css2.1唯一可选值)

4. 文本颜色 color

4. 文本阴影 text-shadow
    ``` css {.line-numbers}
    text-shadow: 
        <offset-x>      /*必选, 水平偏移量, 正值位于文本右侧*/
        <offset-y>      /*必选, 垂直偏移量, 正值位于文本下方*/
        <blur-radius>   /*可选, 模糊半径, 默认为 0 */
        <color>         /*应选, 阴影颜色, 未指定则使用UA自行选择的颜色*/
        ;
    text-shadow: /*可添加多组阴影, 按 先后次序 自上向下 堆叠*/
        1px 1px 2px black, 
        0 0 1em blue, 
        0 0 0.2em blue;
    ```

5. 字型大小
    > 浏览器中默认 `font-size:16px`
    1. `em` :基于继承的大小缩放 需留意最终计算结果
    2. `rem` :基于root element的em大小缩放(即基于html element的font-size缩放)
    3. [缩放比例参考](https://www.modularscale.com/): perfect fourth 1.333

6. 文本粗细 font-weight
    - 100,200,300 | 400(`normal`) | 500,600 | 700(`bold`) | 800,900
    - `lighter` | `bolder` 相比 父元素继承值 调整
    - 回退机制
        1. `x∈[400,500]` : 升序查找`[x,500]` → 降序查找`[1,x]` →升序查找`[500,1000]`
        2. `x∈[1,400)` : 首先降序查找`[1,x]` → 升序查找`[x,1000]` 先小后大
        3. `x∈(500,1000]` : 升序查找`[x,1000]` →  降序查找`[1,x]` 先大后小
        - 若一字体只包含 normal(400), bold(700), 则 `[1,500] → normal` , `[501,1000] → bold`
    - 浏览器能尽量模拟**加粗**效果(无对应变体), 但不能~~模拟变细~~效果

7. 高级字体样式

    > OpenType特性: 字距调整(kerning), 连字(ligature), 替代数字(alternative numeral), 饰线(swash) 等

    2. 连字 ligatures 
    ``` css {.line-numbers} 
    font-variant-ligatures: common-ligatures discretionary-ligatures;
    font-feature-settings:　"liga","dlig"; /*OperiType 特性*/
    ```

    3. 线性数字
    ``` css {.line-numbers} 
    font-variant-numeric: lining-nums | oldstyle-nums ;
    font-feature-settings: "lnum" | "onum"; /*OperiType 特性*/
    ```

    4. 表列线性数字(垂直对齐)
    ``` css {.line-numbers} 
    font-variant-numeric: tabular-nums lining-nums;
    font-feature-settings: "tnum", "lnum"; /*OperiType 特性*/
    ```

    5. 字距调整kerning
    ``` css {.line-numbers} 
    font-kerning: normal | auto | none;
    font-feature-settings: "kern";
    ```

## 排版相关 字词行间距

1. 字词间距
    - 少用: 词间距 `word-spacing` 
    - 字符间距 `letter-spacing` 可便于abbr的识别(与`font-variant:small-caps`联用)

2. 垂直对齐 vertical-align
    - 基线: 每个行内盒子的底边都默认对齐于靠近底部的共同水平线
    - `vertical-align:` `baseline`(默认) | `sub` | `super` | `inherit` ...
    - vertical-align 会影响行盒子高度

3. 行高 line-height 
    - 指行盒子的总高度
    - `font-size` + `上下的行间距`
    - 推荐: 行高**无单位**时, 子元素继承系数，依据自身font-size计算
    - 行高有单位(px em %), 子元素继承 计算后得到的px像素值

4. 行长度 
    - eg. `max-width: 36em;`

5. 文本对齐
    - 段首缩进 `text-indent`
    - `text-align:` `start` `end` | `left` `right` `center` | `justify` ...
    - 逻辑方向 与文本书写模式对应 | 左右居中 | 两侧对齐(不加`-all`对最后一行无效)

6. 连字符
    - 软连字符`＆shy;`只在需要时显示

## 多栏文本

0. CSS Multi-column Layout Module
    ``` css {.line-numbers}
    article {
        max-width: 70em;
        columns: 20em;
        column-gap: 1.5em;
    }
    ```
1. `cloumns` 
    - `cloumns` 分为 `column-count` `column-width`
    - `columns: 3;` 确定3栏, 宽度auto;
        == `column-count: 3;`
    - `columns: 20em;` 确定最小宽度20em, 栏数auto;
        == `column-width: 20em;`
    - `columns: 3 20em;` 最少3栏, 每栏宽度最小20em
        == `column-count: 3; column-width: 20em;`

2. 后备宽度
    ``` css {.line-numbers}
    article > p { /* 应用到段落元素 */
        max-width: 36em;
    }
    ```

3. 部分元素跨栏
    `column-span:` `all` | `none` `;`

4. 垂直律动与基线网格
    > 不同于印刷, 网页排版难以保证多栏文本对齐基线
    - 可手动调整非段落元素(如标题h2 h3)
    - 使*标题元素* `margin-top + line-height + margin-bottom` `=` *正文元素* `line-height * n`
        - `line-height(px)` `=` `font-size * line-height`


# 盒模型

## 颜色值与不透明度

0. 不推荐 预定义关键字
    red b1ack teal goldenrod darkseagreen 

1. 十六进制表示法 #RRGGBB
    - 如果三组值中两位数字都重复, 可简写为 #RGB

2. rgb() / rgba() 函数式表示法
    0. rgb(R, G, B) / rgb(R, G, B, a)
    1. alpha 取值 0 ~ 1.0 (不透明 ~ 完全透明)
    2. RBG用十进制数字: 取值 0 ~ 255
    3. RBG用百分比值: 取值 0% ~ 100%

3. hsl() / hsla()
    0. Hue-Saturation-Lightness 色相-饱和度-亮度
    1. alpha 取值 0 ~ 1.0 (不透明 ~ 完全透明)
    2. h 取值 0 ~ 360 (deg) (720 == 360)
    3. s,l 取值 0% ~ 100%

## 背景

0. 透明度属性 opacity(不透明)
    - 改变整个元素(包括内容, 子元素)的透明度
    - 取值 0 ~ 1 , 完全透明 ~ 不透明
``` css {.line-numbers}
background-color: #8Da9cf;
background-imge: url();
background-repeat: no-repeat;
```
1. `background-color` 背景颜色
2. `background-image` 背景图片 
    - img 元素: 内容图片 - 图片自身有意义
    - background-image 背景图片 - 装饰性
    0. 应添加默认背景颜色以防止图片加载失败
    1. 相对路径不加/ eg. `img0/img1.img` 则从保存当前css的目录的img1子目录中寻找img1
    2. 相对路径加/ eg. `/img2/img3.img` 则从相对于css文件所在域的顶级目录的img2子目录中寻找img3
    3. 使用绝对路径需要写全 协议, 域名, 路径, 文件名
    4. data URL eg. `url(data:image/png;base64,...)`
3. `background-repeat: repeat;` 为默认值
4. `background-position` 
    1. 关键词: `top/center/bottom left/center/right`
    2. `x% y%`: 左上角为 `0% 0%`, 右下角为 `100% 100%`
    3. `x-pos y-pos`: 左上角为 `0 0`, 单位为 px/em/...
    4. % 和 position值 可混用
    5. 若只规定一个值, 则另一个为 `center`/`50%`








































<br><br><br><br><br><br><br><br>

<br><br><br><br><br><br><br><br>
<br><br><br><br><br><br><br><br>

<hr>

<br><br><br><br><br><br><br><br>

<hr>

    ``` html {.line-numbers}
    ``` html {.line-numbers}
    ``` html {.line-numbers}

    ```
    ```


<br><br><br><br><br><br><br><br>

<hr>

<br><br><br><br><br><br><br><br>
<br><br><br><br><br><br><br><br>

<hr>

<br><br><br><br><br><br><br><br>

<hr>

    ``` html {.line-numbers}
    ``` html {.line-numbers}
    ``` html {.line-numbers}

    ```
    ```


<br><br><br><br><br><br><br><br>



    ``` html {.line-numbers}

    ```
