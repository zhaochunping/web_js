[TOC]



# 第一部分：JavaScript基础知识

查缺补漏

## 第一章 什么是JavaScript

#### 1.1、完整的 JavaScript 实现的部分组成：

- 核心（ECMAScript） ；
- 文档对象模型（DOM，Document Object Model）：提供访问和操作网页内容的方法和接口，用于在HTML(HyperText Markup Language, 超文本标记语言)中使用扩展的XML(可扩展标记语言) ；
- 浏览器对象模型（BOM，Browser Object Model）：提供与浏览器交互的方法和接口；

（注：（1）JavaScript编程语⾔， Html和Css是标记语⾔。ECMAScript(ES)是JavaScript的标准，JavaScript是ECMAScript的实现；（2）DOM 4新增的内容包括替代Mutation Events的Mutation Observers，鉴于前者浏览器兼容问题和同步执行监听DOM树结构变化的性能问题。故提出Mutation Observers，当使用observer监听多个DOM变化时，并且这若干个DOM发生了变化，那么observer会将变化记录到变化数组中，等待一起都结束了，然后一次性的从变化数组中执行其对应的回调函数）

#### 1.2、for of 和for in和 forEach（）

```js
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
for (const digit of digits) { console.log(digit);}
for (const index in digits) {console.log(digits[index]);}
```

- for...of 循环将只循环访问对象中的值，不用担心向对象中添加新的属性。for of可以与 break、continue和return 配合使用；只要有 iterator 接口的数据结构，都可以使用 for of循环。如：数组 Array、Map、Set、String、arguments对象、Nodelist对象， 就是获取的dom列表集合。


