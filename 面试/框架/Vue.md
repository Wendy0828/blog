#### nextTick
答：在下一次dom更新循环结束之后执行的延迟回调，在修改时数据之后立即使用这个方法，可获取更新后的dom
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

#### 页面中定义一个定时器，在哪个阶段清除？
答：beforeDestory中销毁定时器

#### 父组件如何获取子组件的数据，子组件如何获取父组件的数据，父子组件如何传值？
* 父组件获取子组件的数据: $children / $refs
* 子组件获取父组件的数组: $parent 
* 其他父子组件通信有：
    * props
    * emit
    * inheritAttrs：控制子组件html上是否显示父组件的提供的属性
        * PS：当父子组件中属性冲突时，默认采用父组件，若想采用子组件，则需将inheritAtts: false
    * atts：获取到没有使用的注册属性，也可以向下传递
    * provide/inject也适用于隔代组件通信

#### 自定义指令如何定义，它的生命周期是什么？
答：通过Vue.directive定义全局指令
* 声明周期(可用钩子)：
    * bind: 指令附加到元素时触发
    * inserted: 元素被添加到父元素时触发
    * updated: 元素本身更新时触发
    * componentUpdated: 组件和子组件被更新时触发
    * unbind：指令移除时触发

#### vue 生命周期，各个阶段简单讲一下？
* beforeCreate(): 实例创建前，该阶段实例的data和methods读取不到
* created()：实例创建后，该阶段完成了实例的数据监测、属性和方法的调用
    * watch/event：事件回调
    * 数据不渲染到DOM上
* beforeMount(): 实例挂载前，render函数首次被调用
    * template编译成render函数，有render函数才有beforeMount()
* mounted()：实例挂载后，数据渲染到DOM上
* beforeUpdate/updated：数据更新，先调用beforeUpdate，虚拟DOM渲染，再调用updated
* beforeDestroy/destroy: 数据销毁，先调用beforeDestroy，再调用destroyed

#### watch 和 computed 的区别？
* watch: 可接受两个参数、监听时可触发回调，并执行一些事情、允许异步、监听的属性必须存在
    * watch配置：handler/deep(是否深度)/immeditate(是否立即执行)
* computed：不能有参数、有缓存机制、可以依赖于其他computed，甚至其他组件的data、不能与data属性重复
* 总结：
    * 当有一些数据需要随着另一些数据变化时，建议使用computed
    * 当有一个通用的响应数据变化时，要执行一些业务逻辑或异步操作时建议使用watch

#### 请说一下 computed 中的 getter 和 setter
* computed可以分成getter(读取)和setter(设值)
* 一般情况下没有setter，computed预设只有getter，也就是说只能读取值，不能改变设值

#### 导航钩子有哪几种，分别如何用，如何将数据传入下一个点击的路由页面？
* 导航钩子
    * 全局导航守卫
        * 前置导航守卫
        ```javascript
        router.berforeEach((to, from, next) => {
            // do someting
        )}
        ```
        * 后置钩子
        ```javascript
        router.afterEach((to, from) => {
            // do someting
        })
        ```
    * 路由独享守卫
        ```javascript
        cont router = new  VueRouter({
        routes: [
        {
            path: '/file',
            component: File,
            beforeEnter: (to, from ,next) => {
            // do someting
            }
        }
        ]
        });
        ```
    * 组件内的导航钩子：直接在组件内部进行定义
        * beforeRouterEnter
        * beforeRouterUpdate
        * beforeRouterLeave
* 通过路由将数据传入下一个跳转的页面
    * params
    ```javascript
    //传参
    this.$router.push({
    name:"detail",
    params:{
    name:'xiaoming',
    }
    });
    //接收
    this.$route.params.name
    ```
    * query
    ```javascript
    //传参
    this.$router.push({
    path:'/detail',
    query:{
        name:"xiaoming"
    }
    })
    //接收 //接收参数是this.$route
    this.$route.query.id
    ```
    * params && query对比
        * params只能用name来引入路由；query除了用name外，还可以使用path
        * params相当于post方法，参数不会在URL显示；query相当于get方法，参数再URL可见
    * PS: router为Vue Router实例，想导航到其他URL，需要使用router.push()；$route为当前router跳转对象，里面可以获取到name，path，query，params等

#### vue 双向绑定原理？
答：通过Object.defineProperty()来劫持各个属性的getter/setter，数据变动时发送消息给订阅者，触发相应的监听回调

#### vue-router 的实现原理，history 和 hash 模式有什么区别？
答：vue-router有两种模式，hash模式和history模式
* hash模式：url带#的，#后面是hash值，它的变化会触发hashchange事件
* history模式：
    * 切换历史状态：back/forward/go
    * 修改历史状态：pushState/replaceState

#### 怎么在vue中点击别的区域输入框不会失去焦点？
答：阻止事件的默认行为。具体操作：监听你想点击后不会丢失input焦点的那个元素的mousedown事件，回调里面调用event.preventDefault()，会阻止使当前焦点丢失这一默认行为

