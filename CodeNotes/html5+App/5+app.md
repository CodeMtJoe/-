#5+app开发笔记📕
很早之前就想开发一个app,但是苦于学习成本高,一直没有着手
安卓开发😭,但是最近了解到有一款国产框架可以实现我这个愿望,
于是乎便开始记录并用起来,那就是**5+APP**
## 什么是html5+❓
>html5+是Dcloud提供H5强化引擎,可以把HTML5 App打包为原生App,并且达到原生的功能和体验。
>说白了就是原本只能原生APP才能实现的功能，现在可以通过html5+这个强化引擎作为桥梁，你通过调用plus.*方法实现，
>也就是你可以通过书写js代码实现android和ios两套的原生功能。html5+封装了一些最常用的功能，并向W3C提交了作为标准的提案.  
> 
    总结:使用了html5+就能开发一个具有与原生APP功能一样的体验
## 什么是mui❓
HBuilder自带的一套UI套件，模拟了目前APP应用的按钮了，显示条目了，等等UI元素。
## 什么是Native.js❓
这个东西可以在javascript中调用安卓和ios的原生api,是Hbulider组织开发的一个javascruot引擎,使用特定语法就能调用原生的API了

## mui与html5+有什么关系❓
>mui是Dcloud官方推出的一个基于html5+标准的框架，同时拥有h5组件和原生组件，原生组件依赖于html5+运行环境，也就是原生app里面的webview组件（能加载显示网页，可以将其视为一个浏览器），所以mui里面的原生组件不能用于浏览器环境，可以通过mui里面的mui.os.plus进行判断，如果是plus环境会返回true，否则会返回undefined。开发者可以根据自己的需要进行代码适配，对于APP使用增强的原生组件，对于普通浏览器里面运行的页面使用h5组件。同时用户还可以使用mui.os.android、mui.os.ios及mui.os.wechat对平台进行检测，然后书写不同的逻辑代码。对于mui里面没有封装的原生组件，大家可以根据自己的需要基于html5+标准和native.js语法进行个性化定制。因此这里我们可以有一个基本影响就是我们开始可以直接上手mui，不过需要明白mui与其他UI框架的区别在于，mui拥有独有的原生组件，而且这个是依赖于html5+标准的，所以mui里面的很多组件实现方法甚至用户就是html5+里面的标准写法，对html5+标准有一定了解有助于我们理解mui的一些使用方法.
> 
    总结:Mui是基于html5+开发的UI组件框架,原生组件依赖于5+运行环境
    也就是mui里面的组件不能用于浏览器环境.

