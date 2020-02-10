JavaScript类型
==============
Number/Null/Undefined/Boolean/String/Symbol/Object

#### 为什么有的编程规范要求用 void 0 代替 undefined?
答：undefined表示未定义，而且它并不是关键字，为了避免被无意的篡改，所以建议使用void 0来获取undefined值

#### 字符串有最大长度吗？
答：有的，字符串最大长度受限于字符的编码长度

#### 0.1 + 0.2 不是等于 0.3 么？为什么 JavaScript里不是这样的？
答：不等于。浮点数运算的精度问题导致等式左右的结果并不是严格相等，而是相差了微小的值。正确的比较方法是使用JavaScript提供的最小精度值:
console.log(Math.abs(0.1+0.2-0,3)<=Number.EPSILON());

#### ES6 新加入的 Symbol 是个什么东西？
答：Symbol是ES6中引入的新类型，它是一切非字符串的对象key的集合，在ES6规范中，整个对象系统被用Symbol重塑。
Symbol可以具有字符串类型的描述，但是即使描述相同，Symbol也不相等。
##### 创建Symbol类型：
```javascript
var symbol = Symbol('my symbol')
```
#### 为什么给对象添加的方法能用在基本类型上？
答：运算符提供了装箱操作，它会根据基础类型构造一个临时对象，使得我们能在基础类型上调用对应对象的方法

#### 类型转换规则：
* StringToNumber: 字符串到数字的类型转换，存在一个语法结构，类型转换支持十进制、二进制、八进制和十六进制
*  NumberToString:
在较小的范围内，数字到字符串的转换是完全符合你直觉的十进制表示。当Number绝对值较大或较小时，字符串表示则是使用科学计数法表示的。
* 装箱转换：
把基本类型(Number/String/Boolean/Symbol)转换为对应的对象
* 拆箱转换：
在JavaScript标准中，规定了ToPrimitive函数，它是对象类型到基本类型的转换
对象到String和Number的转换会遵循"先拆箱再转换"的规则。通过拆箱转换，把对象转为基本类型，再从基本类型转为对应的String或Number
拆箱转换会尝试调用valueOf和toString来获取拆箱后的基本类型。若valueOf和ToString都不存在，或没有返回基本类型，则会产生类型错误TypeError

JavaScript对象
==============

#### JavaScript标准对给予对象定义
答：语言和宿主的基础设施由对象来提供，并且JavaScript程序即是一系列互相通讯的对象集合

#### 面向对象

#### JavaScript对象的特征
* 对象具有唯一标识性：即使两个完全相同的对象，也并非同一个对象
* 对象有状态：对象具有状态，同一对象可能处于不同状态之下
* 对象具有行为：即对象的状态，可能因为它的行为产生变迁

`JavaScript中对象独有的特色是：`对象具有高度的活跃性，因为JavaScript赋予了使用者在运行时为对象添改状态和行为的能力

#### JavaScript对象的两类属性
答：数据属性、访问器属性

##### 数据属性的特征：
* value: 属性的值
* writable: 决定属性能否被赋值
* enumerable: 决定for in能否枚举该属性
* configurable: 决定该属性能否被删除或改变特征值

##### 访问器属性的特征：
* getter: 函数或undefined，在取属性值时被调用
* setter: 函数或undefined，在设置属性值时被调用
* enumerable: 决定for in能否枚举该属性
* configurable: 决定该属性能否被删除或改变特征值

`查看数据属性：` 内置函数Object.getOwnPropertyDescripter

`改变属性特征或定义访问器属性：` 内置函数Object.defineProperty

`模拟面向对象：` 模拟基于类的面向对象 

`原型：` 顺应人类自然思维的产物

#### JavaScript的原型：
* 若所有对象都有私有字段[[prototype]]，就是对象的原型
* 读一个属性，若对象本身没有，则会继续访问对象的原型，直到原型为空或者找到为止

#### ES6访问操纵原型的方法：
* Object.create 根据指定的原型创建新对象，原型可以是null
* Object.getPrototypeOf获取一个对象的原型
* Object.setPrototypeOf设置一个对象的原型

#### 对象分类：
* 宿主对象： 由JS宿主环境提供的对象
* 内置对象： 由JS语言提供的对象

#### 内置对象：
* 固有对象： 随JS运行时创建而自动创建的对象实例
* 原生对象： 由用户通过内置构造器或者特殊语法创建的对象
* 普通对象： 由{}语法，Object构造器或Class关键字定义类创建的对象，它能够被原型继承

#### 函数对象的定义是：具有[[call]]私有字段的对象
#### 构造对象的定义是：具有私有字段[[construct]]的对象

#### JavaScript的执行




