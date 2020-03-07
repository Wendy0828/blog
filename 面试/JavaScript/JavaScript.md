#### 原型(prototype)：
答：一个简单的对象，相当于一个对象模版，用于实现对象的属性继承
#### 构造函数(constructor):
答：通过new创建一个对象的函数

#### 实例：
答：由构造函数和new创建出来的对象。实例通过__proto__指向原型，通过constructor指向构造函数

#### 原型/构造函数/实例关系：
* 实例.__proto__ === 原型
* 原型.constructor === 构造函数
* 构造函数.prototype === 原型
* 实例.constructor === 构造 函数

#### __proto__：
* 对象特有
* 指向上层(创建自己的那个构造函数)的原型对象(prototype)
* 对象从prototype继承属性和方法

#### prototype：
* 函数特有
* 用于存储要共享的属性和方法

#### constructor：
* 函数特有，定义在prototype里面
* 通过new创建实例时，该实例便继承了prototype的属性和方法

#### 对象是由构造函数创建的
* 原型链顶端是Object.prototype
* 所有对象(Object/Function/Array/普通对象等)，它们的__proto__均指向Function.prototype。构造函数创建的对象都是Function的实例
* 除了Object，所有对象(构造函数)的prototype，均继承自Object.prototype


#### 原型链：
答：原型链是由原型对象组成，每个对象都有__proto__属性，指向创建该对象的构造函数原型，__proto__将对象连接起来组成了原型链。用于实现继承和共享数据的有限的对象链。通俗点讲利用原型让一个引用类型继承另一个引用类型的属性和方法
* 属性查找机制：当查找对象属性时，若实例对象自身不存在该属性，则沿着原型链往上一级查找，找到时则输出，不存在时，则继续沿着原型链往上一级查找，直至最顶级的原型对象Object.prototype，若还没有找到，则输出undefined
* 属性修改机制：只会修改实例对象本身的属性，若不存在，则进行添加该属性

#### 执行上下文:
答：相当于一个对象，代码从上到下依次执行，就叫做执行上下文

##### 属性：
* 变量对象(VO)
* 作用域链(词法作用域)
* this指向

##### 特点：
* 单线程，在主进程运行
* 同步执行，从上往下依次执行
* 全局上下文只能有一个，在浏览器关闭时自动销毁
* 函数的执行上下文没有数目限制
* 函数每被调用一次，就会产生一个新的执行上下文

##### 生命周期:
* 创建阶段：生成变量对象、建立作用域链、确定this指向
* 执行阶段：变量赋值、函数引用、执行其他代码
* 销毁阶段：执行完毕出栈，等待回收被销毁

##### 执行过程：
答：执行全局代码时，会产生一个执行上下文环境，每次调用函数都又会产生执行上下文环境。当函数调用完后，这个上下文环境以及其中的数据都会被消除，再重新回到全局上下文环境。处于活动状态下的执行上下文环境只有一个

#### 变量对象(VO)：
答：可以抽象为一种数据作用域，也可以理解为是一个简单的对象，它存储着该执行上下文中所有的变量和函数声明(不包括函数表达式)

#### 活动对象(AO)：
答：当变量对象所处的上下文为active EC(Execution Context,执行上下文) 时，称为活动对象

#### 作用域：
答：该执行上下文中声明的变量和声明的作用范围。可分为块级作用域和函数作用域

##### 特性：
* 声明提前：一个声明在函数体内都是可见的，函数优先于变量
* 非匿名自执行函数，函数变量是只读状态，无法修改

#### 作用域链：
答：作用域链可以理解为一组对象列表，包含父级和自身的变量对象，因此便能通过作用域链访问到父级里声明的变量或函数

#### 闭包：
答：闭包属于一种特殊的作用域，称为静态作用域。它的定义可以理解为父函数被销毁的情况下，返回的子函数的[[scope]]中仍然保留着父级函数的单变量对象和作用域链，因此可以继续访问到父级的变量对象，这样的函数称为闭包

##### 闭包会产生一个很经典问题：
答：多个子函数的[[scope]]都是同时指向父级，是完全共享的。因此当父级的变量对象被修改时，所有的子函数都会受到影响

##### 问题解决方案：
* 变量通过函数参数的形式传入，避免使用默认的[[scope]]向上查找
* 使用setTimeout包裹，通过第三个参数传入
* 使用块级作用域，让变量成为自己上下文的属性，避免共享

