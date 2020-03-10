#### nextTick
答：在下一次dom更新循环结束之后执行的延迟回调，可用于获取更新后的dom状态
* 新版本中默认是microtasks，v-on中会使用macrotasks
* macrotasks任务的实现：
    * setImmediate/MessageChannel/setTimeout

#### vue中v-if和v-show的区别
* v-show: 不管条件是真还是假，第一次渲染时标签都会添加到DOM中。切换时，通过display: none; 样式来显示隐藏元素。对性能影响不是很大
* v-if: 在首次渲染的时，若条件为假，不会在页面上渲染该元素，当条件为真时，开始局部编译，动态向DOM中添加元素。当条件从真变为假时，开始局部编译，从DOM中删除元素。对性能有一定影响

#### 直接给一个数组项赋值，Vue 能检测到变化吗,为什么
答：vue中的数组的监听不是通过Object.defineProperty来实现的，是通过对'push', 'shift', 'unshift', 'splice', 'sort', 'reverse'等改变数组本身的方法来通知监听的，所以直接给数据某一项赋值无法监听到变化的，解决方案：
* 用vue的set方法改变数组或者对象
* 用改变数组本身的方法如splice, pop, shift等
* 用深拷贝,解构运算符