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