#### script引入方式：
* html静态<script>引入
* js动态插入<script>
* <script defer>：延迟加载，元素解析完后执行
* <script async>：异步加载，但执行时会阻塞元素渲染

#### 对象的拷贝：
* 浅拷贝：以赋值的形式拷贝引用对象，扔指向同一个地址，修改时原对象也会受到影响
    * Object.assign
    * 展开运算符(...)
* 深拷贝：完全拷贝一个新对象，修改时原对象不再受到任何影响
    * JSON.parse(JSON.stringify(obj))：性能最快
        * 具有循环引用的对象时，报错
        * 当值为函数、undefined、symbol时，无法拷贝
    * 递归进行逐一赋值

#### new运算符的执行过程：
* 新生成一个对象
* 链接到原型：obj._proto_ = Con.prototype
* 绑定this： apply
* 返回新对象(若构造函数有自己的return时，返回该值)

#### instanceof原理：
答：能在实例的原型对象链中找到该构造函数的prototype属性所指向的原型对象，就返回true

```javascript
// __proto__: 代表原型对象链
instance.[__proto__...] === instance.constructor.prototype
// return true
```
#### 代码的复用：
答：当发现任何代码开始写第二遍时，就要开始考虑如何复用。

##### 代码复用方式：
* 函数封装
* 继承
* 复制extend
* 混入mixin
* 借用apply/call

#### ☆继承：
答：JavaScript中支持继承，但不支持接口继承，实现继承的主要依靠是原型链来实现的
* 原型链：利用原型让一个引用类型继承另一个引用类型的属性和方法
    * 缺点1: 包含引用类型值的原型属性会被所有示例共享，这会导致对一个实例修改会影响另一个实例 
    * 缺点2: 在创建子类型的实例时，不能向超类型的构造函数中传递参数
* 构造函数：在子类型构造函数的内部调用超类型的构造函数。 通过使用apply()和call()方法可以在新创建的对象上执行构造函数
    * 优点：可以在子类型构造函数中向超类型构造函数传递参数
    * 缺点1: 无法避免构造函数模式存在的问题，方法都在构造函数中定义，因此无法复用函数
    * 缺点2：在超类型的原型中定义的方法，对子类型而言是不可见的，因此这种技术很少单独使用
* 组合继承：将原型链和借用构造函数来实现对实例属性的继承。既通过在原型上定义方法实现了函数的复用，又能保证每个实例都有它自己的属性
    * 优点：避免了原型链和借用构造函数的确定，融合了他们的优点，是JavaScript中最常用的继承模式。isntanceof和isprototypeOf()也能够用于识别基于组合继承创建的对象
* 原型式继承
* 寄生式继承
* 寄生组合式继承

#### 类型转换：
在JS中使用运算符号或对比符时，会自动隐式转换，规则：
* -、*、/、%：一律转换成数值后计算
* +：
    * 数字 + 对象，优先调用对象的valueOf -> toString
    * 数字 + 字符串 = 字符串，运算顺序从左到右
    * 数字 + boolean/null -> 数字
    * 数字 + undefined -> NaN
* [1].toString() === '1'
* {}.toString() === '[object object]'
* NaN !== NaN、+undefined为NaN

#### 类型判断：
* 基本类型(null): 使用String(null)
* 基本类型(string/number/boolean/undefined) + function：直接使用typeof判断
* 引用类型(Array/Date/RegExp/Error)：调用toString后根据[object XXX]进行判断

```javascript
// 判断封装
let class2type = {}
'Array Date RegExp Object Error'.split(' ').forEach(e => class2type[ '[object ' + e + ']' ] = e.toLowerCase()) 

function type(obj) {
    if (obj == null) return String(obj)
    return typeof obj === 'object' ? class2type[ Object.prototype.toString.call(obj) ] || 'object' : typeof obj
}
```
#### 模块化：
答：它大大提高了项目的可维护性、可拓展和可协作性。在浏览器中使用ES6的模块化支持，在Node中使用commonjs的模块化支持
* 分类
    * es6：import/export
    * commonjs: require/module.exports/exports
    * amd: require/defined
