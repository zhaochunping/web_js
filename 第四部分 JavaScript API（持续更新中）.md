第四部分 JavaScript API（持续更新中）

[TOC]



### 第20章 JavaScript API

#### 1、Atomics

- `SharedArrayBuffer()`和`ArrayBuffer()`

-  `Atomics API` 解决了以下的问题:

1. 所有原子执行互相之间不会重排。
2. 使用原子读或者原子写保证所有指令都不会相对原子读/写重新排序。

可以使用 `load` 和 `store` 构建代码围栏，即进行本地重排，即可以保证非原子操作可以在原子操作之前或者之后完成；`Atomics.load()` 和`Atomics.store()`代码围栏

- `exchange()`和`compareExchange()`：后者只有在缓冲区未被修改的情况下才能向缓冲区写入新值。

- `Futex` 操作只能用于 `Int32Array` 视图，并且只能运用在工作线程内部。

调用 `wait` 方法会停止执行，在指定时间或者相应索引上调用 `notify` 之后，才会继续执行。

#### 2、postMessage()

跨文档消息（cross-document messaging， XDM）：是一种在不同执行上下文间传递信息的能力；

同源策略：

3、批量解码是通过TextDecoder()的实例完成的；

4、Atomics API用于保护代码在多线程内存访问模式息,同时保证安全和遵循同源第策略API支持从不同源跨文档发送消postMessage()逢转换（越来越常见的操作)。 Encoding API 用于实现字符串与缓冲区之间的无绒的可靠工具。File API提供了发送、接收和读取大型二进制对象于操作音频和视频。开个是每母个浏览器都会支

5、Blob：size、type属性；slice()方法；

6、流

- 可读流
- 可写流
- 转换流

7、使用`DocumentFragment`可以一次性添加所有子节点，最多只会有一次布局重排，此时不适合用`document.appendChild()`；

```
const fragment=new DocumentFragment();//p649
foo.appendChild(fragment);
console.log(fragment.children.length);//0

```

8、影子DOM是通过attachShadow()方法创建并添加给有效HTML元素的；



### 第21章 错误处理与调试

为保证跨浏览器兼容，最好只依赖message属性；

1、只要代码中包含了finally子句，try块或catch块中的return语句就会被忽略，即try/catch语句中可选的finally子句始终运行；

2、组织浏览器对JavaScript错误作出反应的方法：

- 使用`try/catch`语句，可以通过更合适的方式对错误做出处理；

- 定义`window.onerror`事件处理程序；（任何没有被`try/catch`语句处理的错误都会在window对象上触发error事件）

  ```JS
  window.onerror=(message,url,line)=>{//错误信息，发生错误的URL,行号
      return false;//阻止浏览器默认报告错误的行为
  }
  ```

3、**静态代码分析器**或代码检查器（linter）

4、JavaScript经常出现的错误：

- 类型转换；
- 数据类型检测不足；
- 向服务器发送错误数据或从服务器接收到错误数据；

#### 5、错误类型

- error（基类型，很少出现，主要用于开发者抛出自定义错误）
- InternalError（会在底层JavaScript引擎抛出异常时由浏览器抛出）
- EvalError（会在使用eval（）函数发生异常时抛出）
- RangeError（数值越界时抛出）
- ReferenceError（找不到对象时发生）
- SyntaxError（在给eval（）传入的字符串包含JavaScript语法错误时发生）
- TypeError(常见，主要发生在变量不是预期类型，或者访问不存在的方法时)
- URIError（只会在使用encodeURI（）或decodeURI（）但传入了格式错误的URI时发生）

#### 6、非重大错误和重大错误

- 非重大错误
  - 不会影响用户的主要任务
  - 只会影响页面中某个部分
  - 可以恢复
  - 重复操作可能成功

- 重大错误：
  - 应用程序绝对无法继续运行
  - 错误严重影响了用户的主要目标
  - 会导致其他错误

7、web应用程序开发中的一个常见做法就是建立中心化的错误日志存储和跟踪系统，要建立JavaScript错误日志系统，首先需要在服务器上有页面或入口可以处理错误数据。

### 第22章 处理XML

#### 1、XML

- DOMParser：把XML解析为DOM文档；

- XMLSerializer：把DOM文档序列化为XML字符串；

#### 2、XPath和XSLT

XPath是为了在DOM文档中定位特定节点而创建的；（DOM Level3新增）

XSLT( Extensible Stylesheet Language Transformations)可扩展样式表语言转换：没有与之相关正式的API；

### 第23章 JSON

