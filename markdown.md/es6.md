1. let
  - 声明唯一
  - 块级作用域
  - 无变量提升
  - 不会影响作用域链
2. const 定义常量
  ```js
  const A = 'bb'
  ```
  - 一定要赋初始值
  - 一般常量使用大写
  - 常量值不能修改
  - 块级作用域
  - 对于数组和对象的元素修改，不算修改常量，只是修改地址
3. 解构赋值
  - 按一定模式从数组和对象中提取值，对变量进行赋值
  ```js
  const F4 = ['tang','song','yuan','ming']
  let [唐,宋,元,明] = F4
  \\即 唐 = 'tang'

  const zhao = {
    name: 'zhao',
    age: 1,
    a: function(){
      console.log('啊吧啊吧')
    }
  }
  let {name,age,a} = zhao
  \\相当于把对象的属性创建对应的变量，且同值
  ```
4. 模板字符串
  - `sdfsafa` 'adf' "sdff"
  - `` 内容可以直接出现换行符
  - 变量直接拼接
      ```js
      let a = `aaa`
      let b = `${a}bbb`
      ```
5. 简化对象写法
  - 对象中直接写变量和函数，作为对象的属性和方法
  ```js
  let a = 'a'
  let b = function () {console.log(a)}
  const c = {
    a,//相当于 a: a,
    b,// b: b
      // c: function(){console.log(b)}
    c(){
      console.log(b)
    }
  }
6. 箭头函数
  ```js
  let funa = function(){}
  let funb = () => {}
  ```
  - 箭头函数的this是静态的，this始终指向声明时所在作用域下的this。使用call也无法改变指向
    - 箭头函数适合与this无关的回调，如定时器、数组方法回调
    - 不适合与this有关的回调，如事件回调、对象的方法
  - 无法作为构造实例化对象
  - 不能使用arguments变量
  - 箭头函数简写
    - 只有一个形参，省略()
    - 代码体只有一条语句，省略{},return也必须省略
    ```js
    let a = b => b*b
    ```
7. 函数参数默认值
  ```js
  function c(a,b = 1) {
    return a + b
  }
  ```
8. rest参数，代替arguments，就是... 位于形参末尾
9. 扩展运算符 ...  能将数组转换成逗号分隔的参数序列 位于实参位置
  ```js
  const a = ['a','b','c']
  function aa (){console.log(arguments)}
  aa(...a)//相当于aa('a','b','c')
  //数组合并、克隆(浅拷贝)
  const a = ['a']
  const b = ['b']
  const ab = a.concat(b)
  const ab = [...a,...b]
  const c = [...ab]
  //将伪数组转数组
  const divs = document.querySelectorAll('div')
  const divArr = [...divs]
  ```
10. Symbol 原始数据类型
  - Symbol 值唯一，用来解决命名冲突
  - Symbol的值不能与其他数据参与运算
  - Symbol定义的对象属性不能使用 for in 遍历循环，但可以使用Reflect.ownKeys 来获取对象的所有键名
  ```JS
  let s = Symbol()
  let s2 = Symbol('张三')
  let s3 = Symbol('张三')
  //s2 不等于 s3
  let s4 = Symbol.for('zhangsan')
  let s5 = Symbol.for('zhangsan')
  //s4 = s5

  //给未知对象添加属性
  //不知是否有a，b属性
  let Obj = {...}
  let obj2 = {
    a: Symbol(),
    b: Symbol(),
  }
  Obj[obj2.a] = function(){}
  ```
11. 迭代器(Iterator) 是一种接口
  - Iterator接口主要提供 for of
  ```js
  const xiyou = ['tangseng','sunwukong','zhubajie','shaseng']
  //返回键名123
  for (let a in xiyou) {
    console.log(a)
  }
  //返回键值
  for (let a of xiyou) {
    console.log(a)
  }
  ```
12. 生成器 是一种特殊的函数，用来异步编程
  ```JS
  //生成器
  function * gen () {
    //yield 相当于把此函数分割开
    yield '1'
    yield '2'
    yield '3'
  }
  //调用
  let iterator = gen()
  iterator.next()//next里传参，是作为上一次yield的结果返回
  ```
13. Promise 是一个构造函数，用来封装异步操作并且可以获取其成功或失败的结果
  ```js
  //实例化Promise对象
  const p = new Promise(function(resolve, reject){
    setTimeout(function(){
      let date = '数据库用户数据'
      resolve(date)

      let err = '读取失败'
      reject(err)
    },1000)
  })
  //调用Promise的then方法
  p.then(function(value){
    console.log(value)
  }, function(reason){
    console.log(reason)
  })
  ```
14. Set(集合)，类似数组，但成员值唯一，集合实现了iterator接口，所以可以使用for of
  - size 返回集合的元素个数
  - add 增加一个新元素，返回当前集合
  - delete 删除元素，返回boolean值
  - has 检测是否含有某个值，返回boolean值
  - clear 清空
  ```js
  let s = new Set()
  let s2 = new Set([1,'2',a])

  //集合使用
  数组去重
  let a = [1,1,2,2,3]
  let result = [...new Set(a)]
  交集
  let b = [1,2,3,4]
  let result = [...new Set(a)].filter(item => {
    let s2 = new Set(b)
    if (s2.has(item)) {
      return true
    }else return false
  })
  并集
  let c = [...new Set([...a,...b])]
  差集
  let d = [...new Set(a)].filter(item => !new Set(b).has(item))
  ```
15. Map 类似对象，也是键值对的集合，但键的范围不限于字符串，Map也实现了iterator接口，也可以使用扩展运算符和for of。
  - size
  - set
  - get
  - has
  - clear
  ```js
  let m = new Map()
  m.set('name','jojo')
