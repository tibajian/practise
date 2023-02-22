# 目录
- [](#)
    - [1.字面量、变量、标识符](#1字面量变量标识符)
    - [2.数据类型与运算符](#2数据类型与运算符)
    - [3.语句、表达式、代码块](#3语句表达式代码块)
    - [4.对象](#4对象)
    - [5.函数](#5函数)
    - [6.垃圾回收](#6垃圾回收)
    - [7.数组](#7数组)
    - [7.Date对象](#7date对象)
    - [8.Math对象](#8math对象)
    - [9.包装类](#9包装类)
    - [10.正则表达式对象](#10正则表达式对象)
    - [11.DOM-Document Object Model](#11dom-document-object-model)
    - [12.BOM - 浏览器对象模型](#12bom---浏览器对象模型)
    - [13.JSON](#13json)

### 1.字面量、变量、标识符
- **字面量**：不可改变的值，可直接使用，如：1，2
- **变量**：保存字面量
  - 变量申明：var、let、count
- **标识符**：自命名的变量名、函数名
  - 下划线、$、非关键字或保留字
### 2.数据类型与运算符
- 六种数据类型：typeof x(类型判断) **String\Number\Boolean\Null\Undefind(基本数据类型)** \Object(引用数据类型)
- 基本类型与引用数据类型
  - 基本类型有实际物理地址，独立存在，相互不影响
  - 引用类型是变量指向内存地址，变量指向相同会互相影响
  ````js
  //a为2，b还是1
  a = 1
  b = a
  a++
  //而对象改变，指向同对象会同时改变
  ````
- 类型转换(数据转为数字、字符串、布尔)：
  - 1.调用方法
    - toString()：不改变原值、null和undefined无String方法
  - 2.调用函数
    - String(): null和undefined可以使用
    - Number(): 有非数字转换和undefined为NaN、空串变0、true为1\false和null为0
  - 3.字符串专用：parseInt(值， 进制)\parseFloot();**传入两个参**;该方法可单取串中前面为数字部分进行转换，如：'123px' => 123
    - 进制：0x3ff(16)\077(8)0b101(2)
  - 4.布尔：Boolean();数字除了0和NaN都为true;非空字符串(空格不算空)都转true;**null和undefined为false**;对象都为true。
- 操作符(运算符)
  - 加减乘除余
    - 任何与NaN得NaN
    - '+' 其他类型与字符串相加为拼接(隐式转换)
    - 其他类型转数字值：**如undefined为NaN、null为0**
  - typeof x(类型判断返回字符串)
  - 一元运算符
    - +a、-a(也会发生类型转换)
    - 前增减、后增减；**a++的值为a,a的值为a+1**、++a的值为自增后值
  - 逻辑运算符 ! && ||  与和或 的短路特性;**&& 全真返回后者；|| 全假返回前者**
  - 赋值运算符 =、+=等
  - 关系运算符 数字与非数字类型数据比较判断，非数字转为数字返回布尔;**任何值与NaN(或转为)比较都为false**;**字符串之间比较按字码编码一位一位比较**
  - 相等运算符 不同类型判断发生转换;NaN不等NaN自己;null==undefined;
  - 条件运算符 表达式?为true取值:为false取值
  - 逗号运算符 声明多变量并赋值
  - 运算符优先级 &&比||优先级高
### 3.语句、表达式、代码块
- 条件 if switch
- 循环 for while
- break continue
### 4.对象
- 多种类型数据组合的类型
- 内建对象
  - ES标准定义的如：Math String Number Function Object
- 宿主对象
  - js运行环境提供的如浏览器环境
- 自定义对象
  - 创建对象
    - 使用构造函数创建
      ````js
      //先创建空对象，然后添加属性，适用于开始不确定对象数据
      var obj = new Object();
      var ary = new Arrary();
      var f = new Function();
      ````
    - 对象字面量创建
    ````js
    //创建多个时代码重复
    var obj = {xxx}
    ````
    - 工厂模式（函数）——借用函数返回多个创建的对象、缺点对象都是Object类型
    - 自定义构造函数模式——先创建自定义构造函数，然后通过new创建对象、缺点-每个对象都有相同的数据（方法）浪费内存
    - 构造加原型——属性在构造函数、方法在原型
    - 继承模式
      - 原型链继承——子类型的原型为父类型的一个实例对象、让子类型的原型的constructor指向子类型
      - 借用构造函数继承（假）——call
      - 组合（上面两个）继承——原型链继承得到方法，call继承得到属性
  - 添加、读取、修改、删除属性
    ````js
    //obj.value和obj['属性名']
    //添加、修改
    obj.name = 'xxx'
    //读取
    obj.age
    //删除
    delete obj.gender
    ````
  - in运算符 判断对象是否含有该属性、'属性名' in obj,但是当对象没有该属性而原型对象有该属性时，也返回真
  - hasOwnProperty  obj.hasOwnProperty('属性')判断对象自己而不是原型，hasOwnProperty方法不在对象中，不在对应原型中，而在原型对象的原型中找
### 5.函数
- 函数对象作用：封装功能
- 函数创建
  ````js
  //使用构造，不推荐
  var fun = new Function('console.log(2223)')
  //函数声明
  function fun () {}
  //函数表达式(匿名函数赋给变量)
  var a = function () {}

  ````
  - 使用工厂方法大量创建对象，在函数内部创建对象，函数形参为对象属性值，就可以在外面大量创建对象；类型都是object,无法区分对象类型。
  - **使用构造函数创建对象，同构造函数称类，对象称类的实例**
  - **对象 instanceof 构造函数、判断对象是否是类的一个实例，所有对象都是Object的实例**
  ````js
    //工厂——理解:调用函数创建对象和内容

    //类型都是object,无法区分对象类型
    function create(name, age) {
      var obj = new Object()
      obj.name = name
      obj.age = age
    }
    var obj1 = create(name, age)
    //构造——理解:创建对象调用函数创建内容

    //构造函数，首字母大写，使用new调用，普通函数直接用
    //构造函数执行流程，1立即创建新对象，2新对象为函数中this，3逐行执行，4返回新对象
    function Create(name, age) {
      this.name
      this.aaa = function(){xxx}
      }
    var obj2 = new create(name, age)
    //构造函数对象方法在函数内创建，调用多次创建多次，优化为在函数外创建函数作为对象方法，但是会污染
    function Create(name, age) {
      this.aaa = fun}
    function fun () {xxx}
    var obj2 = new create(name, age)
    //使用原型对象创建属性,不影响全局
    Create.prototype.fun = function (){}
    ````
- 形参，相当于在函数内部声明变量。实参传值(任意数据类型如对象)给形参。调用函数时解析器不会检查实参类型(数量)，所有使用时可能要判断接收实参值得类型，没有传入实参的形参值为undefined
- arguments
  - arguments和this是每次调用函数时浏览器传递给函数的两个隐含参数
  - arguments,封装实参成类似数组形式，但不是数组
  - arguments的callee属性，callee指向当前函数对象
- 返回值
- 立即执行函数，即不复用，f(){}();
- 对象方法，即对象属性值为函数对象
- 枚举对象属性
  ````js
  for (var a in obj) {console.log(obj[a])}
  ````
- 作用域
  - 全局作用域，在页面打开时创建，关闭销毁
    - 全局变量(作为对象window属性)、函数(作为对象window方法)保存在全局对象window(即浏览器窗口)
    - var
      - 变量声明(只是声明，赋值不会)提前,不论在哪;
      - 函数声明创建的函数提前，可随时调用，表达式创建(var a = f())只是变量声明提前，不能提前调用
  - 函数作用域
    - 调用时创建，使用后销毁
    - 每一次调用的作用域相互独立
    - 函数作用域内可以访问外部的变量，外部不能访问内部
    - 函数作用域中访问变量时，一级一级向外/上找
    - 函数作用域中想访问全局变量而不是自己的，使用window.value
    - 函数作用域中不声明的变量会变成全局变量(因为会向上找)
    - 定义的形参相当于声明了变量
  - this
    - 解析器在调用函数会向函数内部传递隐含参数this，this指向的是对象
    - 此对象为函数执行环境上下文
    - 根据函数调用方式不同，this指向不同，
      - 函数调用，指向对象为window
      - 方法调用，指向对象为该对象
      - 构造函数调用，指向新创建对象
- 原型对象-prototype
  - 创建的所有函数都有自己的属性prototype，该属性指向函数对应的原型对象
  - 普通函数调用prototype没有什么作用
  - 构造函数调用时，所创建的对象有隐含的属性，指向该构造函数的原型对象，可以通过__proto__来访问该属性(同类实例对象.__proto__ == 该构造函数.prototype 为true)
  - 原型对象相当于公共区域，可以将对象公共内容添加进去
  - 当对象查找属性或方法时，先找自己，然后访问原型对象，没有时继续向上找原型对象的原型，直到Object,如果还没有，返回undefined;Object的原型为null
- 打印对象时，输出的实际上是对象的toString()方法返回值——[object Object],可以修改输出为——
  ````js
  obj.prototype.toString = function() {
    return 'obj[name='+this.name+']'
  }
  ````
- 函数方法
  - 调用call和apply时，函数都会执行，并且可以将一个对象指定为第一个参数,此对象成为函数执行时的this；即改变函数的执行环境
    - fun.call(obj,实参1,实参2)
    - fun.apply(obj,[实参1,实参2])
- this
  - 以函数形式调用时，this永远为window
  - 以方法形式调用时，this为方法的对象
  - 以构造函数形式调用时，this为新创建的那个对象
  - 以call和apply调用时，this为指定的对象
  - 在事件响应函数中，this为绑定函数
### 6.垃圾回收
- 垃圾:使用后不再使用的内存空间，判断引用次数/时间
- js 自动垃圾回收机制
### 7.数组
- 索引 index
- 内存空间连续
- 连续数组，离散数组(长度?)
- 创建
  - 构造函数
    ````js
    //单个参表长度
    var ary = new Array(a1, a2)
    ````
  - 数组字面量
    ````js
    var ary = [a1, a2]
    ````
- 属性
  - 获取、修改长度 length
  - 原型对象 prototype
  - 获取索引
- 常用方法
  - 头尾添加删除,添加返回长度，删除返回元素
  - forEach遍历方法
  ````js
  ary.forEach(function (形参1是元素, index索引, ary数组对象) {xxx})
  ````
  - slice(start, end) 返回新指定数组元素，负值为倒数元素 (不影响原数组)
  - splice(start, number, 元素, ary2) 返回删除指定元素,原数组内容增加或减少 (影响原数组)
  - ary.concat(ary1, 元素) 返回连接的新数组 (不影响原数组)
  - ary.join('连接符号') 数组转字符串(不影响原数组)
  - ary.reverse() 反转数组(影响原数组)
  - ary.sort(function(a,b){xxx}) 排序，默认按字符编码(影响原数组),回调函数返回大于0元素才位置交换
- 数组去重
### 7.Date对象
- 创建
  ````js
  var a = new Date()
  ````
- 时间为执行时时间
- 指定时间，传入时间字符串(月 日 年 时间)
- 属性、方法
  - date.getDate() 几号
  - getDay 星期几0~6，0为星期天
  - getMonth 月0~11
  - getFullYear 完整年时间
  - 时分秒等
  - getTime 时间戳——指从标准时间1970年1月1日0时0分0秒到当前时间的毫秒，为了好保存因年月日时的单位进制不同的问题
  - Date.now(),获取当前时间戳，可以用来测试代码性能
### 8.Math对象
- 不用创建，直接使用
- 属性 PI
- 方法
  - 绝对值 Math.abs()
  - 取大/小值
  - 平方，根号
  - 取整 ceil floor round
  - 取伪随机数(0~1) random
    ````JS
    //取其他范围值
    Math.random() * x + y
    ````
### 9.包装类
- 基础类型数据包装对象，有三个包装类可以使用
  - String(),将基本数据类型包装成string对象
  - Number()，将基本数据类型包装成number对象
  - Boolean()，将基本数据类型包装成boolean对象
- 包装类容易产生混淆
- 方法和属性使用只能是对象，但是当给基本数据类型使用属性和方法时，浏览器使用包装类将基本数据类型包装成对象，然后调用属性和方法，最后仍转回基本数据类型
- String方法
  - 操作方法与数组类似，如索引，length
  - charAt(索引) 返回索引指定位置字符
  - charCodeAt(索引) 返回索引指定位置字符的Unicode编码
  - formCharCode(编码) 获取Unicode编码对应的字符，**使用构造函数string调用：String.formCharCode(0x2233)**
  - concat 连接
  - indexOf 检索是否含有指定内容，返回首次出现索引或-1(表示无),indexOf('str',索引)
  - lastIndexOf 反方向检索，其他同上
  - slice 同数组
  - substring 同slice截取字符串，不同，不接受负值(-1),自动调整参数小大排列，substring(start,end)
  - substr 截取 substr(索引，长度)
  - split 字符串转字符串数组，参数为根据什么分割串
  - toUpperCase 变大写(lower小写)
### 10.正则表达式对象
- 正则表达式定义字符串表达规则
- 创建
  - 构造函数(灵活)
    ```js
    //匹配模式(可组合) i 忽略大小写 g 全局匹配
    var reg = new RegExp('正则表达式','匹配模式')
    //使用**test方法判断是否符合**
    var str = 'sdgsagsaeg'
    var result =reg.test(str)
    ```
  - 字面量(简单)
    ```js
    //var reg = /正则表达式/匹配模式
    //表匹配a或者b a|b  或用 [ab]
    //表匹配范围 [a-c]小写 [A-C]大写 [A-c]任意
    //匹配abc 或 adc 或 aec /a[bde]c/
    //匹配除了它之外 /[^0-9]/
    //次数 /a{number}/
      {a,b}出现a到b次
      {a,}a次以上
      a+b a一次以上=={1,}
      * == {0,}
      ? == {0,1}
    //合并 /(ab){3}c/ 找ab连续3次
    //检查开头a /^a/
    //结尾a /a$/
    //同时使用 ^$ 必须严格符合 如/^a$/,表只有一个a，而不是aa
    //.表任意字符 要使用.用转义表示 \.
    //使用构造函数，传入正则因为是字符串，所以转义使用\\.  ,要先把斜杠转义再转其他
    //其他转义 \w (数字，字母，下划线)，W(表w以外)，d(任意数字) ，D(除d外)，s(空格)，S(!s),b(单词边界,即相同单词不多字母，)，B(!b)
    ```
- 配合字符串方法——传递正则表达式作为参数
  - split 分 传递正则表达式作为参数，分全部
  - search 搜素 是否含有指定内容，返回第一次索引或-1
  - match 返回 找到多个匹配内容并封装到数组，默认找一个，设置全局g找所有、
  - replace 替换 replace('匹配','替换') 默认一个，设置g
- 检查手机号，邮箱，编号，去空格(单词前后中)
### 11.DOM-Document Object Model
- 操作web页面所有内容
- Dom树模型
- 节点及**dom查询**
  - 查询时，一级一级向下找
  - 文档节点,代表网页，浏览器提供，这个对象是window的属性
    - 通过document对象调用
      - getElementById(),通过id获取一个元素节点对象
      - getElementsByTagName()，通过标签名获取一组元素节点对象，返回的是类数组对象
      - getElementsByName()，通过name属性获取一组元素节点对象
      - getElementsByClassName() 获取元素属性为class
      - querySelector() 根据css选择器，返回第一个
      - querySelectorAll() all全选
  - 元素节点
    - 元素.属性名，除了class，它是保留字，使用应该为 .className
      - 获取元素节点的子节点
        - getElementsByTagName()，返回当前节点的指定标签后代节点
        - childNodes -属性 返回当前节点的所有后代节点(包括文本节点，标签间空白也会是文本节点)
        - children -属性 获取当前元素的所有**子元素**
        - firstChild -属性 包括文本节点
        - lastChild -属性 包括文本节点
  - 属性节点
  - 文本节点
      - 获取父，兄弟节点
        - parentNode -属性 不包括文本节点
        - previousSibling -属性 兄弟节点 包括文本节点
        - nextSibling -属性 后一个兄弟节点
      - 获取body标签
        - document.getElementsByTagName('body')[0]
        - document.body   (好用)
      - html根标签
        - document.documentElement
      - 所有元素
        - document.all
        - document.getElementsByTagName('*')
- 节点共有属性
  - nodeName
  - nodeType
  - nodeValue
- 获取button对象,修改内容
    ```js
    var btn = document.getElementById('按钮id')
    //innerHTML,可获取元素内部的HTML代码
    //innerText,获取元素内文本内容
    btn.innerHTML = 'XXX'
    ```
- 事件-Event
  - 页面中发生的事件如交互行为
  - 给事件对应属性设置js代码而不是在HTML标签内写
    - 获取对象后，给对象绑定事件
      ```js
      //函数称单机绑定函数
      btn.onclick = function(){xxx}
      ```
  - 鼠标移动 - onmousemove、
  - 鼠标滚轮
- 事件对象
  - 事件响应函数触发时，浏览器每次将一个事件对象作为实参传给响应函数
  - 事件对象中封装了事件的所有信息如：鼠标坐标、按键、滚轮方向等等
  - event.clientX 鼠标横坐标
    - 坐标是相对浏览器可见页面的
  - IE8及一下，事件对象保存在window的属性中
    - window.event.clientX
  - event.pageX  坐标是相对浏览器整个页面的(IE8不兼容)
  - 浏览器定义的页面滚动条是body(谷歌)还是html的
  - 事件冒泡(Bubble)
    - 事件冒泡即事件的向上传导，当后代元素上的事件被触发时，其祖先元素相同的事件也触发。而不是被覆盖或向下
    - 取消冒泡。给元素的事件对象  event.cancelBubble = true
    - 事件委任
      - 绑定一次事件，能让多个元素也能有该事件，包括新添加元素
      - 给祖先元素绑定，后代元素事件触发时产生冒泡到祖先响应函数
      - 利用到事件对象 —— event.target
  - 事件绑定
    - 多个绑定相同响应函数会被后者覆盖
    - 解决方法——addEventListener()可以为一个事件绑定多个响应函数
    - addEventListener() 的this为绑定事件的对象
      - 参数
        - 1-事件字符串，不要on
        - 2-回调函数，事件触发时调用
        - 3-是否在捕获阶段触发需要一个布尔值，一般传false
          ```js
          btn.addEventListener('click',function(){alert(1)},false)btn.addEventListener('click',function(){alert(2)},false)
          ```
    - IE8 attachEvent() 绑定多个响应函数
      - 与addEventListener()不同的是，attachEvent是后绑定先执行
      - attachEvent 的this为window
      -  参数
        - 1-事件字符串，要on
        - 2-回调函数，事件触发时调用
        ```js
          btn.attachEvent('onclick',function(){alert(1)})
        ```
  - 事件传播
    - 1-捕获阶段
      - 捕获时，从最外层祖先元素到目标元素，但不触发事件
      - 如果希望捕获时触发事件，给addEventListener()的第三个参数设置true
    - 2-目标阶段
      - 事件捕获到目标
    - 3-冒泡阶段
      - 事件从目标元素触发并向上传递
- 浏览器加载自上而下，优先加载页面内容，js后加载
  - 因此，先加载js可能会产生错误
  - onload事件会在页面加载完成后触发，由此：
    ```js
    //对应响应函数在加载完成后触发
    window.onload = function(){xxx}
    ```
- dom增删改
    - document.createElement()
      - 用于创建一个元素节点，参数为标签名
      - 返回该新节点对象
    - document.createTextNode()
      - 创建文本节点对象
    - 创建后添加联系  (父节点可以直接找，也可以调用 子节点.parentNode )
      - 父节点.appendChild(子节点) 父子
      - 父节点.insertBefore(新节点，旧节点)   增加父节点的指定子节点前面
      - 父节点.replaceChild(新节点，旧节点)  替换父节点的子节点
      - 父节点.removeChild() 删除父节点的子节点
      - 父节点.innerHTML += '<>xxx</>' //这种使用会刷新父节点的所有子节点状态，不推荐
        - 优化一下：1-先创建新节点，2-然后添加内容 节点.innerHTML = 'XXX'   3-最后把节点添加到父节点
  - 增(从上至下添加节点)
    - 1-新增元素和元素属性值以及文本内容
    - 2-给新增内容设置保存或展示的格式(即html结构)
    - 3-将新增内容添加进设置的格式中
    - 4-最后添加到原页面中
  - 删
    - 实现超链接删除功能时，取消链接的默认跳转行为(还有如表单提交跳转)
      - return false  添加到超链接的响应函数里
      - 或者给html里a标签的链接地址设置为 href = "javascript: ;"
    - 给链接响应函数设置删除
      - 1-获取链接要删除的元素节点
      - 1-1为防误操作，加一个删除提示框(window的confirm()方法)，提高体验。注意-添加提示框返回值和删除元素节点操作之间的联系
      - 2-父节点.removeChild()
  - a链接的索引
      ```js
      //注意单击响应函数在页面加载函数后单击执行。因此在单击响应函数里获得外面的加载函数里的内容会不正确
      window.onload = function(){
        for (var i = 0; i < a.length = 3; i++) {
          a[i]
        }
        yyy.onclick = function(){
          //此时的a[i]直接为a[3]而不是会从0开始
          a[i]
        }
      }
      ```
- dom操作css
  - style获取css
    - 元素.style.样式名 = 样式值
      ```js
      box.style.width = "100px"
      ```
    - 如果样式名中有‘-‘等，如background-color 修改为驼峰命名 backgroundColor
    - 这种修改的样式是内联样式，优先级高，但低于 !important
    - 读取的也是内联
  - 获取当前页面css(可以获取页面生效的css，无则为默认值)(兼容)
    - 元素.currenStyle.样式名
  - getComputedStyle(元素，可传伪元素(一般传null)).样式
    - 返回样式的对象
    - 对象属性值为真实值而不是auto
  - 返回不带数字的样式值
    - clientWidth/Height
      - 获取的宽高包括内容区，内边距作用的结果。可见高度。只读
    - offsetWidth/Height
      - 获取的宽高包括内容区，内边距，**边框**作用的结果。只读
    - offsetParent
      - 获取最近的定位祖先元素或body
    - offfsetLeft/Top
      - 当前元素相对定位父元素的偏移量
    - scrollWidth/height
      - 元素滚动条的高度(包括隐藏部分)
    - scrollLeft/right
      - 滚动条滚动的大小
    - scrollTop/Left
      - 滚动条距离上面的距离
        - scrollHeight - scrollTop == clientHeight ——**表示滚动条滚动到最下面**
        - 应用在如：确认已读协议了(即要把滚动条拉到底)，才能确认继续操作。具体给按钮加disabled属性，滚动到底修改为可用(设置按钮.disabled == false)
### 12.BOM - 浏览器对象模型
- bom对象
  - Window
    - 代表窗口，也是全局对象
    - 方法和属性
      - 方法-**定时**
        - setInterval()
          - 定时调用
          - 将函数每隔一段时间调用一次
          - 参数
            - 回调函数
            - 时间 毫秒
          - 返回值
            - 返回一个Number类型的数据
            - 这个数字为此次定时器的唯一标识
        - 关闭定时
        - clearInterval(标识) 如果接受的不是定时器标识，不会报错
              ```js
              setInterval(function(){}, 100){}
              ```
      - 延时调用
        - setTimeout()
        - 隔一段时间执行**一次**
        - 关闭 clearTimeout()
  - Navigator
    - 代表当前浏览器信息，用以识别浏览器
    - 由于历史原因Navigator的大部分属性已经识别不了
    - 现在一般使用 **Navigator.userAgent** 如：Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36
    - 识别IE 判断 'ActiveXObject' in window 因为ActiveXObject只有IE有
  - Location
    - 代表浏览器地址栏信息，用以获取地址或跳转
  - History
    - 浏览器历史记录，但因为用户隐私问题，该对象不能获取具体的信息，只能操作浏览器翻页，且访问有时效
  - Screen
    - 用户屏幕信息
  - 以上对象都是作为全局window的属性保存，可以直接使用
### 13.JSON
- 特殊的字符串，可悲任何语言识别
- 用作数据交互
- 与js对象格式一样，只是属性名加双引号
- 转换为js JSON.parse(JSON)
- 转换为JSON JSON.stringify(js对象)
