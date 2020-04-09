#### ES6新特性:
* const和let：let声明的变量和const声明的常量，两个都有块级作用域，ES5中是没有块级作用域的，并且var有变量提升，使用let变量一定要进行声明
* 模板字符串：增强版的字符串，用反引号(`)标识，可以当做普通字符串使用，也可以用来定义多行字符串
* 箭头函数：箭头函数就是函数的一种简写形式，使用括号包裹参数，跟随一个=>，紧接着是函数体
    * 特点：1. 不需要function关键字来创建函数; 2. 省略return关键字; 3. 继承当前上下文的this关键字
<br>

` 当函数有且仅有一个参数时，可省略掉括号；当函数返回有且仅有一个表达式时可省略{}和return `
* Spread / Rest 操作符：指的是...展开符，当被用于迭代器中时，它是一个Spread操作符；当被用于函数传参时，是一个Rest操作符
* 二进制和八进制字面量：通过在数字前面添加0o或0O即可将其转为八进制值,二进制使用0b或者0B
* 解构赋值：允许按照一定的模式，从数组和对象中提取值，对变量进行赋值
* for..of循环：遍历数组、Set和Map结构、某些类似数组的对象、以及字符串等
* Modules(模块, 如import, export)：将JS代码分隔成不同功能的小块进行模块化，将不同功能的代码分别写在不同的文件中，各模块只需导出公共接口的部分，然后通过模块的导入就可以在其他地方使用
* Set()数据结构：类似数组，所有的数据都是唯一的，没有重复值。它本身就是一个构造函数
* 修饰器@decorator：一个函数，用来修改类甚至方法的行为，修饰器本质就是编译时执行的函数
* ES6中的类(class)：不再像ES5一样使用原型链实现继承，而是引入Class这个概念
* async/await：搭配promise，可以通过编写形式同步的代码来处理异步流程，提高代码的简洁性和可读性，async用于声明一个function是异步的，而await用于等待一个异步方法执行完成
* Promise：异步编程的一种解决方案，比传统的解决方案(回调函数和事件)更合理、强大
* Symbol：一种基本类型。Symbol通过调用symbol函数产生，它接受一个可选的名字参数，该函数返回的symbol是唯一的
* Proxy代理：使用代理监听对象的操作，然后可以做一些相应的事情

#### var/let/const之间的区别
* var声明的变量可重复声明，let不可以重复声明
* var不受限于块级作用域，而let受限于块级作用域
* var存在变量提升，而let有暂存死区

#### 使用箭头函数应注意什么？
* this就不是指向window，而是父级(指向是可变的)
* 不能使用参数对象
* 不能用作构造函数，也就是说不能够使用new命令，否则会抛出一个错误
* 不能使用yield命令，因此箭头函数不能用作Generator函数

#### ES6的模板字符串有哪些新特性？并实现一个类模板字符串的功能
答：基本的字符串格式化。将表达式嵌入字符串中进行拼接。用${}来界定。在ES5中，通过反斜杠(\)和加号(+)进行拼接，ES6中，通过反引号(`)进行拼接
```javascript
let name = 'Wendy';
let age = 24;
console.log(`${name}今年${age}岁了`)
```
#### 介绍下Set、Map的区别
答：Set用于数据重组，Map用于数据存储
##### Set
* 成员不能重复
* 键值没有键名，类似于数组(3)可以遍历，方法有add, delete, has
##### Map
* 本质上是键值对的集合，类似集合
* 可以遍历，可以跟各种数据格式转换

#### ECMAScript 6怎么写calss，为何会出现class
答：ES6中的class可以看成一个语法糖，它的大部分功能ES5都能实现。新的class写法只是让对象原型的写法更清晰，更像面向对象编程的语法
```javascript
//定义类
class Person {
    constructor(x, y){
        //构造方法
        this.x = x;
        this.y = y;
    }
    
    toString(){
        return '(' + this.x + ',' + this.y + ')';
    }
}
```

#### Promise构造函数时同步执行还是异步执行，那么then方法呢
答：同步执行的，then方法是异步执行的

#### setTimeout、Promise、Async/Await的区别
答：事件循环中分为宏任务和微任务，其中setTimeout的回调函数放到宏任务队列里，等到执行栈清空后执行；promise.then里的回调函数会放到相应的宏任务的微任务队列里，等宏任务里面的同步代码执行完再执行；async函数表示函数里面可能有异步方法，await后面跟一个表达式；async方法执行时，遇到await会立即执行表达式，然后把表达式后面的代码放到微任务队列里，让出执行栈让同步代码先执行

#### promise有几种状态，什么时候会进入catch
* 三个状态：pending（进行中）、fulfilled（已成功）和rejected（已失败）
* 两个过程：pending -> fulfilled、pending -> rejected
当pending为reject时，会进入catch

#### Promise中reject和catch处理上有什么区别
* reject是用来抛出异常的，catch是用来处理异常的
* reject是Promise的方法，catch是Promise实例的方法
* reject后的东西，一定会进入then中的第二个回调，如果then中没有写第二个回调，则进入catch
* 网络异常(比如断网)，会直接进入catch而不会进入到then的第二个回调

#### 使用结构赋值，实现两个变量的值的交换
```javascript
let a = 1;
let b = 2;
[a, b] = [b, a];
```

#### 如何使用Set去重
```javascript
let arr = [1,2,3,4,2,4,6,7,8];
let item = [...new Set(arr)];
console.log(item);
```

#### forEach、for in、for of 三者区别
* forEach 用来遍历数组
* for in 用来遍历对象或者json
* for of 数组对象都可以遍历，遍历对象需要通过和Object.keys()
* for in 循环出的是key，for of循环的是value

#### 取数组的最大值（ES5、ES6）
```javascript
//es5
Math.max.apply(null, arr);
//es6
Math.max(...arr);
```

#### Promise和Callback有什么区别
答：相比于Callback，Promise具有更易读的代码组织形式(链式结构调用)，更好的异步处理方式(在调用Promise的末尾添加上一个catch方法捕获异常即可)，以及异步操作并行处理的能力。CallBack最大的问题就是我们通常说的回调地域，一旦业务逻辑复杂了，我们不得不使用大量的嵌套回调代码，可维护性很低

#### ES6中的map和原生的对象有什么区别
答：Object和Map存储的都是键值对组合。区别：
* Object键的类型是字符串; Map键的类型可以是任意类型
* Object获取键值使用Object.keys，返回数组; Map获取键值使用map变量.keys()，返回迭代器

#### ES6中let块作用域是怎么实现的
答：可以通过闭包自执行函数实现块作用域

#### 操作数组常用的方法
* ES5：concat 、join 、push、pop、shift、unshift、slice、splice、substring 和 substr 、sort、 reverse、indexOf 和 lastIndexOf 、every、some、filter、map、forEach、reduce
* ES6：find、findIndex、fill、copyWithin、Array.from、Array.of、entries、values、key、includes

