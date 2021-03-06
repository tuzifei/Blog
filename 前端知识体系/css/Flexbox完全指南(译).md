
# Flexbox
# [Flexbox（弹性盒模型）布局完全指南](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
> 这个指南讲诉了flexbox的所有内容，重点介绍了父元素（`flex`容器）和子元素（`flex`元素）的所有不同可能属性。它还包括历史记录、演示、模式和浏览器支持图表。
## 背景
`Flexbox`布局（弹性盒模型）模块的目的在于提供一种更有效的方法在容器中的项之间布局、对齐和分配空间，即使它们的大小未知或是动态的(因此使用“`flex`一词)。

`flex`布局背后的主要思想是让容器能够更改其项（`item`）的宽度/高度(和顺序)，以最佳地填充可用空间(主要是为了适应各种显示设备和屏幕大小)。`flex`容器（`container`）扩展项以填充可用的空闲空间，或者收缩项以防止溢出。

最重要的是，与常规布局(基于垂直的块和基于水平的内联块)相比，`flexbox`布局是与方向无关的。虽然这些常规方法在页面上运行得很好，但是它们缺乏灵活性来支持大型或复杂的应用程序(特别是在改变方向、调整大小、拉伸、收缩等方面)。

**注意**:`Flexbox`布局最适合应用程序的组件和小规模布局，而`Grid`布局则适用于更大规模的布局。

## 基本术语
由于`flexbox`是一个完整的模块而不是一个单独的属性，所以它涉及到很多东西，包括它的整个属性集。其中一些是要在容器上设置的(父元素，称为“`flex container`”)，而其他的是要在子元素上设置的(称为“`flex item`”)。

