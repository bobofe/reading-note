# 本周书目——CSS揭秘

[TOC]



## 第一章

## 第二章 背景与边框

### 知识仓库

#### 盒子模型

![img](images/box-model.png) 

#### 背景属性

+ background-color
+ background-image
+ background-repeat
+ background-attachment
+ background-position
+ background-origin
+ background-clip
+ background-size

#### 颜色的表示方法

前景色：内容区+边框
背景色：背景部分

表示颜色的方法：

颜色由红(R)、绿(G)、蓝(B)组成，每个颜色的最低值为 0(十六进制为 00)，最高值为 255(十六进制为FF)

解释：0(00)为这个颜色的最浅值，225(fff)为这个颜色的最深值

+ rgb(red,green,blue)

  rgb的数值可以为0-255，也可以是百分数0-100%

+ rgba()

+ 16进制编码
  #开头，前两位表示三原色中的红色，中间两位表示绿色，最后两位表示蓝色。00表示没有颜色，ff表示颜色最强。

  #000000表示黑色，对应rgb(0,0,0)

  #ffffff表示白色，对应rgb(255,255,255)

  #ff0000表示纯红色，对应rgb(255,0,0)

  #00ff00表示纯绿色，对应rgb(0,255,0)

  #0000ff表示纯蓝色，对应rgb(0,0,255)

+ 表示颜色的词

+ hsl(色相，饱和度%，亮度%)

  色相：哪个颜色，取值：0-360

  ![image-20190327083015968](../../../../Users/lsb/Library/Application Support/typora-user-images/image-20190327083015968.png)

  饱和度：颜色的纯度（颜色深浅程度）

  亮度：颜色的明暗程度，亮度值越高，色彩越白，亮度越低，色彩越黑。

  例子：

  ```css
  div{
   border:10px solid hsla(0,0%, 100%, 0.5);
   }
  ```

+ hsla()

#### shim和polyfill

在 javascript 的世界里，我们经常会遇到`shim`和`polyfill`两个术语，那么它们之间到底有什么区别呢？

##### Shim

Shim 通常是一个代码库，它给旧环境（并不一定特指浏览器环境）带来的往往是全新的 api，而且这些 api 只能在这个环境当中运行。这个库中的方法接收的参数与调用方法与标准的方法一样，但是shim中的方法是自己实现逻辑处理的，因此在方法中加入了兼容性处理。所以方法的返回结果与标准方法相同。

##### Polyfill

在 2010年10月，Remy Sharp在他的博客中对 [polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill/) 做了如下定义：

> Polyfill 就是一系列的代码或者插件，它为开发者提供的技术特性，都是希望浏览器本就应该原生支持的，并且抹平了 api 之间的使用差异。

polyfill指的是符合shim标准的API。polyfill API使用老方法来实现新功能，从而保证在低级浏览器中也能使用比较新的方法。

因此，一个 polyfill 就是一个浏览器层面的 shim。典型地像检测浏览器是否支持某一个 api，如果不支持就加载一个 polyfill，这样就可以让开发者在任何情况下无缝的使用那些 api 了。Polyfill 这个术语其实来自于一款家居装修产品：

> Polyfilla 是英国生产的一种用来抹泥修墙的膏状物，它因能够很好地修复墙壁上的裂纹而被人们所熟知。所以，试想浏览器就相当于一堵有裂纹的墙，这些 polyfill 能够抹平墙壁上的裂纹，也就是浏览器之间的 api 差异，使开发者能够正常的在浏览器上使用这些技术特性。

可以理解为：“polyfill(n):一种JavaScript“衬垫”，用于在旧浏览器中提供标准API。”

因此，websocket polyfill会创建一个window.WebSocket对象，提供与原生实现相同的属性和方法。这意味着你可以使用真正API面向未来开发啦！只要在不支持该API的浏览器中加载兼容性polyfill即可。

举几个非常著名的例子：

一个是爱尔兰的 Paul 发布的 [html5 跨浏览器 polyfills](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-browser-Polyfills)，里面收集了所有能够给浏览器植入 html5 功能的 polyfills 和 shims。