1、JSON是一种轻量级数据格式，可以方便地表示复杂的数据结构。其与XML功能类似，但是更简洁，而且所有浏览器都已经原生支持全局JSON对象；

2、JSON语法支持3种类型的值：

- 简单值：字符串、数值、布尔值、null（undefined不可以）；

  - JSON字符串必须是双引号，没有变量声明，最后没有分号，同一个对象中不允许出现两个相同的属性。
- 对象：表示有序键/值对

  1. 与JavaScript对象字面量相比，JSON有两处不同：没有变量声明、没有最后的分号；同一个对象不允许有两个相同的属性；
  2. `JSON.stringify()`：用于**将JavaScript对象序列化为JSON对象；**
    - 默认情况下，该方法会输出不包含空格祸所进的JSON字符串，值为undefined的任何属性也会被跳过；在序列化 JSON 对象时，所有函数和原型成员都会被忽略。
    - 参数：序列化的对象、过滤器（数组或函数）、用于缩进结果JSON字符串的选项（数值）；
    - 有时候需要在`JSON.stringify()`上自定义JSON序列化；
    - 在把对象传给JSON.stringify()时会执行如下步骤：
      1. 如果可以获得实际值，则调用toJSON()方法获取实际的值，否则使用默认的序列化；
      2. 如果提供了第二个参数，则应用过滤。传入过滤函数的值就是第1步返回的值；
      3. 如果第2步返回的每个值都会相应地进行序列化；
      4. 如果提供了第3个参数，则相应地进行缩进；
  3. `JSON.parse()`：**将JSON数组解析为JavaScript对象；**
    - 将JavaScript对象转为JSON对象，再将其转为JavaScript对象，这两个对象是两个完全不同的对象，但是它们拥有相同的的属性和值。
- 数组
  - 数组可以通过数值索引访问的值的有序链表；
  - 数组和对象可以组合使用，表示更加复杂的数据结构；

3、把对象成给`JSON.stringify()`时会执行如下步骤：

1. 如果可以获取实际的值，调用`toJSON()`方法获取实际的值，否则使用默认的序列化；
2. 如果提供了第二个参数，则应用过滤，传入过滤函数的值就是第1步返回的值；
3. 第2步返回的每个值都会相应的进行序列化；
4. 如果提供了第三个参数，则相应的进行缩进；

### 第24章 网络请求与远程资源

可扩展标记语言（Extensible Markup Language，XML）： 被设计用来传输和存储数据。

超文本标记语言（HyperText Markup Language，HTML）

（XMLHttpRequest，XHR）

#### 1、Ajax：

无需刷新当前页面即可从服务器获取数据的一个方法通信。

#### 2、XHR（XMLHttpRequest）

2.1 XHR（XMLHttpRequest）的一个主要限制是同源策略，即只能在相同域名，相同端口和相同协议的前提下完成。

```js
let xhr=new XMLHttpRequest();//通过构造函数XMLHttpRequest创建XHR对象
//open()的使用方法：三个参数（请求类型、请求URL、表示请求是否异步的布尔值）
xhr.open("get","example.php",false);
```

XHR对象有一个readyState属性，表示当前处在请求/响应过程的哪个阶段：

- 0：未初始化，未调用open()
- 1：已打开，未调用send()
- 2：已发送，已调用send()，尚未收到响应
- 3：接收中，
- 4：完成

2.2 进度事件

- 1、loadstart
- 2、progress
- 3、error
- 3、abort
- 3、load
- 4、loadend

2.3跨源资源共享（ Cross-Origin Resource Sharing，CORS）

定义了浏览器与服务器如何实现跨源通信；

#### 3、JSONP

JSONP(JSON with Padding) 是JSON 的一种"使用模式"，可以让网页从别的域名（网站）那获取资料，即跨域读取数据。JSONP格式包含两个部分：回调和数据。**回调**是在页面接收到响应之后应该调用的函数，通常回调函数的名称是通过请求来动态指定的。数据就是作为参数传给回调函数的JSON数据。

缺点：

- JSONP是从不同的域拉取可执行代码，如果这个域不可信，则可能在响应中加入恶意内容，此时需要完全删除JSONP。
- 不好确定JSONP请求是否失败（开发者常使用计时器来决定是否放弃等待响应）。

#### 4、Fetch API 

