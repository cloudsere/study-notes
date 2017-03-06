## ```<meta name = 'viewport'>``` ...?

在响应式开发中经常见到的是：```<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">```

如果不加上这个标签，很容易出现这种情况：

![desk-vs-mobile](/Users/heqingqiu/Desktop/playmyself/study-notes/img/desk-vs-mobile.png)

什么viewport和device-width等等我都特别不懂，所以特别写一个读书笔记。。期望自己可以弄懂吧。

### device pixels vs CSS pixels

* device pixels是设备的物理像素，可以通过```screen.width/screen.height```获取
* CSS pixels是CSS样式表中写的 ‘px'，顺带一提，css一共有15个单位。。
  ![css-unit](/Users/heqingqiu/Desktop/playmyself/study-notes/img/css-unit.png)
* 在缩放比例为100%时，1个CSS pixel = 1个device pixel

### screen size

![screen size](http://www.quirksmode.org/mobile/pix/viewport/desktop_screen.jpg)

前面提到，可以用```screen.width```和```screen.height```来获取device-pixel，screen是不会变的：它是屏幕的特性，而不仅是浏览器的特性。

### window size

![window size](http://www.quirksmode.org/mobile/pix/viewport/desktop_inner.jpg)

- *意义：浏览器窗口的整体大小，包括滚动条。*
- *度量单位：CSS像素。*
- *浏览器错误：IE7不支持。Opera以设备像素进行度量。*

如果放大屏幕，```window.innerWidth/window.innerHeight```会缩小，用户能在浏览器窗口看到的内容也会减少

### Viewport

viewport是用来限定```<html>```元素的，为什么要限定呢？

> 比如一个块级元素宽度为10%，那么你也知道10%实际上是父级元素宽度的10%。但是你并没有设置父级元素的宽度啊，好吧，你也知道父级元素的宽度与其父级元素宽度一样（通过继承得来，假设这些元素都是块级元素）。然后向上到body元素的宽度，最终为html元素的宽度，其值可以通过 `document.documentElement.clientWidth` 获取

在css的单位中还有一种叫做```vh/vw```的，是把整个viewport划分为100 * 100的网格，比如50vw就是viewport的一半。

### ちょっとまっで！（等一下）

到这里我已经有点晕了，什么是```window```什么是```viewport```什么是```document```，虽然看了各种高度但还是很难懂。。。

* **Viewport:** 设备的屏幕

  * 用```window.innerWidth/Height```去获取，包括滚动条

  * `document.documentElement.clientWidth/Height`也可以获取，但是不包括滚动条。而且可以用element.clientHeight来获取其他元素的宽高

  * 到底为什么要有两对属性啊！摔！浏览器大战害死个人

    > The fact that we have two property pairs is a holdover from the Browser Wars. Back then Netscape only supported `window.innerWidth/Height` and IE only `document.documentElement.clientWidth` and `-Height`. Since then all other browsers started to support `clientWidth/Height`, but IE didn’t pick up `window.innerWidth/Height`.

* **Window:** 浏览器窗口，包括滚动条，可以和viewport一样大，或者比viewport小

  * 不仅有window.innerHeight，还有window.outerHeight哦...吐血
  * ![outer vs inner height](http://harttle.com/assets/img/blog/css/inner-outter-height.png)

* **Document:** 网页，可以比viewport大，甚至可以比window大

  * 可以用```document.docuemntElement.offsetHeight/Width```来获取
  * ![offsetHeight and offsetWidth](http://www.quirksmode.org/mobile/pix/viewport/desktop_offset.jpg)

有一些网站不是为移动设备架设的，所以这些网站的document比设备的viewport要大的多。

### scrolling offset

还有就是滚动条带来的问题。还记得那些年被```window.pageYOffset```，```document.documentElement.scrollTop```和```document.body.scrollTop```支配的恐惧吗。。。

关于滚动条，主要想知道的问题有两个：

1. 一共可以滚多长？
2. 现在滚了多长？

获取‘一共可以滚多长’的方法是：```element.scrollHeight```，其实```offsetHeight``` 也可以获取

回答‘滚了多长’，有很多度量的方法：

* window.scrollX == window.pageXOffset，pageXOffset的兼容性比scrollX好，但老版本的IE浏览器（<9）不支持这两个属性，所以比较保险的方法是：

  ```javascript
  var x = (window.pageXOffset !== undefined)? window.pageXOffset:(document.documentElement || document.body.parentNode || document.body).scrollLeft;

  var y = (window.pageYOffset !== undefined)? window.pageYOffset:(document.documentElement || document.body.parentNode || document.body).scrollTop;
  ```

[a-tale-of-two viewports](http://www.quirksmode.org/mobile/viewports.html)

[stackoverflow-viewport vs window vs document](http://stackoverflow.com/questions/33770549/viewport-vs-window-vs-document)

[移动设备的各种高度](http://tripleodeon.com/assets/2011/12/table.html)