- for...in 循环访问所有可枚举的属性（包括原型属性），意味着如果向数组的原型中添加任何其他属性，这些属性也会出现在循环中。可以用hasOwnProperty（） 避免遍历到原型属性上；
- forEach() 方法用于调用数组的每个元素，并将元素传递给回调函数。forEach() 本身是不支持的 continue 与 break 语句的，但可以通过 [some](https://www.runoob.com/jsref/jsref-some.html) 和 [every](https://www.runoob.com/jsref/jsref-every.html) 来实现。

```js
var arr = [1, 2, 3, 4, 5];
//实现continue（不显示3）
arr.forEach(function (item) {
    if (item === 3) {
        return;
    }
    console.log(item);
});
//实现continue（不显示2）
arr.some(function (item) {
        if (item === 2) {
                return;  // 不能为 return false
        }
        console.log(item);
});
//实现break（只显示1 2 3）
arr.every(function (item) {
    //如果数组中检测到有一个元素不满足，则整个表达式返回 false ，且剩余的元素不会再进行检测。
        console.log(item);
        return item !== 3;
});
```

```js
Object.prototype.objCustom = function() {}; 
Array.prototype.arrCustom = function() {};
let iterable = [3, 5, 7];
iterable.foo = 'hello';
 
for (let i in iterable) {
  console.log(i); // logs 0, 1, 2, "foo", "arrCustom", "objCustom"
}
 
for (let i in iterable) {
  if (iterable.hasOwnProperty(i)) {
    console.log(i); // logs 0, 1, 2, "foo"
  }
}
 
for (let i of iterable) {
  console.log(i); // logs 3, 5, 7
}
```

## 第二章 HTML中的JavaScript

#### 2.1、`<script>`元素

```js
<script type="text/javascript">  //type属性 
 //内容不可以直接出现</script>，需要转义字符转换；
 alert("<\/script>"); //转义字符“\”
</script>
```

2.2、带有 src 属性的`<script>`元素不应该在其`<script>和</script>`标签之间再包含额外的 JavaScript 代码。如果包含了嵌入的代码，则只会下载并执行外部脚本文件，嵌入的代码会被忽略。

2.3、一般都把全部 JavaScript 引用放在`<body>`元素中页面内容的后面，在解析包含的 JavaScript 代码之前，页面的内容将完全呈现在浏览器中。浏览器会按照`<script>`在页面出现的顺序解释，前提未使用**async="async"** 和 **defer=“defer”**

- async属性表示立即开始下载脚本，不需要等待其他脚本，同时也不阻塞文档渲染，即异步加载，异步脚本不能保证按照他们在页面中出现的次序执行；
- defer表示在文档解析和显示完成后在**执行**脚本是没有问题的；
- 二者均只对外部脚本文件有效

## 第三章 语言基础

**3.1、标识符：**可以自主命名的都可以称之为 标识符。例如：变量名、函数名、属性名等。（*标识符中可以含有字母，数字，下划线 _，$*；不能以数字开头；**关键字、保留字、true、false、null不能作为标识符**）

**3.2、严格模式：**ES5引入（"use strict"; 用在脚本开头或者函数内部开头）

#### **3.3、var 介绍：**(let、const)

（1）var message; //未初始化的变量会保存一个特殊的值**undefined**

（2）var：该变量可以用来保存任何值。var message = "hi"; **message = 100;** //有效但是不推荐；

（3）如果变量在函数中定义时没有用var，则为全局变量，在函数外部也可以使用；

**var、let、const区别：**

- 使用let声明的变量可以重新赋值,但是不能在同一作用域内重新声明；

- **var声明提升，let声明的变量不会在作用域中提升**；

- 使用const声明的变量必须赋值初始化,但是不能在同一作用域类重新声明也无法重新赋值；

- 使用let在全局作用域中声明的变量不会成为window对象的属性

  ```js
  var name="mike";console.log(window.name)//'mike'
  let age=26;console.log(window.age)//undefined
  ```

#### **3.4 typeof和instanceof**

typeof对基本数据类型（string、number、undefined、boolean、object、symbol、function）进行判断；instanceof对引用数据类型进行判断，

```js
typeof undefined             // undefined
typeof null                  // object（重点）
null === undefined           // false
null == undefined            // true
var a=new Array();
alert(a instanceof Array)//true
//null可以被理解为是一个特殊的值，undefined可以被认为是声明了一个变量未赋初值
console.log(typeof null);//object
console.log(null instanceof Object)//false
```

**3.5 数据类型**

ES 能够表示的最小数值保存在 **Number.MIN_VALUE** 中——在大多数浏览器中，这个值是 5e-324；能够表示的最大数值保存在**Number.MAX_VALUE** 中；

原始数据类型：Undefined、Null、Boolean、Number、String、Symbol；

**undefined和null区别：**

```js
typeof undefined             // undefined
typeof null                  // object
null === undefined           // false
null == undefined            // true
//null保存在栈中。
```

**3.6 NaN** 即非数值（Not a Number，表示本来要返回数值的结果失败了）。有两个特点：（1）任何涉及 NaN 的操作（例如 NaN/10）都会返回 NaN（2）NaN 与任何值都不相等，包括 NaN 本身。

```js
alert(isNaN(NaN)); //true 
alert(isNaN(10)); //false（10 是一个数值）
alert(isNaN("10")); //false（可以被转换成数值 10）
alert(isNaN("blue")); //true（不能转换成数值）
alert(isNaN(true)); //false（可以被转换成数值 1）
```

**3.7 模板自变量**

（1）其最常用的特性就是支持字符串插值；在插值内也可以调用函数；

```js
var a=2;var b=3;let res=`${a}+${b}=${a+b}`

function capitalize(word){return `${word[0]}.toUpperCase()}${word.slice(1)}`};
console.log(`${capitalize('hello')},${capitalize('world')}!`)
```

(2)用`String.raw`获取原始模板字面量内容

```js
String.raw`first line\nsecond line`;  //first line\nsecond line
```

(3)模板变量支持定义标签函数

```js
//标签Tag函数的语法是函数名后面直接带一个模板字符串，并从模板字符串中的插值表达式中获取参数，
let taggedResult=simpleTag`$(a)+$(b)=$(a+b)`;//标签函数传入的参数依次是原始数组字符串数组（非变量组成的字符串）和对每个表达式求值的结果；
```

#### **3.8 Symbol类型**：

- 符号实例唯一不可变，Symbol最大的用途是用来定义**对象的唯一属性名**；

```js
//一：Symbol（）函数不能用作构造函数，与new一起用；
const sym = new Symbol(); // 抛出错误TypeError
//二：定义及输出
const sym1 = Symbol();
const sym2 = Symbol(42);
const sym3 = Symbol('hello');
console.log(sym1, sym2,sym3); //Symbol() Symbol(42) Symbol(foo)
//三、独一无二的特性
console.log(Symbol() === Symbol());//false
//四、Symbol值不能与其他类型的值进行运算。
console.log(Symbol('Alice') + "Bruce"); // 报错  
//五、Symbol值可以显式转为字符串，也可以转为布尔值，但是不能转为数值。
console.log(sym3.toString()); // Symbol(hello)
console.log(Boolean(sym1)); // true  空也为真
console.log(Boolean(sym2)); // true  
console.log(Number(sym2)); // 报错：TypeError  
```

