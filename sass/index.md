# Sass语法总结

## 1.1 变量声明

```scss
$highlight-color: #F90;
$highlight-border: 1px solid $highlight-color;
.selected {
  border: $highlight_border;
}
```
编译后
```scss
.selected {
  border: 1px solid #F90;
}
```
> 注：在sass中，中划线(-)和下划线(_)是相互兼容的。

## 2.1 选择器嵌套
在scss中我们可以使用嵌套的方法指定样式 省去写重复的id选择器
```scss
#content {
  article {
    h1 { color: #333 }
    p { margin-bottom: 1.4em }
  }
  aside { background-color: #EEE }
}
```
```scss
 /* 编译后 */
#content article h1 { color: #333 }
#content article p { margin-bottom: 1.4em }
#content aside { background-color: #EEE }
```
## 2.2 父选择器的标识符&;
在scss解析嵌套时上层的选择器和下层的选择器会被用" "的方式连接，但很多时候我们不希望他如此。通过符号&标识来实现指向他的选择器。
```scss
article a {
  color: blue;
  &:hover { color: red }
}
```
```scss
 /* 编译后 */
 article a { color: blue }
 article a:hover { color: red }
```
这种方式还可以被用于在父选择器之前添加选择器。
```scss
#content aside {
  color: red;
  body.ie & { color: green }
}
```
```scss
/*编译后*/
#content aside {color: red};
body.ie #content aside { color: green }
```
## 2.3 组群选择器（超级强大）
```scss
.container {
  h1, h2, h3 {margin-bottom: .8em}
}
nav, aside {
  a {color: blue}
}
```
```scss
/*编译后*/
.container h1, .container h2, .container h3 { margin-bottom: .8em }
nav a, aside a {color: blue}
```
>注：这种方式在嵌套关系复杂的情况下，优势更为明显。

## 2.4 子组合选择器和同层组合选择器：>、+和~
> `>`选择一个元素的直接子元素,

> `+`选择header元素后紧跟的p元素 `header + p { font-size: 1.1em }`

> `~`选择所有跟在article后的同层article元素 `article ~ article { border-top: 1px dashed #ccc }`

```scss
article {
  ~ article { border-top: 1px dashed #ccc }
  > section { background: #eee }
  dl > {
    dt { color: #333 }
    dd { color: #555 }
  }
  nav + & { margin-top: 0 }
}
```
```scss
/*编译后*/
article ~ article { border-top: 1px dashed #ccc }
article > footer { background: #eee }
article dl > dt { color: #333 }
article dl > dd { color: #555 }
nav + article { margin-top: 0 }
```

## 2.5 属性嵌套
在scss中属性也可以嵌套
```scss
nav {
  border: {
  style: solid;
  width: 1px;
  color: #ccc;
  }
}
```
甚至可以这样
```scss
nav {
  border: 1px solid #ccc {
  left: 0px;
  right: 0px;
  }
}
```
#3. 导入SASS文件;
## 3.1 导入语法
在scss中可以使用`@import`的方式来依赖其他的scss样式文件。

例如：`@import"sidebar"`可以省略.sass或.scss文件后缀
>注：当文件已‘_’为前缀命名时sass解析后不会生成css文件
## 3.2 默认变量值
一般情况下，你反复声明一个变量，只有最后一处声明有效且它会覆盖前边的值。
但 !default 会修改此规则 无论什么顺序，!default总是先被替换。
```scss
$fancybox-width: 400px !default;
.fancybox {
width: $fancybox-width;
}
```
# 4 混合器
当重用大段语法时我们可以使用混和器
```scss
//声明混和器
@mixin rounded-corners {
  -moz-border-radius: 5px;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}
//使用
.notice {
  background-color: green;
  border: 2px solid #00aa00;
  @include rounded-corners;
}
//编译
.notice {
  background-color: green;
  border: 2px solid #00aa00;
  -moz-border-radius: 5px;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}
```
## 4.1 混合器中的CSS规则
简而言之，混合器仍能套用css规则(这个编译的真心强,请仔细看下面的demo)
```scss
//声明混和器
@mixin no-bullets {
  list-style: none;
  li {
    list-style-image: none;
    list-style-type: none;
    margin-left: 0px;
  }
}
//使用
ul.plain {
  color: #444;
  @include no-bullets;
}
//编译
ul.plain {
  color: #444;
  list-style: none;
}
ul.plain li {
  list-style-image: none;
  list-style-type: none;
  margin-left: 0px;
}
```
## 4.2 混合器传参
```scss
//声明混和器
@mixin link-colors($normal, $hover, $visited) {
  color: $normal;
  &:hover { color: $hover; }
  &:visited { color: $visited; }
}
//使用混合器
a {
  @include link-colors(blue, red, green);
}
//Sass最终生成的是：
a { color: blue; }
a:hover { color: red; }
a:visited { color: green; }
```
## 4.3 混合器默认参数值
```scss
@mixin link-colors($normal,$hover: $normal,$visited: $normal){
  color: $normal;
  &:hover { color: $hover; }
  &:visited { color: $visited; }
}
```
如果像下边这样调用：`@include link-colors(red)` `$hover`和`$visited`也会被自动赋值为red。

# 5 选择器继承
```scss
//通过选择器继承继承样式
.error {
  border: 1px solid red;
  background-color: #fdd;
}
.seriousError {
  @extend .error;
  border-width: 3px;
}
```
元素最终的展示效果就好像是class="seriousError error"。

.seriousError不仅会继承.error自身的所有样式，任何跟.error有关的组合选择器样式也会被.seriousError以组合选择器的形式继承，如下代码:
```scss
//.seriousError从.error继承样式
.error a{  //应用到.seriousError a
  color: red;
  font-weight: 100;
}
h1.error { //应用到hl.seriousError
  font-size: 1.2rem;
}
```
