## todo
- https://www.tmall.com/?from=m#/main
- 网易移动端
- 研究一些大站的移动端再来说一下结论
- https://www.cnblogs.com/whowhere/p/7651661.html
- http://www.cnblogs.com/lixinglong/p/7889526.html


## 推荐布局工具
- http://koala-app.com/index-zh.html
    + 推荐理由：很多同学对npm环境不熟悉,编辑器的less,sass编译环境一旦出问题就搞不定了，用此工具完全不用配置任何环境，安装好即可使用
- 移动端调试工具:vConsole
    + 推荐理由：手机上不能按f12打开控制台
- browserSync
    + 推荐理由：每次改代码都要刷新浏览器，太麻烦了
    + cnpm install -g browser-sync
    + browser-sync start --files "*.*" --server (一定要是双引号)


## 响应式布局
- 如果有一个页面，需要能在pc上正常适配，也能在移动端上适配，我们可以称之为响应式
- 代表：
    + http://expo.bootcss.com/
    + https://www.microsoft.com/zh-cn
- 原理：媒体查询

- 为什么响应式并不值得去推崇
    + 响应式是当时Pc端占主流市场下的一种妥协的技术,响应式的思路是先在pc端做好之后，再考虑在移动端通过媒体查询让某些标签隐藏或者改变样式，是一种以pc为主要考虑的思维方式，用一种方案来解决两个问题，注定了性能会十分的低下，现在是移动端的时代，大部分的新创公司对pc端基本上不太重视
    + 刚成立的公司，快速制作一个官网，等以后有钱了，肯定还是会pc端一套，移动端一套，分开写
    + 用"廉价"的bootstrap搭建而成，一个只会php,java的技术人员只要理解了栅格式的原理，照着文档就像搭建积木一样就能写出来一个页面
    + 拉勾网上并没有多少招聘信息刻意强调会bootstrap,会响应式
    + 响应式在国内基本上没有推广开
    + 一般需要给客户看的网站，不大可能用响应式，因为响应式的页面不能做一些很复杂的效果(为什么淘宝官网不用响应式)
    + 只有公司内部项目考虑用bootstrap的可能性大一些
    
# 移动端布局

## 懒人捷径
少废话，我不想懂原理，你就告诉我怎么做就行了-->
直接看《推荐布局思路》

## 布局思路

### 为什么移动端布局如此混乱
+ css这套技术系统本身十分的混乱，基本上可以说毫无规律可言，依赖于技术人员的熟练程度而不是逻辑更多一些
+ css历经了多个时代的升级，每一次升级之后，新的技术标准和旧的基本上没有任何关联
    + table布局
    + div+css布局
    + flex布局
    + grid布局
+ 手机终端市场的混乱
    + 各种尺寸的手机
    + 由iphone的retina技术带来的dpr的混乱

### 基本概念的理解

#### 物理设备像素
思考：为什么手电筒只能发出一种颜色的光，而我们的屏幕能发出这么多种颜色的光?
因为我们的屏幕是由无数个小的手电筒组成的，每个点可以发不同的颜色的光，最后就组成了我们看到的彩色的效果。
https://baike.baidu.com/pic/%E4%BD%8D%E5%9B%BE/1017781/0/b03533fa828ba61e23dfd8614034970a304e594e?fr=lemma&ct=single#aid=0&pic=b03533fa828ba61e23dfd8614034970a304e594e
每张图片都是由色点组成的，每个色点称为一个像素。一张图片由30万个色点组成，这个图片的像素就是30W。我们常说相机是多少像素，这个像素就是说这款照相机的感器件有多少个，有100W个感光器件的相机就是100W像素的相机，有4000W个感光器件的相机就是4000W像素，以此类推。一台100W像素的相机拍摄的照片洗成5寸的照片会比洗成6寸清晰一点。

#### 屏幕分辨率
屏幕分辨率是屏幕每行的像素点数*每列的像素点数，每个屏幕有自己的分辨率。屏幕分辨率越高，所呈现的色彩越多，清晰度越高。

结论： 
1. 像素的单位本质上是：个数，100像素你可以理解成你有100个手电筒
2. 同样大小(比如1cm*1cm大小的矩形)，里面的像素越多，画面越清晰

## css像素
- 在pc端1css像素相当于1物理设备像素
- 试验：缩放网页，观察你写的1px会变大变小

## 思考
我们的手机分辨率是640*1136(iphone 5和iphone 5s的物理设备分辨率)，如果我们打开一个纯粹pc端的网站会出现什么情况?
(比如jumei.com,min-width是1090px,在pc端的我的电脑的设备宽度是1280,通过screen.width进行检测)
我们会发现网站会缩小到我们可以看到整个网站(www.jubi.com)


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
    *{
        margin:0;
        padding:0;
    }
    </style>
</head>
<body>
    <div style="width:1200px;height:100px;background:red;"></div>
</body>
</html>
```

如果我们尝试加上：

```html
<meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0"/>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0"/>    
    <title>Document</title>
    <style>
    *{
        margin:0;
        padding:0;
    }
    </style>
