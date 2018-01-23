---

title:  前端W3C标准及规范
date:  #时间，一般不用改
categories:  
tags:  [前端W3C标准,W3C标准,前端规范] #标签，格式可以是[Hexo,总结]，中间用英文逗号分开
keywords:  [前端W3C标准,W3C] #文章关键词，多个关键词用英文逗号隔开

---
##  css代码规范
   1. 对于属性值或颜色参数，省略小于 1 的小数前面的 0 （例如，.5 代替 0.5；-.5px 代替-0.5px）;
   2. 十六进制值应该全部小写和尽量简写，例如，#fff 代替 #ffffff;
   3. 避免为 0 值指定单位，例如，用 margin: 0; 代替 margin: 0px;
   4. 与 <link> 相比，@import 要慢很多，不光增加额外的请求数，还会导致不可预料的问题;
   5. 通过 Sass 或 Less 类似的 CSS 预处理器将多个 CSS 文件编译为一个文件;
   6. 将公用的东西抽出来 写成组件，利于CSS代码的维护;
   7. 任何时候尽可能使用 classnames。标签选择器在使用上没有问题，但是其性能上稍弱，并且表意不明确;
   8. 慎重选择高消耗的样式，高消耗属性在绘制前需要浏览器进行大量计算;
	  +  box-shadows
	  *  border-radius
	  *  transparency 
	  *  transforms
	  *  CSS filters（性能杀手）
   9. Display 属性会影响页面的渲染，请合理使用;
	  *  display: inline后不应该再使用 width、height、margin、padding 以及 float；  
	  *  display: inline-block 后不应该再使用 float；  
	  *  display: block 后不应该再使用 vertical-align；  
	  *  display: table-* 后不应该再使用 margin 或者 float；			  
   10. CSS选择器从右到左匹配的机制后，只要当前选择符的左边还有其他选择符，样式系统就会继续向左移动，
	  直到找到和规则匹配的选择符，或者因为不匹配而退出
* * * *
##  html代码规范
   1. 属性顺序
	  *  HTML 属性应该按照特定的顺序出现以保证易读性（id,class,name,data-xxx,(src, for, type, href),
	   (title, alt),(aria-xxx, role)）。
	  *  属性的定义，统一使用双引号
	  *  HTML5 规范中 disabled、checked、selected 等属性不用设置值。
   2. 嵌套
	  *  a 不允许嵌套div这种约束属于语义嵌套约束，与之区别的约束还有严格嵌套约束比如a 不允许嵌套 a。
	  *  严格嵌套约束在所有的浏览器下都不被允许；而语义嵌套约束，浏览器大多会容错处理，
	     生成的文档树可能相互不太一样
	  *  inline-Level 元素，仅可以包含文本或其它 inline-Level 元素;
	  *  a里不可以嵌套交互式元素a、button、select等;
	  *  p里不可以嵌套块级元素div、h1~h6、p、ul/ol/li、dl/dt/dd、form等。

   * * * *
##  HEAD
   1. 为每个 HTML 页面的第一行添加标准模式（standard mode）的声明， 这样能够确保在每个浏览器中拥有一致的表现
	  *  html lang="zh-Hans"（中文）
	  *  html lang="zh-cmn-Hans"（简体中文）
	  *  html lang="zh-cmn-Hant"（繁体中文）
	  *  html lang="en"（English）
	  *  指定字符编码的 meta 必须是 head 的第一个直接子元素；
   2. SEO 
	  *  title   //页面名称
	  *  meta name="keywords" content="your keywords"  //页面关键词
	  *  meta name="description" content="your description"  //页面描述
	  *  meta name="author" content="author,email address"   // 页面作者
   3. 使用最新的浏览器
	  *  meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"
   4. favicon
	  *  在未指定 favicon 时，大多数浏览器会请求 Web Server 根目录下的 favicon.ico 。为了保favicon 可访问，避免404，必须遵循以下两种方法之一：1.在 Web Server 根目录放置 favicon.ico 文件；2.link rel="shortcut icon" href="path/to/favicon.ico"
   * * * *				
##  JS代码规范
   1. 变量, 使用 Camel 命名法。
   2. 私有属性、变量和方法以下划线 _ 开头。
   3. 类名，使用名词。
   4. 函数名，使用动宾短语。
   5. boolean 类型的变量使用 is 或 has 开头。
   6. Promise 对象用动宾短语的进行时表达。
   7. Promise 类型检测优先使用 typeof。对象类型检测使用 instanceof。null 或 undefined 的检测使用 == null。
   8. Promise 不要在 Array 上使用 for-in 循环。
   9. Promise 浏览器遍历 DOM 元素的代价是昂贵的。最简单优化 DOM 树查询的方案是，当一个元素出现多次时，将它保存在一个变量中，就避免多次查询 DOM 树了。
   10. Promise 循环无疑是和 JavaScript 性能非常相关的一部分。通过存储数组的长度，可以有效避免每次循环重新计算。（注: 虽然现代浏览器引擎会自动优化这个过程，但是不要忘记还有旧的浏览器。）
   11. 当你无法保证嵌入第三方内容比如 Youtube 视频或者一个 like/tweet 按钮可以正常工作的时候，你需要考虑用异步加载这些代码，避免阻塞整个页面加载。
* * * *
参考链接：<a>https://www.w3cschool.cn/webdevelopment/q3k8wozt.html</a>