#### vue中data的属性可以和methods中的方法同名吗？为什么？
答：不可以，因为Vue会把data和methods全部代理到Vue生成的对象中，产生覆盖

#### 怎么给vue定义全局的方法？
答：vue.prototype.方法名

#### Vue 2.0 不再支持在 v-html 中使用过滤器怎么办？
* 全局方法
```javascript
Vue.prototype.msg = function（msg）{
  return msg.replace（"\n"，"<br>"）
 }
 <div v-html="msg(content)"></div>
```
* computed
```javascript
computed：{
 content：function(msg){
  return msg.replace("\n"，"<br>")
 }
}
<div>{{content}}</div>
```
* $options.filter
```javascript
filters：{
 msg：function(msg){
  return msg.replace(/\n/g，"<br>")
 }
}，  　　
data：{
 content："XXXX"
}
<div v-html="$options.filters.msg(content)"></div>
```

#### 怎么解决vue打包后静态资源图片失效的问题？
答：将静态资源的存放位置放在src目录下

#### 怎么解决vue动态设置img的src不生效的问题？
答：require

#### 跟keep-alive有关的生命周期是哪些？描述下这些生命周期
答：activated/deactivated
* activated: 当组件激活时，钩子触发顺序created -> mounted -> activated
* deactivated: 组件停用触发，当再次前进或后退时触发activated

#### vue中怎么重置data？
答：Object.assign()，用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。
<br>
首先，this.$data获取到当前状态下的data，再通过this.$options.data()获取到该组件初始状态下的data，最后使用Object.assign(this.$data, this.$options.data)就可以将当前状态的data重置到初始状态

##### vue怎么实现强制刷新组件？
* v-if
* this.$forceUpdate

#### vue如何优化首页的加载速度？
* CDN
* vue-router路由懒加载
* 压缩图片资源
* 静态文件本地缓存
* 服务端SSR渲染

#### vue能监听到数组变化的方法有哪些？为什么这些方法能监听到呢？
* 监听数组变化的方法：push/pop/shift/unshift/splice/reverse/sort
* 原因：通过Object.defineProperty()劫持数组的getter/setter后，调用数组的方法改变元素时并不会触发setter，继而数组的数据的变化不是响应式的，但vue实际开发中实时响应的，是因为vue重写了数组的方法

#### 说说你对proxy的理解？
答：proxy用于修改某些操作的默认行为。可以理解为在目标对象之前设置拦截，外部所有的访问都必须要通过这层拦截，因此可以对外部访问进行过滤和修改

#### 怎么缓存当前的组件？缓存后怎么更新？
答：keep-alive 调用activated

#### axios怎么解决跨域的问题？
答：配置代理，因为客户端请求服务器会存在跨域的问题，而服务器与服务器之间不存在跨域问题，所以我们需要配置一个代理服务器可以请求另一个服务器的数据，并将请求的数据返回到代理服务器，然后代理服务器再返回到客户端。
* 操作：配置baseUrl、配置代理(proxyTabel拦截/api，并把/api及其前面的所有替换成目标中的内容)

#### 怎么实现路由懒加载呢？
* vue异步组件技术(异步加载)，vue-router配置路由 , 使用vue的异步组件技术 , 可以实现按需加载 .但是,这种情况下一个组件生成一个js文件
* 路由懒加载(使用import)
* 按模块划分懒加载

#### 怎样动态加载路由？
* 在Vue-Router对象中初始化公共的路由，如首页、404、登录等
* 用户登录后，拿到对应的菜单信息，将菜单信息转成我们需要的router数据格式
* 通过router.addRouter(routers)方法，同时将转后的菜单信息保存在vuex中，我们可以在侧边栏组件中获取到全部的路由信息，并渲染到侧边栏

#### vue-router如何响应路由参数的变化？
* watch监测
* beforRouterUpdate

#### vue模板中为什么以_、$开始的变量无法渲染？
答：名字以_、$开始的属性不会被Vue实例代理，因为它可能与vue内置的属性或api方法冲突。可用vm._property访问

#### v-for循环时为什么要加key？
答：key的作用是为了高效的更新虚拟DOM

#### vuex是什么？怎么使用？哪种功能场景使用它？
答：vuex是vue框架中的状态管理，在main.js中引入store，注入
场景：单页应用中，组件之间的状态、音乐播放、登录状态、加入购物车

#### vuex有哪几种属性？
* state：基本数据
* getters: 由基本数据派生出来的数据
* mutations：提交更新数据的方法，同步
* action: 像一个装饰器，包裹mutations，使之异步
* module：vuex模块化

#### vue的两个核心点
* 数据驱动: ViewModel 保证数据和视图的一致性
* 组件系统：应用类UI可以看作全部是组件数构成的

#### mvvm 框架是什么？
答：mvvm框架是双向数据绑定，当视图层发生更新模型层，当模型层发生改变更新视图层，vue实现了双向数据绑定技术，即当View改变时更新Model，但Model改变时更新View