* require 与 import区别
    * require支持动态导入；import不支持，正在提案(babel下可支持)
    * require是同步导入；import属于异步导入
    * require是值拷贝，导出值变化不会影响到导入值；import指向的内存地址，导入值会随导出值而变化

#### 防抖与节流：
答：防抖与节流函数是一种最常用的高频触发优化方式，能对性能有较大的帮助
* 防抖(debounce): 将多次高频操作优化为只在最后一次执行，通常使用场景是：用户输入，只需再输入完成后做一次输入校验即可

```javascript
function debounce(fn, wait, immediate){
    let timer = null;
    return function(){
        let args = arguments;
        let context = this;
        if(immediate && !timer){
            fn.apply(context, args);
        }
        if(timer) clearTimeout(timer)
        timer = setTimeout(()=>{
            fn.apply(context, args)
        }, wait)
    }
}
```

* 节流(throttle)：每隔一段时间后执行一次，也就是降低频率，将高频操作优化成低频操作，通常使用场景：滚动条事件/resize事件，通常每隔100~500ms执行一次即可
```javascript
function throttle(fn, wait, immediate){
    let timer = null;
    let callNow = immediate;
    return function(){
        let context = this;
        let args = arguments;
        if(callNow){
            fn.apply(context, args);
            callNow = false;
        }
        if(!timer){
            timer = setTimeout(()=>{
                fn.apply(context, args);
                timer = null
            }, wait)
        }
    }
}
``` 
#### 函数执行改变this:
答：由于JS设计原理，在函数中，可以引用运行环境中的变量。因此就需要一个机制来让我们可以在函数体内部获取到当前的运行环境，这就是this
* 函数的运行环境：
    * obj.fn()：this === obj
    * fn()：this === window
* 手动修改this指向：
    * call: fn.call(target, 1, 2)
    * apply: fn.apply(target, [1, 2])
    * bind: fn.bind(target)(1, 2)

#### ES6/ES7:
* 声明
    * let/const：块级作用域、不存在变量提升、暂时性死区、不允许重复声明
    * const：声明常量、无法修改
* 解构赋值
* class/extend：类声明与继承
* Set/Map：新的数据类型
* 异步解决方案：
    * Promise的使用与实现
    * generator:
        * yield: 暂停代码
        * next(): 继续执行代码
        * await/async：generator的语法糖，babel中基于promise实现

#### AST：
答：抽象语法树(Abstract Syntax Tree)，是将代码逐字母解析成树桩对象的形式。这是语言之间的转换、代码语法检查、代码风格检查、代码格式化、代码高亮、代码错误提示、代码自动补全等等的基础

#### babel编译原理：
* babylon将ES6/ES7代码解析成AST
* babel-traverser对AST进行遍历转译，得到新的AST
* 新AST通过babel-generator转换成ES5

#### 函数柯理化：
答：在一个函数中，首先填充几个参数，然后再返回一个新的函数的技术，称为函数的柯理化。通常可用于在不侵入函数的前提下，为函数预置通用参数，供多次重复调用

#### 数组：
* map：遍历数组，返回回调返回值组成的新数组
* forEach：无法break，可以用try/catch中throw new Error来停止
* filter: 过滤
* some：有一项返回true，则整体为true
* every：有一项返回false，则整体为false
* join：通过指定连接符生成字符串
* push/pop：末尾推入和弹出，改变原数组，返回推入/弹出项
* unshift/shift：头部推入和弹出，改变原数组，返回操作项
* sort(fn)/reverse：排序与反转，改变原数组
* concat：连接数组，不影响原数组，浅拷贝
* slice(start, end)：返回截断后的新数组，不改变原数组
* splice(start, number, value...)：返回删除元素组成的数组，value为插入项，改变原数组
* indexOf/lastIndexOf(value, fromIndex)：查找数组项，返回对应的下标
* reduce/reduceRight(fb(pre, cur), defaultPrev)：两两执行，prev为上次化简函数的return值，cur为当前值(从第二项开始)
* 数组乱序：
```javascript
var arr = [1, 2, 3, 4, 5, 6];
arr.sort(function(){
    return Math.random() - 0.5;
})
```
* 数组拆解：flat:[1, [2, 3]] --> [1, 2, 3]
```javascript
Array.prototype.flat = function(){
    return this.toString().split(',').map(item => +item)
}
```

    














