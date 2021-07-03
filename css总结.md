[TOC]

# 1、em、rem、px

- px是相对于显示器屏幕分辨率而言（默认字体高16px）；

- em是相对于当前对象内文本的字体尺寸（1em=16px），声明font-size=62.5%，故1em=10px，em会继承父级元素的字体大小；
- rem（root em）：相对HTML根元素，只需要修改根元素就可以成比例调正所有字体大小，又可以避免字体大小逐层复合的连锁反应；

# 2、常用字符实体

| `<br/>` | 换行 | &lt    | <    | &amp  | &    |
| ------- | ---- | ------ | ---- | ----- | ---- |
| &nbsp   | 空格 | &gt    | >    | &copy | ©    |
| &reg    | ®    | &trade | ™    | &yen  | ¥    |

- 如果需要打印 `<br/>` 到屏幕上，则需要使用转义字符 ，其表示为` &lt br/ &gt`

```html
<li>&lt</li>
<li>&lt;p&gt</li>
<li>&lt;hr /&gt</li>
<li>&lt;img /&gt</li>
注释：空格就是空格，；可以区分前后文，不表示为空格；
<p>使用 br 元素<br>在文本中<br>换行。</p>
```

```css
font-size:20px;
line-height:2;<!--2倍-->
```

# 3、页面布局

## 3.1、 position：absolute、relative、fixed、static



### 3.1.1、left和margin-left

- left边框靠左侧父级的位置，父级需要有position：relative；
- margin-left是指边框向左扩展的宽度；margin-left的负值：表示反方向；margin-left: 100%（表示上级标签容器的百分比）
- left正值表示左边框距离父级左边框左侧的距离，负值表示左边框距离父级左边框右侧的位置；
- block元素有margin；

## 3.2、 **display：**incline、block、incline-block、flex、none

```css
vertical-align: top;/*incline-block*/
```

inline：span、a、b、strong、em、img、imput、textarea、

block：div、p、h、ul、dl

inline-block：

- display：隐藏对应的元素不占据原来的空间。visibility：隐藏对应的元素仍占据空间位置。

## 3.3、float、flex、grid布局

left、right；（浮动布局分栏）

- 两个同级div，设置float：left和宽高后，不会覆盖，顺序排列；
- 只有普通文档流中块框的**垂直边界margin**才会发生边界叠加。行内框、浮动框或绝对定位框之间的边界不会叠加。通过父级添加一个垂直边框或填充padding，空白边就不再叠了，而且元素的高度就是它包含的子元素的顶部和底部空白边边缘之间的距离。

### 3.3.1、**两栏：**

左侧nav：（float：left；width：200px；height）；右侧content：（margin-left：200px；height）

### 3.3.2**三栏：**

**法一：**左侧（float：left；width：200px；height）；右侧right（float：right；width：200px；height）;中间content（margin-left：200px；margin-right：200px；）或（margin：0 200px）

**法二：**左中右position

法三：flex，左右设置宽度，中间 设置flex:1;父容器设置display：flex；

**圣杯布局**

```xml
        <body>
            <div class="center contain">center</div>
            <div class="left contain">left</div>
            <div class="right contain">right</div>
        </body>
```

.contain{float: left;height: 300px; }  center设置width：100%，left、right为左右边宽；



**双飞翼布局**

```
  <body>
    <div class="center contain">
      <div class="innner-center ">center</div>
    </div>
    <div class="left contain">left</div>
    <div class="right contain">right</div>
</body>
```

让`<a>`浮动，则可以通过设置其float：left；

```css
//写个小三角形
<div class="demo">这是一个测试</div>
.demo:after{
    content: '';
    display: inline-block;
    width: 0;
    height: 0;
    border: 8px solid transparent;
    border-left: 8px solid #AFABAB;//箭头朝向右
    /*border-right: 8px solid #AFABAB;//箭头朝向左*/
    position: relative;
    top: 2px;
    left: 10px;
}
```

清除浮动（content用在伪类上）

```
.clearFixed:after{
	content:"";
	display:block;
	clear:both;
}
```

`<img alt="它规定在图像无法显示时的替代文本">`



## 3.4居中

css中文字的水平垂直居中： line-height  然后设置为盒子高度height；text-align： center;

## 3.5三角形

[纯CSS绘制三角形（各种角度）](https://www.jb51.net/article/42513.htm)

**下边border-bottom 控制了三角形的高（100px）**，表示底边的宽度，即三角形高

**左右两边的 border分别控制了三角形的底边长的两部分**（加起来共 200px），左边代表左边框的宽度，但是隐藏了，右边代表右边框宽度，同时隐藏，即为顶点到右边的宽度。

```
//等边，有底边的向上三角形
.d1 {
    width: 0;
    height: 0;
    border-left: 100px solid transparent;
    border-right: 50px solid transparent;
    border-bottom: 100px solid red;
}
//有右侧边的向左三角形
.d2{
     margin-left: 110px;
     width: 0; 
     height: 0;
     border-width: 100px;
     border-style: solid;
     border-color:  transparent  #0099CC transparent  transparent;//上右下左
}
```

4、使用transition属性也能够实现过渡动画效果，但是略显粗糙，因为不能够更为精细的控制动画过程，比如只能够在指定的时间段内总体控制某一属性的过渡，而animation属性则可以利用**@keyframes**将指定时间段内的动画划分的更为精细一些。

`<div>`标签的data-* 属性用于存储私有页面后应用的自定义数据，而且data-* 属性可以在所有的 HTML 元素中嵌入数据。

3.6、BFC

**块格式化上下文（Block Formatting Context，BFC）**

- 创建条件：
  - float的值不是none
  - position的值是absolute、fixed；position的值不是static或者relative。
  - display的值是inline-block、flow-root、table-cell、table-caption、flex或者inline-flex、grid或者inline-grid
  - overflow的值不是visible

- Box垂直方向的距离由margin决定。属于**同一个**BFC的两个相邻Box的margin会发生重叠。

# 5、标签

## 5.1、a标签

`< a rel="nofollow" href="index.html"  target="_blank" >跳转打开一个新的页面（不刷新本页）</a>`

`nofollow`：告诉搜索引擎不要此网页上的链接或不要追踪此特定链接。<a> 标签的 rel 属性用于指定当前文档与被链接文档的关系。

`target="_blank"`：跳转打开一个新的页面（不刷新本页）

a标签有四个“状态”的先后过程是：a:link ->a:hover ->a:active ->a:visited。

- 超链接的LVHA原则
- （a:link超链接被点前状态）、（a:visited 超链接点击后状态）、（a:hover  悬停在超链接时）、（ a:active点击超链接时）

# 6、盒模型

```css
box-sizing: border-box;  // 设置为IE模型（height包括boeder+padding+content）
box-sizing: contetn-box; // 设置为标准模型（height包括content）
```

# 7、轮播图（swiper）

轮播图：自动播放，轮播---->scroll-view是指滑动连续；

href="#"与href="javascript:void(0)"的区别：

- **#** 包含了一个位置信息，默认的锚是**#top** 也就是网页的上端。

- 而javascript:void(0), 仅仅表示一个死链接。

# 8、工具

8.1 wow.js ([dowebok ](https://www.dowebok.com/)) `https://www.dowebok.com/`







SVG.js是一个轻量级的JavaScript库，让您可以轻松地操纵SVG和让SVG产生动画。

8、注意事项：

- 不要滥用`<br>`
- 不用`<table>`标签布局网页
- 