如果“常规”布局基于块和内联流方向，那么`flex`布局则基于“`flex-flow`方向”。请从规范中查看这个图，解释`flex`布局背后的主要思想。
![](https://css-tricks.com/wp-content/uploads/2018/11/00-basic-terminology.svg)
`item`将沿着主轴（`main axis`）(从主轴开始（`main-start`）到主轴结束（`main-end`）)或纵轴()(从纵轴开始（`cross-start`）到纵轴结束（`cross-end`）)布置。

**main axis**：伸缩容器的主轴是放置伸缩项的。**注意，它不一定是水平的，它取决于`flex-direction`属性(参见下面)**。

**main-start|main-end**：`flex`项被放置在容器中，从`main-start`到`main-end`。

**main size**：伸缩项（`flex item`）的宽度或高度，无论在主维度（`main`）中是哪个，都是项的主尺寸。`flex item`的`main``size`属性是“`width`”或“`height`”属性，两者在主维度中都有。

**cross axis**：垂直于主轴（`main axis`）的轴称为横轴。它的方向取决于主轴方向。

**cross-start|cross-end**：伸缩线由`item`填充，并从伸缩容器的`cross-start`侧开始，一直到`corss-end`侧，然后放入容器中。

**cross size**：`flex item`的宽度或高度，无论在`corss`维度中是哪个，都是`item`的`cross size`。`cross size`属性是在`corss`维度中的“宽度”或“高度”中的任何一个。
#### [返回顶部](#flexbox)
父元素属性(`flex container`) | 子元素属性(`flex item`)
------ | ------
![父元素属性(`flex container`)](https://css-tricks.com/wp-content/uploads/2018/10/01-container.svg) | ![子元素属性(`flex item`)](https://css-tricks.com/wp-content/uploads/2018/10/02-items.svg)
**dispaly** | **order**
  | ![](https://css-tricks.com/wp-content/uploads/2018/10/order.svg)
定义了一个`flex`容器，内联或块取决于它给定的值。它为所有直接子元素启用`flex`上下文<br>**注意**：`css`列对`flex`容器没有影响 | 默认情况下，`flex item`按源顺序排列。然而，`order`属性控制它们在`flex`容器中出现的顺序
.container{<br>display:flex;//或者 inline-flex<br>} | .item{<br>order:<整数值>;//默认为0<br>}
**flex-direction** | **flex-grow**
![](https://css-tricks.com/wp-content/uploads/2018/10/flex-direction.svg) | ![](https://css-tricks.com/wp-content/uploads/2018/10/flex-grow.svg)
这将建立主轴，从而定义放置在`flex`容器中的方向`flex item`。<br>`flexbox`(除了可选的包装)是一个单向布局概念。可以将`flex item`主要放在水平行或垂直列中 | 这定义了`flex item`在必要时增长的能力。<br>它接受一个作为比例的无单位值。它指定`item`在`flex`容器中应该占用多少可用空间。<br>如果所有项目都将`flex- growth`设置为1，容器中剩余的空间将平均分配给所有子元素。如果其中一个子元素的值为2，那么剩余的空间将会占用两倍于其他元素的空间(或者至少它会尝试这样做)<br>**注意**：负数无效
.container{ <br>flex-direction:row / row-reverse / column / column-reverse;<br>}<br><br>**row(默认)**:`ltr`是从左到右；`rtl`是从右到左;<br>**row-reverse**：`ltr`是从右到左，`rtl`是从左到右<br>**column**:从上到下<br>**column-reverse**：从下到上| .item{<br>flex-grow: <数值>; //默认为0<br>}
**flex-wrap** | **flex-shrink**
![](https://css-tricks.com/wp-content/uploads/2018/10/flex-wrap.svg) |  [返回顶部](#flexbox)
默认情况下，`flex item`都会试着放在一行上。您可以更改此属性，并允许根据需要使用此属性对项进行包装 | 这定义了`flex item`在必要时的伸缩能力
.container{<br>flex-wrap: nowrap / wrap / wrap-reverse;<br>}<br><br>**nowrap（默认）**：所有`flex item`将在一条线上<br>**wrap**：`flex item`将会从上到下分为多行<br>**wrap-reverse**：`flex item`将会从下到上分为多行 | .item{<br> flex-shrink:<数值>;<br>}<br>负数无效
**flex-flow(用于父felx容器元素** | **flex-basis**
这是一个简化的`flex-direction`和`flex-wrap`属性，它们一起定义`flex`容器的主轴和交叉轴。默认值是`row nowrap`。 | 这定义了在分配剩余空间之前元素的默认大小。它可以是一个长度(例如20%，5rem，等等)或者一个关键字。<br>`auto`关键字的意思是“查看我的宽度或高度属性”(这是由`main-size`关键字临时完成的，直到被弃用)。<br>`content`关键字的意思是“根据项目的内容调整大小”——这个关键字还没有得到很好的支持，因此很难进行测试，而且更难知道它的兄弟`max-content`、`min-content`和`fit-content`做了什么。
felx-flow: <'felx-direction'>  <'flex-wrap'> | .item{<br>flex-basis: <长度> / auto; //默认是auto<br>}<br>如果设置为0，则不考虑内容周围的额外空间<br>如果设置为`auto`，则根据其`flex-growth`值分配额外的空间
**justify-content** | **flex**
![](https://css-tricks.com/wp-content/uploads/2018/10/justify-content.svg) |  [返回顶部](#flexbox)
这定义了沿着主轴的对齐。<Br>当一行中的所有`flex item`都是不灵活的，或者都是灵活的，但已经达到最大大小时，它可以帮助分配剩余的额外空闲空间。当项目溢出行时，它还对它们的对齐方式施加一些控制。  | 这是`flex-growth`、`flex-shrink`和`flex-base`组合的简写。<br>第二个和第三个参数(`flex-shrink`和`flex-base`)是可选的。默认值是0 1 auto。
  .container{<br>justify-content: flex-start / felx-end / center / space-around / space-evently;<br>}<br>**flex-start(默认)**：`item`向行的开始聚集**flex-end**：`item`往行尾聚集<br>**center**：`item`在行内居中<br>**space-between**：`item`在行内均匀分布，第一个在行首，最后一个在行尾<br>**space-around**：`item`在行内均匀分布，周围空间相等，在视觉上并不是相等的<br>**space-evently**：`item`是均匀分布的，任何两个`item`之间的间距(以及边缘的空间)是相等的 | .item{<br>flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]<br>}<br>建议您使用这个简写属性，而不是设置各个属性。简单地设置其他值。
  **align-items** | **flex-atart**
 ![](https://css-tricks.com/wp-content/uploads/2018/10/align-items.svg) | ![](https://css-tricks.com/wp-content/uploads/2018/10/align-self.svg)
 这定义了`flex item`如何沿着当前行上的交叉轴的默认行为。<br>可以将其视为交叉轴(垂直于主轴)的`justify-content`版本。   | 这允许为单个`flex`项重写默认对齐(或由`align-items`指定的对齐)<br>
 .container{<br>align-items: stretch / flex-start / flex-end / center / baseline;<br>}<br>**stretch(默认)**：拉伸填充容器(仍然考虑最小宽度/最大宽度)<br>**flex-start**：`item`以`cross-start`边为边对齐<br> **flex-end**：`item`以`cross-end`线为边对齐<br>**center**：`item`在`cross-axis`居中<br>**baseline**：`item`沿它们的基线对齐| .item{<br> align-self: auto / flex-start /flex-end / center / baseline / stretch;<br>}<br>**注意**：`float`、`clear`、`vertical`对一个`flex item`没有影响
  **align-content**| 
  ![](https://css-tricks.com/wp-content/uploads/2018/10/align-content.svg) |  [返回顶部](#flexbox)
  当交叉轴中有额外的空间时，这将使`flex`容器的行对齐，类似于调整内容在主轴中对齐单个条目的方式<br>**注意**：
.container{<br>aligbn-content: flex-start / flex-end / center / space-between / space-around / stretch;<br>}<br>**flex-satrt**：行包装到容器顶部<br>**flex-end**：行包装到容器底部<br>**center**：行在容器中<br>**sapce-between**：行均匀分布，第一行在容器顶部，最后一行在容器底部<br>**strecth(默认)**：行拉伸填充容器剩余空间
  
 ## 例子
 #### 居中
 以一个很简单的例子解决一个常见的问题：**居中显示**
 
```
.parent{
  dispaly:flex;
  height:300px;
}
.child{
  width:100px;
  height:100px;
  margin:auto;
  }
```
这取决于在`flex`容器中设置`margin`为`auto`的空白会吸收额外的空间。因此，设置`auto`的垂直边距将使项目完美地位于两个轴的中心。
#### [返回顶部](#flexbox)
#### 自适应
现在让我们使用更多的属性。考虑一个包含6个项的列表，它们都具有固定的尺寸，但是它们可以**自动调整大小**。我们希望它们**均匀地分布在水平轴上**，以便在调整浏览器大小时一切正常(没有媒体查询!)。
```
.flex-container{
  dispaly:flex;
  flex-flow:row wrap;
  justify-content:space-around;
}

```
#### 响应式
我们再试试其他的，假如我们有靠右对齐的导航栏，我们希望它们在中等尺寸屏幕中居中以及在小屏幕中单列显示。
```
.navigation{
  display:flex;
  flex-flow:row wrap;
  justify-content:flex-end;//交叉轴的右边显示
}
//中等屏幕
@media all and (max-width:800px){
  .navigation{
    justify-content:space-around;
  }
}
//小屏幕
@media all and (max-width:500px){
  .navigation{
    flex-direction: column;
   }
}
```
## 其他资源
[Flexbox in the CSS specifications](https://www.w3.org/TR/css-flexbox-1/)

[Flexbox at MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)

## 浏览器支持
Chrome | Safari | Firefox | Opera | IE | Edge | Android | IOS
------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ 
20-（old）<br>21+ (new) | 3.1+ (old)<br>6.1+ (new) | 2-21 (old)<br>22+ (new) | 12.1 (new) | 10 (tweener)<br>11+ (new) | 17+ (new) | 2.1 +(old)<br>4.4 (new) | 3.2 (old)<br>7.1 (new)
