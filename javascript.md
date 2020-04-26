基础数据类型
--
1. String
2. Number
3. Boolean
4. Null
5. Undefined
6. Symbol(ES6新增)

引用数据类型
--
Object

使用let、var和const创建变量有什么区别
--
1. var声明变量
    + 没有块级作用域
    + 作用域是它当前执行函数内的上下文
    + 可以在声明之前使用（变量提升）
    + 在同一作用域下，可以重复声明同一个名称变量
2. let和const声明变量
    + 有块级作用域
    + 作用域是它当前执行的代码块或函数内的上下文
    + 不能在声明之前使用，提前使用会抛出异常
    + 在同一作用域下，不能重复声明同一个名称变量
3. const声明变量
    + 只允许一次赋值，不能被多次赋值

prototype和__proto__的关系是什么
--
每个实例对象都有一个私有属性 __proto__，它指向对象构造函数的 prototype 属性；但是 Object.create(null) 创建的对象除外，它没有 __proto__ 属性，也没有 prototype 属性。

    const obj = {}
    obj.__proto__ === Object.prototype // true
    
    function Test(){}
    test.__proto__ == Test.prototype // true
    
    const obj2 = Object.create(null)
    obj2.__proto__ // undefined
    obj2.prototype // undefined
所有的函数都同时拥有 __proto__ 和 protytpe 属性。

函数的 __proto__ 指向自己的函数实现，而 protytpe 是一个对象， 所以函数的 prototype 也有 __proto__ 属性，指向 Object.prototype。

    function func() {}
    func.prototype.__proto__ === Object.prototype // true
Object.prototype.__proto__ 指向 null

    Object.prototype.__proto__ // null

原型继承
--
所有的JS对象都有一个prototype属性，指向它的原型对象。当试图访问一个对象的属性时，如果没有在该对象上找到，它还会搜寻该对象的原型，以及该对象的原型的原型，依次层层向上搜索，直到找到一个名字匹配的属性或到达原型链的末尾。

闭包
---
闭包是指有权访问另一个函数作用域中的变量的函数。

    function sayHi(name) {
        return () => {
           console.log(`Hi! ${name}`)
        }
    }
    const test = sayHi('xiaoming')
    test() // Hi! xiaoming
虽然sayHi函数已经执行完毕，但是其活动对象也不会被销毁，因为test函数仍然引用着sayHi函数中的变量name，这就是闭包。
但也因为闭包引用着另一个函数的变量，导致另一个函数已经不使用了也无法销毁，所以闭包使用过多，会占用较多的内存，这也是一个副作用。