## 先上结论
1. 学习css学习成本与投入不成正比，不建议花太多时间研究
2. 准备面试的时候刷题即可
3. 尽量找一些大公司的官网，把自己公司的需求和他们的需求进行对比，把代码抄过去(大部分的css都可以抄，js由于压缩过可能要费一些时间)，会ctrl c + ctrl v就行了
4. 如果去上班的时候，先看看公司其他同事写好的页面是怎么写的，把大体的思路研究明白一下，用他们的思路即可
5. 如果比较懒不想研究，或者没有现成的思路，就用一种自己最熟悉的即可
6. 公司不养闲人，没有人愿意让你用原生的代码写一堆容易出bug的东西出来
7. 学习阶段老师或者自己封装的rem,swiper.js等各种框架、库等只是一个演示demo,bug太多，建议玩玩就可以了，千万不要在以后上班的时候用，以后上班还是用网上别人推荐的比较靠谱的解决方案和库等(比如swiper.js,fullpage.js等)
8. 个人不推荐类似这样的代码写真实的项目(http://www.cnblogs.com/lixinglong/p/7889526.html),因为只考虑了rem,但是比较正规靠谱的rem解决方案是要配合dpr来进行切图的(大家可以参考天猫、淘宝移动端官网)
9. 1rem等于多少?得先看你用的是哪种思路，这块没有标准答案，天猫在iphone6下面的dpr是2,font-size是75px,淘宝在iphone6下面的dpr是2,font-size是37.5px,m.qq.com腾讯官网在iphone6下面的font-size是400px(这块应该有一个尔康鼻孔的表情，找不到算了用文字替代)

### 为什么css这么难学
+ css这套技术系统本身十分的混乱，基本上可以说毫无规律可言，依赖于技术人员的熟练程度而不是逻辑更多一些
+ css历经了多个时代的升级，每一次升级之后，新的技术标准和旧的基本上没有任何关联
    + table布局
    + div+css布局
    + flex布局
    + grid布局
+ 手机终端市场的混乱
    + 各种尺寸的手机
    + 由iphone的retina技术带来的dpr的混乱
+ https://www.zhihu.com/question/66167982/answer/239709754

## 响应式布局
- 如果有一个页面，需要能在pc上正常适配，也能在移动端上适配，我们可以称之为响应式
- 代表：
    + http://expo.bootcss.com/
    + https://www.microsoft.com/zh-cn

### 原理：
媒体查询 media-query

### 为什么响应式并不值得去推崇
+ 响应式是当时Pc端占主流市场下的一种妥协的技术,响应式的思路是先在pc端做好之后，再考虑在移动端通过媒体查询让某些标签隐藏或者改变样式，是一种以pc为主要考虑的思维方式，用一种方案来解决两个问题，注定了性能会十分的低下，现在是移动端的时代，大部分的新创公司对pc端基本上不太重视
+ 刚成立的公司，快速制作一个官网，等以后有钱了，肯定还是会pc端一套，移动端一套，分开写
+ 用"廉价"的bootstrap搭建而成，一个只会php,java的技术人员只要理解了栅格式的原理，照着文档就像搭建积木一样就能写出来一个页面
+ 拉勾网上并没有多少招聘信息刻意强调会bootstrap,会响应式
+ 响应式在国内基本上没有推广开
+ 一般需要给客户看的网站，不大可能用响应式，因为响应式的页面不能做一些很复杂的效果(为什么淘宝官网不用响应式)
+ 只有公司内部项目考虑用bootstrap的可能性大一些

### 响应式布局适用的场景
- 后台管理系统
- 新项目对页面没啥要求，要求快速搞出来一个宣传性页面

### 问题
- 会不会存在一种需求需要移动端布局和响应式布局同时应用?
    + 只可能前台用纯移动端，后台用响应式
    + 也就是用bootstrap用来写纯移动端页面是一种很low的行为
    
# 移动端布局

## 百分比布局(这块大家很熟悉了，有兴趣可以了解一下)
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


## rem布局思路

由于rem布局涉及到的概念很多，为了搞明白，我们先把下面的几个概念理解一下(这块不理解也没关系，大家不行就只要知道会用即可)

### 常识
1. iphone6的分辨率 750*1334px
2. iphone5,iphone5c,iphone5s 640*1136px
3. iphone4,iphone4s 640*960
4. iphone 320 * 480px

### 思考
iphone 6 plus是1242*2208px的分辨率，多少同学的大笔记本电脑有这么高的分辨率??

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
3. 有的手机的分辨率比你的笔记本要高是很正常的事情，不要觉得惊讶

## css像素
- 在没有缩放的情况下pc端1px css像素相当于1物理设备像素
- 试验：缩放网页，观察你写的1px会变大变小
    + 如果放大一倍，则你写的1px*1px变成了2px*2px相当于原来只需要一个手电筒，现在需要4个手电筒了

### 思考问题
1. 为什么在iphone6上打开http://search.jumei.com/是缩小的网页?为什么能够在小屏幕上看到整个页面?
2. 我们把网页切换到响应式模式，宽度切换到640px,发现横向滚动条，表现形式是和在iphone6上看到的并不一样

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

为什么会这样?
这里涉及到一个概念叫viewport

https://www.quirksmode.org/mobile/viewports2.html

简单的理解，移动端时代到来之前的pc时代，只有一个viewport视口，和电脑的分辨率是一致的，但是在移动端时代，手机的浏览器的布局视口viewport和显示屏幕的分辨率脱离关系(比屏幕的分辨率大得多)

#### 在手机上有两个视口
- layout viewport布局视口(虚拟的)，一般是980px
- visual viewport视觉视口(iphone6是750*1334)

#### 对viewport的理解
- http://www.css88.com/archives/5975

上面说这么多，我们现在可以得出的结论是：
1、 我们如果还是按之前的pc端布局思路，把内容区域设置成980px以上，比如1080之类的,在手机上肯定会有滚动条的(这里指的是写死宽度，而不是采用自适应那种)
2. 假如这个世界上只有iphone5,其他手机厂商全倒闭了，苹果只准备卖iphone5,如果我们只考虑布局iphone5(640*960),我们只需要设计一个640*960宽高的设计稿即可

貌似这个思路是对的，咱们试一下，写一个如下的页面，然后在里面写一个640*100的盒子

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
    <div style="width:640px;height:100px;background:red;"></div>
</body>
</html>
```

然后咱们用iphone5测试一下，what a fuck,我们会发现居然出现了横向滚动条???

这时候又引出了我们的最后一个概念 - dpr

我们前面说过了：
1、 css的px单位是一个相对单位，和实际的物理设备像素并不一定是1:1的关系

在手机上1个css像素占多少物理设备像素呢?

在iphone 5下面,1px相当于2个物理像素，也就是我们前面说过的1*1其实会占有4个手电筒，也就是1px*1px实际上会被拉伸铺到一个4*4的盒子上

在iphone 5中，物理设备宽度是320(这个单位叫dpi)(参考http://upload-images.jianshu.io/upload_images/1806083-b0170628417e0f28.png)

应该是320(这是默认的可视区的css宽度) * 2 = 640px

这里的2，我们一般叫它dpr,在chrome的移动端视图是可以看得到的。

到这里，咱们先不往下看了，大家思考一下，如果让你来做，你会怎么办?
1. 如果我们只要的是320px宽度的设计稿，肯定是不行的，因为1px拉伸之后整个页面会模糊
2. 我们最常想到的是让设计师出640宽度的设计稿，这样我们切图的时候把宽度同意除以2即可，这样切出来的图片虽然是2倍大，但可以直接用这样都是比较清晰的

但是，这样做，有一个问题，我们现实生活中手机的尺寸太多了，有750的，也有1080的，我们不可能让设计师一下子给我们出4、5套设计稿，然后，我们每一种手机切一种图，这样太浪费时间了

那怎么办?

我们这时候可以来做一道数学题：

40*40的东西在640宽度的手机里面，如果现在手机变成了750宽度，我们这个100*100的东西要变为多大才不会变形?

40 * (750 / 640) = 46.875px

接着，咱们再来想，我们能不能写一个尺寸，在640px里面代表的是40px,在750px里面代表的是46.875px呢?

这时候，我们可以想到，在写页面的时候，其实有一个单位是相对单位叫rem,

比如说：我们就规定,640px下面的html的font-size是20px,那么，750下面是多少呢?

于是，有了下面的一段代码

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
    <div style="width:2.5rem;height:2.5rem;background:red;margin:0 auto;">
        
    </div>
</body>
</html>
```
思路：
1、 320宽度占全屏幕 --> 640的要除以2 --> font-size是20px --> 量出来的尺寸只要除以40就是实际的rem宽度了
2、好多同学总纠结于各种编辑器里面的px转rem的插件，其实没必要转，因为less里面直接写100/40rem即可，让less帮我们算也行的

上面的方案貌似已经完美了，这也是我知道的大家以前一直在用的上课的时候学的方案，但是这个方案其实存在一些问题的：
1、1px的问题
2、字体如果用rem其实是存在问题的(参考https://www.zhihu.com/question/44243091/answer/114441200)

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

所以，我们上面的js代码虽然可以让我们用rem布局，但是还不够完美，我们其实要搭配着dpr等其他的东西来布局才比较完美

### 实际开发中，用什么布局思路
我们打开m.jd.com,m.vip.com，会发现，实际上没有一个网站用了纯粹的百分比或者rem布局，经常会发现各种布局思路混在一起，因为没有一套布局思路能够通用保证不出问题

这里我给大家推荐几个认为比较靠谱的，经过了时间检验的rem方案

## 推荐布局思路1

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

## 推荐布局思路2
- https://www.cnblogs.com/zzsdream/p/7065015.html
- https://codepen.io/minooo/pen/WoQjKW?editors=1100
- https://minooo.github.io/Demo/react-study-step-03-demo/index.html#/

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

## iconfont字体图标的使用注意事项
https://zhuanlan.zhihu.com/p/27699518

## 推荐布局工具
- http://koala-app.com/index-zh.html
    + 推荐理由：理论上来说命令行gulp,webpack是最ok的，但是很多同学对npm环境不熟悉,编辑器的less,sass编译环境一旦出问题就搞不定了，用此工具完全不用配置任何环境，安装好即可使用
- 移动端调试工具:vConsole
    + 推荐理由：手机上不能按f12打开控制台，我们又不希望随时随地的进行alert，调试太痛苦
- browserSync
    + 推荐理由：每次改代码都要刷新浏览器，太麻烦了
    + cnpm install -g browser-sync
    + browser-sync start --files "*.*" --server (一定要是双引号)
    + 如果出错了，基本上是因为html页面最基本的结构没有写导致的
- 电脑上如何调试手机上的页面
- http://blog.csdn.net/byc233518/article/details/52437498
- fiddler(太过于复杂，貌似查看微信端别人代码只能通过这个来拿，有时间可以研究，貌似上面那种玩法如果ok的话不用玩这个了，确实不友好)









