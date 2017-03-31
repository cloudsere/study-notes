### DOCTYPE的作用

1. 文档类型声明 document type

2. 制定html页面使用的标准和版本

3. **浏览器根据doctype决定使用哪一种渲染方式**

   1. 怪异模式 Quirks Mode,为了兼容旧版本浏览器,盒模型是浏览器 Quirks Mode 和 Standards Mode 的主要区别。

      1. 早期的 IE 浏览器（IE 6 以前）将盒子的 padding 和 border 算到了盒子的尺寸中

   2. 准标准模式 Almost Standard Mode ,inline boxes that have no non-whitespace text as a child and have no border, padding, or margin

   3. 标准模式 Standard Mode

   4. ```html
      <!DOCTYPE html><!--使用标准模式-->
      ```

### 语义化的好处

1. 可访问性
2. 搜索引擎优化
3. 易读易维护

* 元数据元素
  * base:指定基准URL及链接打开方式
  * title
  * script
  * style:嵌入页面样式表
  * link:引入外部资源，比如外链样式表
  * noscript
  * meta:页面元数据

``` html
<!--阻止搜索引擎爬虫将网页编入索引-->
<meta name = 'robots' content = 'noindex' >

<!--格式检测，默认全部是开启的，可以通过meta来关掉，不会自动跳转拨号或者发邮件啦-->
<meta name = 'format-detection' content = 'telephone=no,address=no,email=no'>

<!--制定渲染的内核-->
<meta name = 'renderer' content = 'webkit'>

<!--每5秒刷新-->
<meta http-equiv = 'refresh' content = '5'>
<!-- 2秒以后跳转到首页，可以用来实现‘登陆成功，正在跳转到您之前访问页面’-->
<meta http-equiv = "refresh" content = "2;url='/'">
```

* 章节内容

  * body:页面所有展示内容都放在body内
  * article:文章
  * aside:侧边栏
  * nav:导航栏
  * section:内容块
  * header:页头
  * footer:页尾

* 文本语义

  * a

    * ```html
      <!--target的属性 _self（当前窗口） _blank(打开新窗口) _parent _top-->
      <a href = 'url' target = '_blank'>
      <!--href的属性 mailto: tel:-->
      <a href = 'mailto:name@example.com?subject=The%20subject%'>send email </a>
      ```

  * abbr:缩写 ```<abbr title = 'World Health Organization'>WHO</abbr>```

  * br

  * del/ins:删除／插入```<p>my favourite color is <del>blue</del><ins>red</ins>!</p>```

  * dfn:定义```<p><dfn>html</dfn>is the standard markup language for web pages</p>```

  * em:强调

  * strong

  * sub/sup

* 嵌入内容

  * img 

    * ```html
      <img src = '/path/img.jpg'  alt = '替代文字' width = '300' height = '200'>
                                                                          <figure>
             <img src = '/path/img.jpg' alt = '替代文字'>
             <caption>图片标题</caption>                                                                      <figure>
      ```

  * svg studio video canvas iframe

  * object:其他外部资源