</head>
<body>
    <div style="width:1200px;height:100px;background:red;"></div>
</body>
</html>
```

则会发现，有滚动条了,因为禁止缩放了

在iphone 5下面,我们如果不想出现滚动条，则必须如下的写法：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0"/>    
    <title>Document</title>
    <style>
    *{
        margin:0;
        padding:0;
    }
    </style>
</head>
<body>
    <div style="width:320px;height:100px;background:red;"></div>
</body>
</html>
```


## dpr
1个css像素占多少物理设备像素

思考：iphone 5或者iphone 5s一屏幕能看到的极限是多少宽度?
应该是320(这是默认的可视区的css宽度) * 2 = 640px

以上，我们学习完了所有关于移动端布局相关的概念，接下来，我们来聊一聊布局的思路

### 布局思路


假如我们有640px的设计稿，我们如何才能让用户全部看到呢?

### 思路一：百分比布局
把尺寸除以2，比如我们量出来的是640px ---> 实际上我们只写320px


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0"/>    
    <title>Document</title>
    <style>
    *{
        margin:0;
        padding:0;
    }
    </style>
</head>
<body>
    <div style="width:320px;height:100px;background:red;"></div>
</body>
</html>
```

如果是iphone 6怎么办? iphone 6的宽度是375px

由于320和375的宽度其实差别不大，我们可以不定宽度,也就是把整体宽度设定为100%，然后其他的全部量出来是多少

#### 布局方法
- 拿到设计师给我们的设计稿之后(推荐640px),把所有量出来的尺寸除以2即可
- 遇到等分就用百分比
- 左浮动 + 右浮动(导航部分实现、折扣推荐导航部分) --> 适合于所有的元素宽度固定的
- 左浮动 + padding挤(见超值折扣推荐内容部分) 本质上元素大小在任何尺寸下面都是一致，改变的其实是元素与元素之间的间距大小 --> 适合一个元素宽度固定，另一个宽度自适应


#### 示例
- http://m.duba.com/
- http://m.lagou.com/


#### 常用布局技巧
多列等分 -> 百分比等分 左侧固定宽度 + 右侧自适应宽度 思路一 -> 左侧左浮动+右侧环绕在右侧 思路二 -> 父级给padding-left，预留出来左侧区域的宽度，左侧用绝对定位上去，右侧用百分百宽度 左侧自适应 + 右侧固定宽度 思路一 -> 左侧用百分百宽度,右侧用绝对定位上去 左右固定宽度 + 中间自适应 思路一 -> 左侧左浮动 + 中间百分之百（中间部分再分为左侧百分之百+右侧右浮动） 思路二 -> 左侧左浮动 + 中间百分之百 + 右侧右浮动 （负margin法减掉左右侧） 思路三 -> 左右绝对定位 + 中间百分之百（父元素padding-left,padding-right预留左右侧的位置） 左中右全自适应 -> 全部用百分比 font-size、padding,margin,height直接量像素（当然像当当网是把所有的尺寸用了rem来写） 小的地方可以用display:inline-block;让几个容器放在一排 小图标之类的，可以考虑用::before,::after来实现 小的图标用svg,base64或者Iconfont（字蛛 http://font-spider.org/） 另类圣杯布局（研究国美移动端的时候看到的）： .left+.right+.center -> 左左浮，右右浮，中间用margin正值来减宽度

#### 百分比布局的缺点
在大屏幕的手机下显示效果会变成有些页面元素宽度被拉的很长，但是高度还是和原来一样，实际显示非常的不协调，这就是流式布局的最致命的缺点，往往只有几个尺寸的手机下看到的效果是令人满意的，其实很多视觉设计师应该无法接受这种效果，因为他们的设计图在大屏幕手机下看到的效果相当于是被横向拉长来一样。流式布局并不是最理想的实现方式，通过大量的百分比布局，会经常出现许多兼容性的问题，还有就是对设计有很多的限制，因为他们在设计之初就需要考虑流式布局对元素造成的影响，只能设计横向拉伸的元素布局，设计的时候存在很多局限性。

### 思路二:rem布局

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0"/>    
    <title>Document</title>
    <style>
    *{
        margin:0;
        padding:0;
    }
    </style>
    <script>
        ;(function (doc, win, undefined) {
          var docEl = doc.documentElement,
            resizeEvt = 'orientationchange' in win? 'orientationchange' : 'resize',
            recalc = function () {
              var clientWidth = docEl.clientWidth;
              if (clientWidth === undefined) return;
              docEl.style.fontSize = 20 * (clientWidth / 320) + 'px';
            };
          if (doc.addEventListener === undefined) return;
          win.addEventListener(resizeEvt, recalc, false);
          doc.addEventListener('DOMContentLoaded', recalc, false)
        })(document, window);
    </script>
</head>
<body>
    <div style="width:16rem;height:100px;background:red;margin:0 auto;font-size:0.7rem;">
        测试测试
    </div>
</body>
</html>
```

#### 如何理解rem布局
思考一个问题，假如我们的设计稿是750px,我们量出来一个盒子的宽度是75px,那么在640px下面，它应该是多少合适呢? 答案是:64

