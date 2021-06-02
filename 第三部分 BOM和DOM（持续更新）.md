第三部分 BOM和DOM（持续更新）

[TOC]



## 第12章 BOM

1. 浏览器对象模型（BOM，Browser Object Model）,是以window对象为基础，这个对象代表了浏览器窗口和页面可见的区域。window对象在浏览器中有两重身份，一是ES中的Global对象，一是浏览器窗口的JavaScript接口；

2. 窗口关系：window对象、top对象（最上层窗口，浏览器窗口本身）、parent对象（当前窗口的父窗口）、self对象（始终指向window）；

   CSS像素是web开发中使用的统一像素单位；`window.devicePixelRatio`表示物理像素与逻辑像素之间的缩放系数；（DPI，dots per inch，单位像素密度）；outerWidth返回浏览器窗口自身的大小，包括工具栏滚动条；innerWidth返回浏览器窗口中页面视口的大小；`document.compatMode`检查页面是否处于标准模式；

3. `window.open()`方法可以用于导航指定URL，也可以用于打开新浏览器窗口，接收四个参数：要加载的URL，目标窗口，特性字符串（用于指定新窗口的配置）、表示新窗口在浏览器历史记录中是否替代当前加载页面的布尔值；

4. `setTimeout()`用于指定在一段时间后执行某些代码；`setInterval()`用于指定每隔一段时间执行某些代码；一般来说，不要用`setInterval()`；

   系统提示框：`alert()`、`confirm()`、`prompt()`

5. window的对象：

   - `location对象`:以编程方式操纵浏览器的导航系统；它既是window的属性，又是document的属性;

     - URLSearchParams构造函数提供了一组标准的API方法，通过它们可以检查和修改查询字符串。
     - `location.assign("")`修改location对象修改浏览器的地址；等同于`window.location=""、location.href=""`;

   - `navigator对象`：提供浏览器的信息；通常用于确定浏览器的类型；

     检测插件：window.navigator.plugins

   - `screen对象`：保存着客户端显示器的信息；（使用不多）

   - `history对象`：提供了操纵浏览器历史纪录的能力；（出于安全考虑，这个对象不会暴露用户访问过的URL，但可以通过它在不知道实际URL的情况下前进和后退）

     - go（num）//num为负表示后退几步，为正表示前进几步；

     - go（“#”）；可以用`back()`和`forward()`代替;

     - `history.pushState()`接受三个参数：一个state对象、一个新状态的标题、一个（可选的）相对URL；可以通过history.state获取当前的状态对象，也可以使用replaceState()并传入与pushState()同样的前两个参数来更新状态；

       区别：pushState()可以创建历史，可以配合popstate事件，而replaceState()则是替换掉当前的URL，不会产生历史，只会覆盖当前状态。

## 第13章 客户端检测

1. 能力检测：检测浏览器是否支持某种特性；尽量使用typeof操作符，

   注：!! 做类型判断，如`if(!!a)`

   ```js
   if(object.propertyInQuestion){
   //使用object.propertyInQuestion
   }
   ```

2. 用户代理检测：通过用户代理字符串确定浏览器,用户代理字符串包含在每个HTTP请求的头部，在JavaScript中可以通navigator.userAgent访问；

第十四章 DOM