## 起步📑
![文件结构图](https://s2.ax1x.com/2019/06/19/VOqDGd.png)  
📁css文件夹是存放*.css文件（层叠样式表）的，主要是对页面布局进行修饰，mui.css是修饰mui框架组件的样式表，通过以mui-*为前缀的类选择器进行修饰，也就是你只需要引入mui.css文件，建议放在```<header></header>```之间，然后按照mui一些固定结构去写就可以实现一些常用组件。组件使用方法可以查看后面的章节或者直接在【创建移动APP】工程时选择【Hello MUI】创建一个演示APP项目。

📁fonts文件夹下的mui.ttf是矢量图标字体文件，这里是mui框架内置的图标，具体图标可以查看hello mui演示APP里面的icon(图标)查看，使用用法可以在演示APP项目查看examples文件夹下的icons.html，这个是基于Iconfont-阿里巴巴矢量图标库,用户可以自定义图标，具体方法请看这里mui如何增加自定义icon图标,因为mui.css里面是通过@font-face下的src: url('../fonts/mui.ttf') format('truetype');引入，若图标没有正常显示，请查看是否文件的路径是否正确。

📁js文件夹下的mui.js文件是与mui.css配合使用的，主要是实现一些具有动态效果的组件，mui.js建议放在</body>;前，mui.js暴露出来的公共方法是mui对象，mui.js只封装与组件相关的一些方法，开发者可以根据自己的需要自己选用其他js组件，官方推荐开发者使用原生js去书写，因为原生js效率更高，对于APP性能更佳。

📁mui.min.css和mui.min.js文件是经过压缩后的文件，不影响使用，部署到实际项目中建议使用压缩版。

📁unpackage文件夹不会被打包到APP安装包里面，有些文件不希望被打包，可以存放在这个文件夹下，当APP执行了在线打包后，这个文件夹下也会默认生成release文件夹（存放APP打包生成的安装包文件），res会存放启动图标等文件。

📄manifest.json是APP配置文件，就是定义APP打包所需要的基本设置信息，默认为界面模式也有代码模式。具体配置介绍请查看 manifest配置指南。

📄index.html为APP默认的页面入口文件，可以通过设置manifest.json中的【页面入口】进行修改

##概览📑
深入了解底层结构的关键部分，包括我们让 web 开发变得更好、更快、更强壮的最佳实践。  
[MUi开发文档](http://dev.dcloud.net.cn/mui/window/#subpage)
### 📑界面初始化
```
界面初始化,让一切都准备好.
miu.init();
```
### 📑H5plus初始化 
```
h5+初始化,所有模块功能都准备好
miu.plusready(function(){
    //获取本界面对象
    miu.alert(plus.webview.currentWebview())
    });
```
### 📑创建子页面
在app开发中,会出现共用导航和标题栏,每次打开页面都是要重新渲染的,这样容易出现卡头卡尾的问题.
使用mui的解决方法:
将页面分成主页面和内容页面,主页面显示标题栏,底部选项卡等;内容页面显示具体需要滚动的页面.在主页面调用miu.init()方法初始化内容页面.
```
miu.init(function(){
    subpage:[{
        url:'list.html',
        id:'list.html',
        stlye:{
            //内容页面显示的区域,这样就不会覆盖了标题栏和底部选项卡
            top:'45px',
            bottom:'45px',
        }
        }]
    })
```
![](https://s2.ax1x.com/2019/06/19/VOvbUf.png)
### 📑打开新页面💥
打开新页面是用的非常多的,app的很多操作都需要这个操作.
具体语法:
```
mui.openWindow({
    url:new-page-url,
    id:new-page-id,
    styles:{
      top:newpage-top-position,//新页面顶部位置
      bottom:newage-bottom-position,//新页面底部位置
      width:newpage-width,//新页面宽度，默认为100%
      height:newpage-height,//新页面高度，默认为100%
      ......
    },
    extras:{
      .....//自定义扩展参数，可以用来处理页面间传值
    },
    createNew:false,//是否重复创建同样id的webview，默认为false:不重复创建，直接显示
    show:{
      autoShow:true,//页面loaded事件发生后自动显示，默认为true
      aniShow:animationType,//页面显示动画，默认为”slide-in-right“；
      duration:animationTime//页面动画持续时间，Android平台默认100毫秒，iOS平台默认200毫秒；
    },
    waiting:{
      autoShow:true,//自动显示等待框，默认为true
      title:'正在加载...',//等待对话框上显示的提示内容
      options:{
        width:waiting-dialog-widht,//等待框背景区域宽度，默认根据内容自动计算合适宽度
        height:waiting-dialog-height,//等待框背景区域高度，默认根据内容自动计算合适高度
        ......
      }
    }
})
```
打开新页面的时候,默认是当页面loaded事件发生后自动显示,这样如果打开的新页面比较大的话会产生白屏的现象,因为数据没有加载完,为了有更好的用户体验,在```autoshow```参数中设置为false,让新页面不自动显示  
**实现当新页面加载完之后才显示新页面的效果**  
方法如下:
```
            show:{
                  autoShow:false,//设置为fales不自动显示新页面
                  aniShow:'zoom-fade-out'；
                  duration:'350';
                },
            waiting:{
              autoShow:true,//自动显示等待框，默认为true
              title:'给力加载中...',//等待对话框上显示的提示内容

              }

            //需要打开的新页面
            mui.plusReady(function(){
                //关闭等待框
                plus.nativeUI.closeWaiting();
                //找到自己
                var self=plus.webview.currentWebview();
                //显示页面 参数:显示方式,毫秒
                self.show('zoom-fade-out','350');
            })

```

### 📑关闭页面💥
- 只需要在标签内添加class为```.mui-action-back```的类,点击这个标签就能关闭
- mui框架封装了页面右滑关闭功能,默认未启用(哪个页面就启用此操作只针对打开过的页面才有效,并非整个APP,哪个页面需要这个,)  
     ```
     mui.init({
        swipeBack:true //启用右滑关闭功能
    });
     ```
- mui框架默认会监听安卓back按键,也就是点击返回键就会关闭页面;如果想关闭,可以关闭按键监听,注意的是ios无效,因为他瞄没有返回键啊.但是ios默认快速右滑可以关闭页面  
    ```
    mui.init({
        keyEventBind: {
            backbutton: false  //关闭back按键监听
        }
    });
    ```
