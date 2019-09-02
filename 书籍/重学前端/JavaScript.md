#### JavaScript类型
答：Number/Null/Undefined/Boolean/String/Symbol/Object

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