- **Fetch API 是作为对XHR对象的一种端到端的替代方案而提出来的，**
- 这个API提供了优秀的基于期约的结构、更直观的接口，以及对Stream API更好的支持；
- **（必须是异步的）**；
- Fetch API本身是使用JavaScript请求资源的优秀工具，同时这个API也能够应用在服务线程（service worker）中，提供拦截、重定向、修改通过fetch（）生成的请求接口；
- 能够执行XMLHttpRequest对象的所有任务。

##### 4.1fetch()方法

##### 4.2常见的Fetch请求模式

- 发送JSON数据
- 在请求体中发送参数
- 发送文件：FormData
- 加载Blob文件：blob()方法
- 发送跨源请求
- 中断请求

##### 4.3Headers对象

Headers对象是所有外发请求和入站响应头部的容器；每个外发的Request实例都包含一个空的Headers实例，可以通过Request.prototype.headers访问，每个入站Response实例也可以通过Response.prototype.headers访问包含着响应头部的Headers对象。

实例方法：get()、set()、has()、delete()、entries()

与Map的不同之处：初始化Headers对象时，可以使用键/值对形式的对象，则Map不可以；一个HTTP头部字段可以有多个值，而Headers对象通过append()方法支持添加多个值。

##### 4.4Request对象

Request对象是获取资源请求的接口；有请求体的Request只能在一次fetch中使用；

- 克隆方式：
  - 使用Request构造函数（不总能一模一样）
  - clone（）方法（一模一样）

##### 4.5Response对象

Response对象是获取资源响应的接口；

5、Web Socket是与服务器的全双工、双向通信渠道，其不使用HTTP，而是使用了自定义协议，目的是更快地发送小数据块。

自定义协议：（ws://  wss://）

### 第25章客户端存储

#### 1、cookie 、子cookie

1.1 cookie存储在客户端机器上，cookie由以下参数构成：

- 名称：不区分大小写
- 值：存储在cookie里的字符值，这个值必须经过URL编码
- 域：cookie有效的域
- 路径：请求URL中包含这个路径才会把cookie发送到服务器
- 过期时间：表示何时删除cookie的时间戳
- 安全标志：设置之后，只在使用SSL安全连接的情况下才会把cookie发送到服务器（cookie中唯一的非名/值对）

1.2JavaScript中的cookie，只有BOM的document.cookie属性；要使用decodeURIComponent()对名称和值进行解码；

1.3为绕过浏览器对每个与cookie数的限制，有些开发者提出了子cookie的概念，子cookie是在单个cookie存储的小块数据，本质上是使用cookie的值在单个cookie中存储多个名/值对。

##### 1.4**解析和序列化使用场景**

- 向后台传递参数，接收后台返回的string；
- 页面间传递数据，数组需要使用序列化，否则IE会报错；
- 进行本地存储时，存储在本地`window.localStorage.setItem(key,value)`存储的value是json序列化的字符串；获取得到的`window.localSorage.getItem(key)`也是json序列化的字符串，需要经过json的反序列化进行使用；

#### 2、Web Storage

Web Storage定义了两个对象用于存储数据：

- **sessionStorage**：前者用于严格保存浏览器一次会话期间的数据，因为数据会在浏览器关闭时被删除。在运行本地文件时不能使用，存储在sessionStorage对象中的数据只能由最初存储数据的页面使用，在多页应用程序中的用处受限。

- **localStorage**：后者用于会话之外持久保持数据。

#### 3、IndexedDB

IndexedDB是类似于SQL数据库的结构化数据存储机制。不同的是，IndexedDB存储的是对象，而不是数据表。绝大多数IndexedDB操作要求添加onerror和onsuccess事件处理程序来确定输出。**异步**

- 调用indexedDB.open()，并给它传入一个要打开的数据库名称；

- 使用存储对象

- 创建了对象存储之后，剩下的所有操作是通过**事务**完成的。

  ```js
  //事务：要通过调用数据库对象的`transaction()`方法创建
  let transaction=db.transaction()；
  ```

- 插入对象：add()、put()

- 游标查询：在对象存储上调用OpenCursor()方法创建游标；



### 第26章模块

1、异步模块定义（Asynchronous Module）

通用模块定义（Universal Module Definition， UDM）：

2、ES6最大的一个引进：引入了模块规范；

```js
<script type="module">
//模块代码
</script>
```

特点：

- ES6 的模块自动开启严格模式

- 每个模块都有自己的上下文，每一个模块内声明的变量都是局部变量，不会污染全局作用域。

- 每一个模块只加载一次（是单例的）， 若再去加载同目录下同文件，直接从内存中读取。

- import 是静态执行，所以不能使用表达式和变量。

  

3、依赖模块

4、

### 第27章 工作者线程