问题，如果才能保证你写的css的尺寸只需要写一次，在不同的屏幕尺寸下面不用改?

---> 假如我们在750px下面，我们让html的font-size为75,则这个盒子的宽度是1rem,在640px下面我们让html的font-size为64,则这个盒子的宽度也是1rem，问题就这样解决了


### 实际开发中，用什么布局思路
我们打开m.jd.com,m.vip.com，会发现，实际上没有一个网站用了纯粹的百分比或者rem布局，经常会发现各种布局思路混在一起，因为没有一套布局思路能够通用保证不出问题

为什么rem不是万能的?
比如1px，如果我们在dpr是2的情况下就会变得很粗，我们知道那并不是真正的1像素

对比下面的代码:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,minimum-scale=1.0,maximum-scale=1.0"/>    
    <title>Document</title>
    <style>
    *{
        margin:0;
        padding:0;
    }
    </style>
</head>
<body>
    <div style="width:100%;height:1px;background:black;margin-top:100px;"></div>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,minimum-scale=0.5,maximum-scale=0.5"/>    
    <title>Document</title>
    <style>
    *{
        margin:0;
        padding:0;
    }
    </style>
</head>
<body>
    <div style="width:100%;height:1px;background:black;margin-top:200px;"></div>
</body>
</html>
```



## 推荐布局思路

使用由阿里出品的lib-flexible库

https://github.com/amfe/lib-flexible

![](https://box.kancloud.cn/23c118942e23cffd8e7c16090e4bfae5_600x423.png)

1. 视觉设计阶段，设计师按宽度750px（iPhone 6）做设计稿
2. 在chrome的模拟器里面，选择iphone6，应该就能看到html的font-size已经被设置为font-size: 75px了,进行切图(演示代码见https://github.com/zhengwei1949/mmb_template/tree/master/rem%E5%B8%83%E5%B1%80)
3. 切换到其他尺寸下面，检查并处理兼容性的问题
4. 用真实的手机进行验证

### 如何使用
1. 引入布局用的flexible.js(我已经写到了head标签里，大家直接拷贝过去用即可)，要注意的是不要再写meta:viewport标签了，因为flexible.js会自动帮你创建的
2. 引入base.css
3. 把设计师拿过来的设计稿拿过来，标注稿基准字体大小 = 标注稿宽度 / 10，如标注稿宽为750，标注稿基准字体大小为75；标注稿宽为640，标注稿基准字体大小为64；
4. 除了字体大小以外，其他所有的均按rem来，比如你的设计稿是750px的，那么，假如你量出来的是75px,则是1rem
字体除外，要根据不同的dpr设置不同的大小，比如如果是750的设计稿，那么字体假如是24px,则在dpr为1的情况下是16px,dpr2的情况下是24px,dpr3的情况下是32px(这块涉及到字体专业知识，总结一句话就是没有人会考虑用奇数字体，https://www.zhihu.com/question/20440679，所以不能让工具帮我们自动算，得写死)



### 在vue.js当中如何使用

1. 安装lib-flexible.js

```js
npm i lib-flexible --save
```

2. 在项目入口文件main.js当中引入lib-flexible.js

```js
import 'lib-flexible'
```

3. 其实到第2步就可以了，如果你还是比较懒，不想计算rem值，只要再修改一下cssloader的build/utils.js，即可全部写px

```js
// utils.js
var cssLoader = {
  loader: 'css-loader',
  options: {
    minimize: process.env.NODE_ENV === 'production',
    sourceMap: options.sourceMap
  }
}
var px2remLoader = {
  loader: 'px2rem-loader',
  options: {
    remUnit: 75
  }
}
// ...
```

并放入loaders数组中

```js
// utils.js
function generateLoaders(loader, loaderOptions) {
  var loaders = [cssLoader, px2remLoader]
  // ...
```


## 图片适配
srcset属性：以最合适的src去匹配不同屏幕
见代码

## 移动端常见问题汇总
- http://www.cnblogs.com/PeunZhang/p/3407453.html
- https://github.com/zhiqiang21/blog/blob/master/README.md
- https://github.com/sunmaobin/Mars/tree/master/issues
- http://www.cnblogs.com/PeunZhang/p/4517864.html
- http://www.cnblogs.com/PeunZhang/p/4903710.html
- http://www.cnblogs.com/PeunZhang/p/4633255.html
- http://www.cnblogs.com/PeunZhang/p/3835717.html
- http://www.cnblogs.com/PeunZhang/p/3592096.html
- 1px的问题 --> https://github.com/sunmaobin/Mars/blob/master/solutions/border-1px.md

## 推荐书
- 《移动web手册》

## todo
- 找二个典型的线上项目，自己写出来，做为参考(人性就是懒，路径依赖，哪怕以前用的东西再差，只要熟悉，也不愿意换过来，如果不把所有的东西准备好，这个文档是白写了)
- 结合vue写一个demo


## 字体图标的使用
https://zhuanlan.zhihu.com/p/27699518






