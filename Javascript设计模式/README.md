> Book Name: 《JavaScript设计模式》
> Author: 张容铭

#### Chapter 2

> 组合继承

```js
function SuperClass(name) {
  this.name = name
  this.arr = []
}

SuperClass.prototype.getName = function() {
  console.log(thit.name)
} 

function SubClass(name) {
  // 继承父类中的this.name & this.arr
  SuperClass.call(this, name)
}

// 继承父类原型链上的方法
SubClass.prototype = new SuperClass()
```

**调用了两遍父类构造方法**

> 原型链继承

```js
function inheritObject(o) {
  function F() {}
  F.prototype = o
  return new F()
}
```

**但是新创建的对象发生修改会影响之前的对象以及父对象**

> 寄生组合式继承

```js
function inheritPrototype(subClass, superClass) {
  // 复制一份父类的原型
  var p = inheritObject(superClass.prototype)

  p.constructor = subClass
  p.prototype = p
}

```


#### Chapter 4: Factory

> 安全的工厂方法

```js
var Factory = function*(type, content) {
  if (this instanceof Factory) {
    var s = new this[type](content)
    return s
  } else {
    return new Factory(type, content)
  }
}

// 防止缺少new的情况，导致this执行window，而无法访问到原型链上的方法
```

#### Chapter 5: 建造者模式

理念为：通过拼接组合的方式，自由组合成自己需要的对象，自由度很高

```js
var Person = function(name, work) {
  var _person = new Human()

  _person.name = new Named(name)

  _person.work = new Work(work)

  return _person
}
```


#### Chapter 8: Singleton

> 惰性单例

```js
var LazySingle = (function() {
  var _instance = null

  function Single() {
    return {
      publicMethod: function(){},
      publicProperty: '1',
    }
  }

  return function() {
    if (!_instance) {
      _instance = Single()
    }

    return _instance
  }
})()
```

#### Chapter 12: Decorator

在不影响之前事件执行的前提下，添加新的事件

```js
var decorator = function(input, fn) {
  if (typeof input.onclick = 'function') {
    var oldClickFn = input.onclick;
    input.onclick = function() {
      oldClickFn()
      fn()
    }
  } else {
    input.onclick = fn
  }
}
```

#### Chapter 15: 享元模式

比如说翻页需求，并不需要每次翻页都进行item的创建，可以在首页时创建，并缓存起来，之后只需渲染数据即可。


#### Chapter 21: 命令模式

绘图命令

```js
var CanvasCommand = (function() {
  var canvas = document.getElementById('canvas')
  var ctx = canvas.getContext('2d')

  var Action = {
    fillStyle: function(){}
    // ....
  }

  return {
    excute: function(meg) {
      if (!msg) return;

      if (msg.length) {
        for (var i = 0, len = msg.length; i <len; i++) arguments.callee(msg[i])
      } else {
        msg.param = Object.prototype.toString.call(msg.param) === "[Object Array]" ? msg.param : [msg.param]
        Action[msg.command].apply(Action, msg.param)
      }
    }
  }
})()

// example
CanvasCommand.execute([{command: 'fillStyle', param: 'red'}])
```


#### Chapter 23: Mediator

在中介者模式中，发送消息的只有中介一个，活跃对象在中介者订阅消息，之后触发统一发送消息

```js
Mediator.register('demo', () => console.log('a'))

Mediator.register('demo', () => console.log('b'))

Mediator.send('demo')
// a
// b
```


#### Chapter 27: Operate of Responsibility

链模式：通过在对象方法中将当前对象返回，实现对同一个对象多个方法的链式调用。

**jQuery**

> Step one

```js
var A = function() {
  return A.fn
}

A.fn = A.prototype = {}
```

`fn`此时被看作为A的一个属性

现在我们可以通过`A().func`去掉用原型链上的方法

> Step two

```js
var A = function(selector) {
  return A.fn.init(selector)
}

A.fn = A.prototype = {
  init: function(selector) {
    this[0] = document.getElementById(selector)
    this.length = 1
    return this
  },
  length: 2,
  size: function() {}
}
```

此时存在的问题为：后获取的元素会将前一个元素的值进行覆盖，原因在于`return A.fn.init()`对象指向同一个对象造成的。

但是如果改为`return new A.fn.init()`，则会导致方法的丢失。原因为`return A.fn.init()`返回的`this`是指向`A.fn 和 A.prototype`，而`return new A.fn.init()`中进行了new对对象内的属性复制，this也就不再指向`A.fn和A.prototype`

`return new A.fn.init('demo')`中this的值为`A.fn.A.init {0:div#demo,length:1}`，并不包含其中的方法


> Step three

```js
var A = function(selector) {
  return new A.fn.init(selector)
}

A.fn = A.prototype = {
  constructor: A,
  init: function(selector) {
    // ...
  }
}

A.fn.init.protype = A.fn
```

#### Throttler

```js
var throttle = function() {
  var isClear = arguments[0], fn
  if (typeof isClear === 'boolean') {
    fn = arguments[1]
    isClear && fn.__throttleID && clearTimeout(fn.__throttleID)
  } else {
    fn = isClear
    param = arguments[1]
    var p = extend({
      context: null,
      args: [],
      time: 300
    }, param)
    // 清除计时器
    arguments.callee(true, fn)
    fn.__throttleID = setTimeout(function() {
      fn.apply(p.context, p.args)
    }, p.time)
  }
}
```


#### Chapter 32: layier

在绑定事件的时候，通常需要写polyfill，但是每次进行agent的判断是十分耗费资源的

```js
A.on = function(dom, type, fn) {
  if (dom.addEventListener) {
    return function(dom, type, fn) {
      dom.addEventListener(type, fn, false)
    }
  }
  // ...
}
```

### 感受

总体来说很接地气，没有特别的干货，比较适合新手阅读，阅读过程十分的轻松。

2018.11.17

## DONE