# 打破CSS小小瓶颈

早前看到了张鑫旭老师的一篇文章《说说CSS学习中的瓶颈》http://www.zhangxinxu.com/wordpress/2012/07/bottleneck-css-study/ 由此开始了，一份属于自己的CSS规范和开始深入理解css。

`提示`： 我的css约定规范里有分好移动端和pc端的reset规范 可以看一下 https://github.com/wasdokij/css/blob/master/README.md

## 正文从这里开始

维护最大的难题在于看不懂... <br>
打开别人的代码总会冒出，写的什么鬼？ <br>
没有模块划分、嵌套深如地狱、样式重复不会利用样式优先级等，这些维护时的痛点很多开发者应该都深有体会。。。 <br>
其实本文主要想讲的是，如何管理好页面、组件，把每个组件给颗粒化。***但！*** 更重要的一些规范很多开发者有没有，因子我觉得，有了自己的规范，有了约束、有了规律，以上的问题就可以很好的解决了，所以一下开始学习路线.... `PS`: 记得点下文放出的每个`链接`，并且看完哦


## 主要解决的痛点：
> * [css模块划分](#module)
> * [CSS权重及防止嵌套过深（事关性能和维护问题）](#hierarchy)
> * [层叠上下文和层叠顺序（很多不理解层叠顺序的朋友，写页面时会出现奇奇怪怪的问题， 比如定位、浮动等导致的问题）](#stratum)

---
<a name="module"></a>
### css模块划分
世界很美好！很多前人已经总结很好了，  百度、google了一下，所以就在这里放好机票，自行过去吧....


`提示`：记得看完，并且理解！！！ 开发中，当自己发现css不整洁的时候要停下来！再看一遍、再看一遍、再看一遍。 保持css代码整洁可读，否则html部分的结构也会很槽糕！

 ***google***: http://rscss.io/components.html（英文原版）

 ***百度***: https://segmentfault.com/a/1190000008137332（翻译过的）

`小提示`： 开发小技巧-->
 * 拿到设计稿先规划好公共模块-->模块里再细化组件-->规划每个组件的命名！
 * 如果英文不好的朋友，可以像我一样，把常用的模块和组件命名列成一张表(比较长的单词可以缩写，和小伙伴一起约定好)。 可以一下看我自己的这个规范：https://github.com/wasdokij/css/blob/master/README.md

---
<a name="hierarchy"></a>
### CSS权重等级及浏览器渲染机制

浏览器在渲染css时是有自己的规则的（权重越高就优先渲染）<br>

**权重的基本规则：**
* 相同的权重：以后面出现的选择器为最后规则
* 不同的权重，权重值高则生效

***4个等级的定义***：
1. 第一等：内联样式，如: style=""，权值为1000。
2. 第二等：ID选择器，如：#content，权值为100。
3. 第三等：类、伪类和属性选择器，如： .content，权值为10。
4. 第四等：元素、伪元素选择器，如： h2、:before 与 :after，权值为1。

`小提示`：!important 为最高权重，慎用！

***浏览器渲染机制***：

浏览器读取css选择器有一个很重要的原则，那就是从右到左读取。所以尽量避免使用后代选择器，要去除不必要的祖先元素，以及防止嵌套过深，可以考虑使用类选择器来替换后代选择器
```css
.content div {}  // 浏览器先去找到所有的div这个标签，然后再去找div上面的.content这个样式，往上找父节点，找不到就继续往上...，这样会需要更长的渲染时间。
.content .article {} // 这样就会直接了当的去寻找了
```
***利用好关系选择符提升css权重***：
```css
1.利用选择符提高css权重例子：
.search-form  .field { /* ... */ }
.search-form > .field { /* ... */ } // 尽量用子选择符 > ,少用包含选择符 (空格)，以更好地避免冲突
.btn.action { /* ... */ } // 多种属性或状态, 如：选中按钮
```

`知识点补充`（出自w3cplus大漠老师的文章）：

[《CSS3基本选择器》](https://www.w3cplus.com/css3/basic-selectors)

[《CSS3属性选择器》](https://www.w3cplus.com/css3/attribute-selectors)

[《CSS3伪类选择器》](https://www.w3cplus.com/css3/pseudo-class-selector)

[《CSS选择器优化》](https://www.w3cplus.com/css/css-selector-performance)

---
<a name="stratum"></a>
### 层叠上下文和层叠顺序
这部分可以看张鑫旭老师的文章，理解透这部分对页面布局及常见问题处理会提升一个档次（这部分最好对定位、浮动等有所理解后，看这篇才会理解得更透彻）
http://www.zhangxinxu.com/wordpress/2016/01/understand-css-stacking-context-order-z-index/