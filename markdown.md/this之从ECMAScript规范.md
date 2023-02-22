//ECMAScript 的类型分为语言类型和规范类型。
  //规范类型包括：Reference, List, Completion, Property Descriptor, Property Identifier, Lexical Environment, 和 Environment Record。
  // {base value --基值
  // referenced name --参考名称
  // strict reference --严格参照}
  // base value 就是属性所在的对象或者就是 EnvironmentRecord，它的值只可能是 undefined, an Object, a Boolean, a String, a Number, or an environment record 其中的一种。
  // referenced name 就是属性的名称。
  var foo = 1;

  // 对应的Reference是：
  var fooReference = {
    base: EnvironmentRecord,
    name: 'foo',
    strict: false
  };
  // Reference方法 1、 GetBase 返回 reference 的 base value
  // 2、 IsPeopertyReference 如果 base value 是一个对象，就返回true
  // GetValue 返回对象属性真正的值。如果使用了GetValue如（(foo.bar = foo.bar)、(false || foo.bar)、(foo.bar, foo.bar)）就不是Reference
  //this
  {
    //1、计算 MemberExpression 的结果赋值给 ref
      //简单理解 MemberExpression 其实就是函数调用()左边的部分
    //2、判断 ref 是不是一个 Reference 类型

    //2.1 如果 ref 是 Reference，并且 IsPropertyReference(ref) （是否是对象）是 true, 那么 this 的值为 GetBase(ref)

    //2.2 如果 ref 是 Reference，并且 base value 值是 Environment Record , 那么this的值为 ImplicitThisValue(ref)；查看规范 10.2.1.1.6，ImplicitThisValue 方法的介绍：该函数始终返回 undefined

    //2.3 如果 ref 不是 Reference，那么 this 的值为 undefined
  }