- 要创建跨文件可用的symbol，甚至跨域（每个都有它自己的全局作用域） , 使用 [`Symbol.for()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol/for) 方法和  [`Symbol.keyFor()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol/keyFor) 方法从全局的symbol注册表设置和取得symbol。

**3.9 操作符**

- 位操作符：按位非（~）、按位与（&）、按位或（|）、按位异或（^）、左移(<<)、有符号右移(>>)、无符号右移(>>>)；

- 布尔操作符：逻辑非（！）、逻辑与（&&）、逻辑或（||）；(数值0、null、NaN、undefined经过逻辑非操作后为true)

- 乘性操作符（乘法、除法、取模或取余）、指数操作符（**）

- 相等操作符：

  ```js
  null == undefined //true 
  true == 1;false == 0 //true 
  "NaN" == NaN ;5 == NaN;NaN == NaN //false 有NaN就是false
  undefined == 0 //false 
  null == 0 //false 
  "5"==5    //true 
  ```

**3.10 语句**

标签语句：常用场景是嵌套循环；可以在后面通过break和continue语句引用；

```js
outermost: for (let i=0; i<10; i++) {
  for (let j=0; j<10; j++) {
    if (i == 5 && j == 5) {  
        console.log(i);
       break outermost;//continue
     }
  }
}
```

**3.11 ECMAScript中的函数与其他语言中的函数不同之处：**

- 不需要指定函数的返回值，因为任何函数可以在任何时候返回任何值。

- 不指定返回值的函数实际上会返回特殊值undefined。

  

## 第四章 变量、作用域和内存

4.1基本数据类型（栈stack中）：Undefined、Null（typeof返回的null是object）、Boolean、Number 和 String、Symbol；（按值传递）

引用数据类型（堆中）：Array、Object、function（按引用传递）；引用类型的存储需要内存的栈区和堆区共同完成，栈区内存保存变量标识符和指向，堆内存中该对象的指针；

```js
var name1 = "Nicholas"; var name2 = new String('Mike'); 
name1.age = 10; name2.age = 20; 
alert(name1.age);  //undefined
alert(name2.age);//20
alert(typeof name1)//string
alert(typeof name2)//object
```

4.2`instanceof` 运算符用于检测构造函数的 `prototype` 属性是否出现在某个实例对象的原型链上。（确定值的引用类型）

4.3 JavaScript垃圾回收策略有**标记清理**（常用）和**引用计数**（不常用）；

内存泄漏的原因：意外声明全局变量、定时器、使用js的闭包



4.4 执行上下文主要有全局上下文和函数上下文，`eval()`调用内部存在第三种上下文；

块级上下文（作用域）：(由最近的的一对包含花括号{}界定)

- 执行上下文分为全局上下文、函数上下文、块级上下文；
- 代码执行流每进人一个新上下文，都会创建一个作用域链， 用于搜索变量和函数。
- 函数或块的局部上下文不仅可以访问自己作用域内的变量，而且也可以访问任何包含上下文乃至全局上下文中的变量。
- 全局上下文只能访问全局上下文中的变量和函数，不能直接访问局部上下文中的任何数据。
- 变量的执行上下文用于确定任么时候释放内存。



## 第五章 基本引用类型

5.1 正则表达式

```
let expression=/pattern/flags
```

RegExp实例的主要方法是exec()、text();

exec()方法用于检索字符串中的正则表达式的匹配，若找到匹配项，则返回第一个匹配信息的数组，如果没有找到，则返回null；返回的数组虽然是Array的实例，但是包含两个额外的属性：index（字符串中匹配模式的起始位置）和input（要查找的数字）；

5.2 charAt()和charCodeAt()

```js
let mes="abcdefg";
console.log(mes.charAt(2));//c
console.log(mes.charCodeAt(2));//99
```

5.3 单例内置对象：Global、Math

5.4 舍入方法

- Math.ceil()执行向上舍入，即它总是将数值向上舍入为最接近的整数；
- Math.floor()执行向下舍入，即它总是将数值向下舍入为最接近的整数；
- Math.round()执行标准舍入，即它总是将数值四舍五入为最接近的整数；
- Math.fround()返回数值最接近的单精度（32位）浮点值表示；