另一个是 [es5-shim](https://github.com/es-shims/es5-shim)，它在 ES3 引擎的基础上对 ES5 的很多特性进行了改进，因为纯粹是语言相关的，所以很多在 nodejs 上才能使用的特性在浏览器端同样能够运行。

实例1：

```
es5-shim.js/es5-shim-min.js:
```

作用：可以让一些低级的浏览器支持ES5中的一些特性。
注意： 由于es5-shim.js使用的是EMCScript的原生方法来实现的，因此必须放在所有外部导入js文件的最上面。

实例2：

```
es6-shim.js/es6-shim-min.js
```

作用：可以让一些低级的浏览器支持ES6中的一些特性。

实例3：

```
require('es6-promise').polyfill();
//require(‘es6-promise/auto’);
```

作用：这个polyfill()方法能够在全局范围内处理promise方法。每当promise方法被调用，polyfill()方法就会自动修改为在低版本浏览器中也能处理的语法。

实例4：一个处理兼容性的例子:

```
html5shiv/html5shim:
```

由谷歌提供的html5.js能够让IE9以下的浏览器也能够正确处理html5中新增的几个标签。正确的调用方法如下：

```html
<!--[if lt IE 9]
    <script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
<![endif]-->
```

注意：
1.这里的注释是不能删除的。这个条件注释用于检查当前浏览器版本是否低于IE9，只有当前浏览器版本低于IE9时，这个js文件才会被引入。
2.这个条件注释必须放在head标签能。因为IE浏览器必须在元素解析前知道这个元素。如果放在其他位置则会导致失效！
除此之外还需要在CSS样式表中添加一条样式：

```
header,section,footer,aside,nav,article,figure {
    display: block;
}
```


备注： 这条样式是为了让低版本的浏览器能够将html5中新增的标签当作块级元素来处理。否则低版本会将这些元素当作行级元素进行处理。

转载文章：

https://github.com/chenxiaochun/blog/issues/37

https://blog.csdn.net/sxLDWX/article/details/78963086

#### 回退机制

在浏览器特性参差不齐的大环境下，“渐近增强” 与 “平稳退化” 是一种务实的策略。因此，在编写华丽样式的同时，我们还需要想好退路，为功能较弱的浏览器提供回退样式（fallback）。总的来说，我们应该利用 CSS 自身的机制来组织回退样式，而不是依赖 CSS hack 来实现。

**渐进增强**     VS   **优雅降级（平稳退化）**

**渐进增强（向上兼容）**：一开始就针对低版本浏览器进行构建页面，完成基本的功能，然后再针对高级浏览器进行效果、交互、追加功能达到更好的体验。

**优雅降级（向下兼容）**：一开始就构建站点的完整功能，然后针对浏览器测试和修复。比如一开始使用 CSS3 的特性构建了一个应用，然后逐步针对各大浏览器进行 hack 使其可以在低版本浏览器上正常浏览。

对比：

```css
.transition { /*渐进增强写法*/
  -webkit-transition: all .5s;
     -moz-transition: all .5s;
       -o-transition: all .5s;
          transition: all .5s;
}
.transition { /*优雅降级写法*/
          transition: all .5s;
       -o-transition: all .5s;
     -moz-transition: all .5s;
  -webkit-transition: all .5s;
}
```

回退写法：

举个例子，设计师要求某个元素的背景色显示为半透明的黑色（如上图所示）。但我们都知道，低版本 IE 等浏览器并不支持 RGBA 颜色，因此对于这些浏览器，我们需要将它的背景色设置为最接近设计意图的纯黑色。那么在这里，半透明黑色是我们期望的 “理想样式”，而纯黑色则是用来兜底的 “回退样式”。

在搞清楚状况之后，我们很快写出了下面的代码：

```css
div{
background: rgba(0,0,0,0.75);
background: #000\9;
}
```

这段代码的意图是这样的：第一条声明是我们理想的样式，写给标准浏览器；第二条声明是专门写给 IE 的 CSS hack，因为只有 IE 浏览器才能识别这一行，所以在 IE 下这个元素的背景色就是黑色的了。

听起来似乎很有道理，现实中也有很多代码就是这样写的，但它存在一些明显的缺陷：

- 首先，第二行代码命中的是 “IE 浏览器”，但实际上我们应该命中那些 “不支持 RGBA 的浏览器”。虽然从现状上来说，这两个集合的重合度相当高，但代码的作用和我们的实际意图不符，这是一个不小的问题。
- 此外，这种回退样式的写法在 IE6、7、8 当道的年代还算说得通，但当 IE9+ 出现之后就站不住脚了。因为 IE9+ 一方面是支持 RGBA 的，另一方面又可以识别第二条声明，最终导致 IE9+ 也把元素显示为纯黑背景（但它本可以显示出我们理想的效果）。在这里我们也可以看出 CSS Hack 的脆弱之处——没有人能对它的未来兼容性提供担保。

我们不妨换个思路，其实 CSS 有一项非常重要的 “向前兼容” 机制——当浏览器遇到无法识别的某行声明时，并不会报错或中止解析，只是默默地忽略它而已。（实际上 CSS Hack 之所以会起作用，也是利用了这个机制。）

因此，**正确的代码组织方式应该是先写 “回退样式”，再写 “理想样式”：**

```css
div{
background: #000;
background: rgba(0,0,0,0.75);
}
```

这种写法更像是具备了 “特性检测” 的功效：不支持 RGBA 的浏览器不识别第二条声明，因此只有第一条会生效；而对于支持 RGBA 的浏览器来说，它们可以同时识别这两条声明，但由于第二条声明的权重更高，这些浏览器最终将显示出半透明的效果。

总结：（1）通过样式的层叠提供完善的回退样式——浏览器前缀

​           （2）CSS向前兼容机制：先写回退样式，再写理想样式

转自：http://www.10tiao.com/html/482/201604/2651552670/1.html

​	   https://www.jianshu.com/p/d313f1108862

#### IE滤镜

待补充....

### 1.半透明边框

使用半透明颜色可能面临的问题：

+ 需要做好回退
+ 加载shim脚本
+ 在IE下用滤镜来hacknannan

题目：给容器设置一个白色背景和一个半透明的边框，父元素的背景色会从半透明的边框透过

效果图：
![img](images/半透明边框效果图.png)

问题：透明边框不显示

关键点：背景和边框的关系

> 默认情况下，背景色会颜色到边框所在的区域

解决：**background-clip属性**

`background-clip`  设置元素的背景（背景图片或颜色）是否延伸到边框下面。取值：

```css
div{
	background-clip: border-box;
	background-clip: padding-box;
	background-clip: content-box;
}
```

### 2.多重边框



## 第三章

## 第四章

## 第五章

## 第六章

## 第七章

## 第八章