16. class 类
  ```JS
  class Phone{
    constructor(brand, price){
      this.brand = brand
      this.price = price
    }
    call(){
      console.log('打电话')
    }
  }
  let onePlus = new Phone('1+',1999)
  ```
  - es5构造函数的继承和class类的继承
  - 子类对父类的重写
  - get set
17. object方法扩展
  Object.is 判断两个值是否完全相等
  Object.assign 对象的合并
  Object.setPrototypeOf/getPrototypeOf 设置原型对象
18. 模块化
  - 优点：防止命名冲突
        代码复用
        高维护性
  - 模块化规范：CommonJS => NodeJS、Browserify
              AMD => requireJS
              CMD => seaJS
  - 语法： export -- 命令用于规定模块的对外接口
          import -- 命令用于输入其他模块提供的功能
  ```js
  //在模块中设置（单独文件）
    //1.分别暴露
    export let school = 'asdfh'
    export function aa () {
      console.log('sdfihasdf')
    }
    //2.统一暴露
    let xxx
    function xx (){}
    expoty {xxx, xx}
    //3.默认暴露
    export default {
      a: 'sdf',
      b: function(){dd}
    }

  //在主文件引入
  <script type = "module">
    //1.通用导入
    import * as a1 form "./地址"
    //2.结构赋值形式
    import {a,b,  c as 别名(防止命名冲突)} form "./地址"
      //2.1结构赋值形式--默认暴露引入
      import {default as a2别名} from "./地址"
    //3.简便形式 针对默认暴露
    import a3 from "./地址"
  //然后就可以使用数据了
  </script>


  //可以把引入语句放入一个单独文件
  引入文件
    import * as a1 form "./地址"
  主文件
    <script src="./引入文件地址" type= "module"></script>

  ```
19. babel
  babel是一个javascript编辑器
  将代码解释成浏览器能识别的代码，解决浏览器兼容问题
20. ES7
  - Array.prototype.include -- 检测数组中是否包含某个元素，返回布尔类型
  - 指数运算符‘ ** ’，实现幂运算，功能与Math.pow结果相同
21. ES8
  - async和await 两种语法结合可以让异步代码像同步代码一样
  - async函数
    - 1. async函数的返回值为promise对象
    - 2. promise对象的结果由async函数执行的返回值决定
  - await表达式
    - await必须写在async函数中
    - await右侧的表达式一般为promise对象
    - await返回的是promise成功的值
    - await的promise失败了，就会抛出异常，需要通过try...catch捕获处理

  - Object.values和Object.entries
    - Object.values()方法返回一个给定对象的所有可枚举属性值的数组
    - Object.entries()方法返回一个给定对象自身可遍历属性[key,value]的数组

  - Object.getOwnPropertyDescriptors
    - 方法返回指定对象所有自身属性的描述对象
22. ES9 为对象提供的rest参数和扩展运算符
  ...user
23. 正则扩展 - 命名捕获分组
24. 正则扩展 - 反向断言
25. 正则扩展 - dotAll模式
26. 对象扩展方法 - Object.fromEntries
27. 字符串方法 - trimStart trimEnd 清除空白
28. 数组方法 - flat (将多维数组转低维) flatMap
29. Symbol.prototype.description
30. 私有属性
31. Promise.allSettled
32. String.prototype.matchAll
33. 可选链操作符
34. 动态improt
35. BigInt
36. 绝对全局对象 - globalThis