5.5 字符串操作的几种方法: concat()、slice()、substr()、substring()、、indexOf()、lastIndexOf、、startsWith()、endsWith()、includes()、、trim()、repeat()、padStart()、padEnd()、、toLowerCase()、toLocaleLowerCase()、、exec()、match()、search()、、localeCompare()

## 第六章 集合引用类型

#### 对象、数组、Map、WeakMap、Set、WeakSet、

6.1 显示创建Object的实例的两种方法：

```js
let person=new Object();person.name='mike';//构造函数
let person={name:'mike'} //使用对象字面量
```

6.2 ES数组中每个槽位可以存储任意类型的数据，即可以同时存在字符串、数字、对象；**数组是对动态大小；**ES6将数组中的空位当成存在的元素，值为undefined；

**声明数组的几种方法：**

```js
//一是使用Array构造函数
let colors=new Array();
let colors=new Array(3);
let colors=new Array('red','green','blue');
//二是使用数组字面量（array literal）
let colors=['red','green','blue']
//三是from():将类数组结构转换为数组实例
console.log(Array.from("Matt"));//["M","a","t","t"]
const m=new Map().set(1,2).set(3,4);
console.log(Array.from(m));//[[1,2],[3,4]]
const s=new Set().add(1).add(2).add(3);
console.log(Array.from(s));//[1,2,3]
//四是of()：将一组参数转换为数组实例
console.log(Array.of(1,2,3,4))
```

**迭代器方法：**`keys()`返回数组索引、`values()`返回数组元素的迭代器、`entries()`返回索引值对的迭代器；

```js
arr.fill(value,start,end)//批量复制
arr.copyWithin(target,start,end)//填充数组,第一个参数为复制到指定目标的索引位置。后两个为可选元素；
用法:const arr=[0,1,2,3,4,5,6,7];
console.log(arr.fill(9,1,2));  //[0,9,9,3,4,5,6,7]
console.log(arr.copyWithin(2,5,7)//[0,1,5,6,7,5,6,7]
```

所有对象都有的**转换方法**：toLocalString()、toString()、valueOf()

**栈方法**：push()、pop()    队列方法：shift()、push()

**排序方法**：reverse()、sort()升序重排数组，但是通过toString转为字符串在判断

```js
let a=[0,1,5,15,2,9];
//比较函数，如果第一个数应该排在第二个参数前面，则返回负值
a.sort((a,b)=>a<b?-1:a>b?1:0);alert(a)//由小到大
a.sort((a,b)=>a<b?1:a>b?-1:0);alert(a)//由大到小
```

**操作方法**：concat()、sclice(srart,end)、splice(index,howmany,item1,,,indexx)howmany表示删除的个数，可以实现删除，替换，插入、

**搜索方法**：按严格相等搜索（indexOf()、lastIndexOf()、includes()）、按断言函数搜索( find()、findIndex() )

**迭代方法**：（5个）every()、filter()、forEach()、map()、some()、

**并归方法：**reduce()、reduceRight()前一个遍历数组方向从前到后；后一个从后到前；

```js
let a=[0,1,5,15,2,9];
alert(a.reduce((prev,cur,index,array)=>pre+cur));
```

6.3 **定型数组**：ArrayBuffer是所有定型数组及视图引用的基本单位；读写ArrayBuffer的视图是DataView；

6.4 ES6标准引入了新的`iterable`类型，`Array`、`Map`和`Set`都属于`iterable`类型。

6.5 **Map**：与Object只能使用数值、字符串或符号作为键不同，Map可以使用任何JavaScript数据类型作为键。从数组(Map)创建一个可迭代对象， 该对象包含了数组的键值对。

```js
const m=new Map([  ["key1","val1"],
				   ["key2","val2"],
				   ["key3","val3"]      ]);
alert(m.entries===m[Symbol.iterator]);//true
for(let pair of m.entries()){   console.log(pair);   }
//[key1,val1]
//[key2,val2]
//[key3,val3]
```

**方法：**set()添加键值对；get和has查询；size获取数量；delete和clear删除（clear清除所有）

**WeakMap：**弱映射，其与Map的区别有两点：

- WeakMap只接受对象作为键名（null除外），不接受其他类型的值作为键名。
- WeakMap的键名所指向的对象，不计入垃圾回收机制。

6.6 Set 

**方法：**add()添加键值对；has查询；size获取数量；delete和clear删除（clear清除所有）

6.7 创建定型数组的方式包括读取已有的缓冲、使用自有缓冲、填充可迭代结构，以及填充基于任意类型的定型数组。另外，通过.from()和.of()也可以创建定型数组：