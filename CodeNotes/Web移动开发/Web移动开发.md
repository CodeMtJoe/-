# 📕wbe移动开发
        关于html以及css的基础知识可以去看w3c或者菜鸟教程,这里主要讲移动web开发中的基础只是以及常用的适配.
### 📑MediaQuery
----------------
    MediaQuery媒体查询
    @media screen and (max-width:400px/min-width:400px){
        /*css*/
        当屏幕<=400px/>=400px时的css样式

    };
### 📑Rem
---------
    - 字体单位
        - 值根据html根元素大小而定,同样可以作为宽度,高度单位...
    - 适配原理
        - 将px替换成rem,动态修改html的font-szie适配
    - 兼容性
        - ios 6以上和andoroid 2.1以上,基本覆盖所有流行的手机系统
    1rem=16px;

### 📑Viewport
--------------
    <meta name="viewport" content="width=device-width,initial-scale=1,minimum-scale=1,maximum-scale=1,user-scalable=no" />
+ width 设定布局vieport的特定值(device-width) 布局viewport=设备宽度
+ initial-scale 设置页面的初始缩放
+ 最小/最大缩放
+ ser-scalable用用户能否缩放

### 📑Flex布局
------------
Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。
任何一个容器都可以指定为flex布局.  
```
.box{
    display:flex
}
```
行内元素也可以使用 Flex 布局。
```
.box{
    display:inline-flex
}
```
Webkit 内核的浏览器，必须加上**-webkit**前缀。
```
.box{
      display: -webkit-flex; /* Safari */
      display: flex;
    }
```
🚨注意 设为 Flex 布局以后，子元素的**float**、**clear**和**vertical-align**属性将失效。
#### 📃 1.基本概念
采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。

![图片](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png)

器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。

项目默认沿主轴排列。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。

#### 📃 2.容器属性  
```
flex-direction 决定主轴的方向(即项目的排列方向)
flex-wrap 默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。
flex-flow flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap
justify-content 属性定义了项目在主轴上的对齐方式。
align-items 属性定义项目在交叉轴上如何对齐。
align-content 属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
```
<table><tr><td bgcolor="#FC961B">flex-direction</td><td><font color="#b32ca1">决定主轴的方向(即项目的排列方向)</font></td></tr></table>


![图片](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071005.png)
```
.box{
    display:flex;
    flex-direction:row|row-reverse|column|column-reverse

}
```

- row（默认值）：主轴为水平方向，起点在左端。
- row-reverse：主轴为水平方向，起点在右端。
- column：主轴为垂直方向，起点在上沿。
- column-reverse：主轴为垂直方向，起点在下沿

<table><tr><td bgcolor="#FC961B">flex-warp</td><td><font color="#b32ca1">默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。</font></td></tr></table>

![示意图](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071006.png)


```
.box{
    flex-warp: nowrap | wrap | wrap-reverse;
}
```

- **nowrap**(默认) 不换行

     ![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071007.png)

- **wrap**：换行，第一行在上方。

     ![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071008.jpg)

- **wrap-reverse**：换行，第一行在下方。

     ![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071008.jpg)

 <table><tr><td bgcolor="#FC961B">flex-flow</td><td><font color="#b32ca1">flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap</font></td></tr></table>

     ```
     box {
              flex-flow: <flex-direction> || <flex-wrap>;
            }
     ```

 <table><tr><td bgcolor="#FC961B">justify-content</td><td><font color="#b32ca1">属性定义了项目在主轴上的对齐方式。</font></td></tr></table> 
     
- **flex-start**（默认值）：左对齐
- **flex-end**：右对齐
- **center**： 居中
- **space-between**：两端对齐，项目之间的间隔都相等。
- **space-around**：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071010.png)

 <table><tr><td bgcolor="#FC961B">align-items</td><td><font color="#b32ca1">属性定义项目在交叉轴上如何对齐。</font></td></tr></table> 

 ```
 .box{
    align-items:flex-start|flex-end|center|baseline|stretch
            
            flex-start：交叉轴的起点对齐。
            flex-end：交叉轴的终点对齐。
            center：交叉轴的中点对齐。
            baseline: 项目的第一行文字的基线对齐。
            stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。           
 }
 ```

 ![tp](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071011.png)

  <table><tr><td bgcolor="#FC961B">align-content属性</td><td><font color="#b32ca1">多行子元素的对齐方式,如果只有一行就不会有效果</font></td></tr></table> 

```

.box {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;

            flex-start：与交叉轴的起点对齐。
            flex-end：与交叉轴的终点对齐。
            center：与交叉轴的中点对齐。
            space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
            space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
            stretch（默认值）：轴线占满整个交叉轴                

}

```

![tp](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png)

#### 📃 2.项目(子元素)属性  
以下6个属性设置在项目上

- **order** 属性定义子元素的排列顺序。数值越小，排列越靠前，默认为0。
    
    ![tp](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071013.png)

- **flex-grow**  属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
    
    ![tp](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071014.png)
    
    如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

- **flex-shrink**  属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

![tp]('http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071015.jpg')
如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。

负值对该属性无效。
- **flex-basis** 属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。

- **flex** 属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

```
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```
该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

- **align-self** 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

```
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

![tp](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071016.png)
