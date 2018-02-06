# CSS约定规范

## 约定
***1. [注释规范](#注释规范)*** <br>
***2. [代码规范](#代码规范)*** <br>
***3. [reset规范](#reset规范)*** <br>
***4. [媒体查询规范](#媒体查询规范)*** <br>
***5. [SASS规范](#SASS规范)*** <br>


### 注释规范
注释的风格应当简洁，并在代码库中保持统一。

* 将注释放在主题上方并独占一行。
* 控制每行长度在合理的范围内，比如80个字符。
* 使用注释从字面上将CSS代码分隔为独立的部分。
* 注释的大小写应当与普通句子相同，并且使用一致的文本缩进。

提示：通过配置编辑器，可以提供快捷键来输出一致认可的注释模式。

#### CSS示例：

```css

/* --------------------------------------------------------------------------
   区块代码注释 Module A
   -------------------------------------------------------------------------- */

/* 次级区块代码注释 Module A form
   -------------------------------------------------------------------------- */
/* 一般的注释 Module A form btn */

/**
 * “Doxygen式注释格式”的简短介绍
 *
 * 较长的说明注释
 *
 * 当需要进行更细致的解释说明、提供文档文本时，较长的说明文本就很
 * 有用了。这种长长的说明文本，可以包括示例HTML啦、链接啦等等其
 *
 *
 * @tag 这是一个叫做“tag”的标签。
 *
 * TODO: 这个“‘需做’陈述”描述了一个接下来要去做的小工作。这种文本，
 *   如果超长了的话，应该在80个半角字符（如英文）或40个全角字符（
 *   如中文）后便换行，并（在“ * ”的基础上）再在后面缩进两个空格。
 */


```

---
### 代码规范

#### 代码格式化

代码风格必须保证：易于阅读，易于清晰地注释，最小化无意中引入错误的可能性，可生成有用的diff和blame。

1. 在多个选择器的规则集中，每个单独的选择器独占一行。
2. 在规则集的左大括号前保留一个空格。
3. 在声明块中，每个声明独占一行。
4. 每个声明前保留一级缩进。
5. 每个声明的冒号后保留一个空格。
6. 对于声明块的最后一个声明，始终保留结束的分号。
7. 规则集的右大括号保持与该规则集的第一个字符在同一列。
8. 每个规则集之间保留一个空行。

```css
.selector-1,
.selector-2,
.selector-3[type="text"] {
    display: block;
    font-family: helvetica, arial, sans-serif;
    color: #333;
    background: #fff;
    background: linear-gradient(#fff, rgba(0, 0, 0, 0.8));
}

.selector-a,
.selector-b {
    padding: 10px;
}
```

#### 属性书写顺序

样式声明的顺序应当：
1. 遵守一个单一的原则。
2. 将相关的属性组合在一起，并且将对结构来说比较重要的属性（如定位或者盒模型）
放在前面，先于排版、背景及颜色等属性。<br>

>  1. 布局定位属性：position / display / float / clear / visibility / overflow <br>
> 2. 自身属性：width / height / margin / padding / border / background <br>
> 3. 文本属性：color / font / text-decoration / text-align / vertical-align / white- space / break-word <br>
> 4. 其他属性（CSS3）：content / cursor / border-radius / box-shadow / text-shadow / background:linear-gradient / CSS3 浏览器私有前缀在前，标准前缀在后<br>

```css
.selector {
    /* Positioning */
    position: absolute;
    z-index: 10;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    /* Display & Box Model */
    display: inline-block;
    overflow: hidden;
    box-sizing: border-box;
    width: 100px;
    height: 100px;
    padding: 10px;
    border: 10px solid #333;
    margin: 10px;

    /* Other */
    background: #000;
    color: #fff;
    font-family: sans-serif;
    font-size: 16px;
    text-align: right;
}
```

#### 例外及细微偏移原则的情况

对于大量仅包含单条声明的声明块，可以使用一种略微不同的单行格式。在这种情况下，在左大括号之后及右大括号之前都应该保留一个空格。

```css
.selector-1 { width: 10%; }
.selector-2 { width: 20%; }
.selector-3 { width: 30%; }
```

对于以逗号分隔并且非常长的属性值 -- 例如一堆渐变或者阴影的声明 -- 可以放在多行中，这有助于提高可读性，并易于生成有效的diff。这种情况下有多
种格式可以选择，以下展示了一种格式。

```css
.selector {
    box-shadow:
        1px 1px 1px #000,
        2px 2px 1px 1px #ccc inset;
    background-image:
        linear-gradient(#fff, #ccc),
        linear-gradient(#f3c, #4ec);
}
```

#### 杂项

* 在十六进制值中，使用小写，如白色`#fff`。
* 单引号或双引号的选择保持一致。推荐使用双引号，如`content: ""`。
* 对于选择器中的属性值也加上引号，如`input[type="checkbox"]`。
* 不要给0加上单位, 如`margin: 0`。
---

### reset规范

#### 移动端reset:

```css
* { -webkit-tap-highlight-color: transparent; outline: 0; margin: 0; padding: 0; vertical-align: baseline; }
body, h1, h2, h3, h4, h5, h6, hr, p, blockquote, dl, dt, dd, ul, ol, li, pre, form, fieldset, legend, button, input, textarea, th, td { margin: 0; padding: 0; vertical-align: baseline; }
img { border: 0 none; vertical-align: top; }
i, em { font-style: normal; }
ol, ul { list-style: none; }
input, select, button, h1, h2, h3, h4, h5, h6 { font-size: 100%; font-family: inherit; }
table { border-collapse: collapse; border-spacing: 0; }
a { text-decoration: none; color: #666; }
body { margin: 0 auto; min-width: 320px; max-width: 640px; height: 100%; font-size: 14px; fon-family: -apple-system,Helvetica,sans-serif; line-height: 1.5; color: #666; -webkit-text-size-adjust: 100% !important; text-size-adjust: 100% !important; }
input[type="text"], textarea { -webkit-appearance: none; -moz-appearance: none; appearance: none; }
```

#### PC端reset:

```css
html, body, div, h1, h2, h3, h4, h5, h6, p, dl, dt, dd, ol, ul, li, fieldset, form, label, input, legend, table, caption, tbody, tfoot, thead, tr, th, td, textarea, article, aside, audio, canvas, figure, footer, header, mark, menu, nav, section, time, video { margin: 0; padding: 0; }
h1, h2, h3, h4, h5, h6 { font-size: 100%; font-weight: normal }
article, aside, dialog, figure, footer, header, hgroup, nav, section, blockquote { display: block; }
ul, ol { list-style: none; }
img { border: 0 none; vertical-align: top; }
blockquote, q { quotes: none; }
blockquote:before, blockquote:after, q:before, q:after { content: none; }
table { border-collapse: collapse; border-spacing: 0; }
strong, em, i { font-style: normal; font-weight: normal; }
ins { text-decoration: underline; }
del { text-decoration: line-through; }
mark { background: none; }
input::-ms-clear { display: none !important; }
body { font: 12px/1.5 \5FAE\8F6F\96C5\9ED1, \5B8B\4F53, "Hiragino Sans GB", STHeiti, "WenQuanYi Micro Hei", "Droid Sans Fallback", SimSun, sans-serif; background: #fff; }
a { text-decoration: none; color: #333; }
a:hover { text-decoration: underline; }
```

---

### 媒体查询规范

#### 判断设备横竖屏
```css
/* 横屏 */
@media all and (orientation :landscape) { }
/* 竖屏 */
@media all and (orientation :portrait) { }
```

#### 判断设备宽高
```css
/* 设备宽度大于 320px 小于 640px */
@media all and (min-width:320px) and (max-width:640px) { }
```

#### 判断设备像素比

```css
/* 设备像素比为 1 */
@media only screen and (-webkit-min-device-pixel-ratio: 1), only screen and (min-device-pixel-ratio: 1) { }
/* 设备像素比为 1.5 */
@media only screen and (-webkit-min-device-pixel-ratio: 1.5), only screen and (min-device-pixel-ratio: 1.5) { }
/* 设备像素比为 2 */
@media only screen and (-webkit-min-device-pixel-ratio: 2), only screen and (min-device-pixel-ratio: 2) { }
````
---

### SASS规范
#### 选择器嵌套
```css
/* SCSS */
.sp {
    body & { }
}

/* CSS */
.sp { }
body .sp { }
```
#### 属性嵌套
```css
/* SCSS */
.sp {
    background: {
        color: red;
        repeat: no-repeat;
        image: url(/img/icon.png);
        position: 0 0;
    }
}

/* CSS */
.sp {
    background-color: red;
    background-repeat: no-repeat;
    background-image: url(/img/icon.png);
    background-position: 0 0;
}
```

#### 变量
抽离可复用属性为页面变量，易于统一维护
```css
// SCSS
$color: red;
.sp {
    color: $color;
    border-color: $color;
}

// CSS
.sp {
    color: red;
    border-color: red;
}
```

#### 混合(mixin)
根据功能定义模块，然后在需要使用的地方通过 @include 调用，避免编码时重复输入代码段

```css
// SCSS
@mixin radius($radius:5px) {
    -webkit-border-radius: $radius;
    border-radius: $radius;
}
.sp-1 {
    @include radius; //参数使用默认值
}
.sp-2 {
    @include radius(10px);
}

// CSS
.sp-1 {
    -webkit-border-radius: 5px;
    border-radius: 5px;
}
.sp-2 {
    -webkit-border-radius: 10px;
    border-radius: 10px;
}

---------------------------------
// SCSS
@mixin icon($x:0, $y:0) {
    background: url(/img/icon.png) no-repeat $x, $y;
}
.sp-1 {
    @include icon(-10px, 0);
}
.sp-2 {
    @include icon(-20px, 0);
}

// CSS
.sp-1 {
    background: url(/img/icon.png) no-repeat -10px 0;
}
.sp-2 {
    background: url(/img/icon.png) no-repeat -20px 0;
}
```

#### 占位选择器 %
如果不调用则不会有任何多余的 css 文件，占位选择器以 % 标识定义，通过 @extend 调用

```css
//scss
%borderbox {
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
}
.sp {
    @extend %borderbox;
}
```

#### extend 继承

```css
// SCSS
.sp-1 {
    font-size: 12px;
    color: red;
}
.sp-2 {
    @extend .sp-1;
    font-weight: bold;
}
// 或者
%font-red {
    font-size: 12px;
    color: red;
}
.sp-1 {
    @extend %font-red;
}
.sp-2 {
    @extend %font-red;
    font-weight: bold;
}

// CSS
.sp-1 {
    font-size: 12px;
    color: red;
}
.sp-2 {
    font-size: 12px;
    color: red;
    font-weight: bold;
}
```

#### for 循环
`注意`：#{} 是连接符，变量连接使用时需要依赖
```css
// SCSS
@for $i from 1 through 3 {
    .sp-#{$i} {
        background-position: 0 (-2px) * $i;
    }
}

// CSS
.sp-1 {background-position: 0 -2px;}
.sp-2 {background-position: 0 -4px;}
.sp-3 {background-position: 0 -6px;}
```

#### each 循环

```css
// SCSS
@each $name in list, detail {
    .sp-#{$name} {
        background-image: url(/img/sp-#{$name}.png);
    }
}

// CSS
.sp-list {
    background-image: url(/img/sp-list.png);
}
.sp-detail {
    background-image: url(/img/sp-detail.png);
}

-------------------------------------------------------

// SCSS
@each $name, $color in (list, red), (detail, blue) {
    .sp-#{$name} {
        background-image: url(/img/sp-#{$name}.png);
        background-color: $color;
    }
}

// CSS
.sp-list {
    background-image: url(/img/sp-list.png);
    background-color: red;
}
.sp-detail {
    background-image: url(/img/sp-detail.png);
    background-color: blue;
}
```

#### function 函数

```css
@function pxToRem($px) {
    @return $px / 10px * 1rem;
}
.sp {
    font-size: pxToRem(12px);
}
```

#### 运算规范
运算符之间空出一个空格
```css
.sp {
    width: 100px - 50px;
    height: 30px / 5;
}
```

`注意`:运算单位，单位同时参与运算，所以 10px 不等于 10，乘除运算时需要特别注意

```css
// 正确的运算格式
.sp {
    width: 100px - 50px;
    width: 100px + 50px;
    width: 100px * 2;
    width: 100px / 2;
}
```


