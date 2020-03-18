#### 盒模型：
答：页面渲染时，dom元素所采用的布局模型。可通过box-sizing进行设置，根据计算宽高的区域可分为content-box(W3C标准盒模型，盒子大小 = content + border + padding + margin)、border-box(IE盒模型，盒子大小 = width(content + border + padding ) + margin)

#### BFC:
答：块级格式化上下文，是一个独立的渲染区域，让处于BFC内部的元素与外部的元素相互隔离，使内外元素的定位不会相互影响
##### 触发条件：
* float !== none 
* position !== static/relative 
* display: inline-block/table-cell/flex/table-caption/inline-flex 
* overflow !== visible
##### 作用：
* 避免margin重叠   
* 自适应两栏布局 
* 清除浮动 
##### 规则： 
* 属于同一个BFC的两个相邻Box垂直排列 
* 属于同一个BFC的两个相邻Box的margin发生重叠
* BFC的区域不会与float元素区域重叠 
* 计算BFC高度时，浮动子元素也参与计算 
* 文字层不会被浮动层覆盖，环绕于周围

#### 层叠上下文：
答：元素提升为一个比较特殊的图层，在三维空间中(Z轴)高出普通元素一等
##### 触发条件： 
* 根层叠上下文(html) 
* position 
* CSS3属性(flex/transform/opacity/filter/will-change/-webkit-overflow-scrolling)
##### 层叠等级：
答：background/border < z-index为负值 < 块级元素 < 浮动元素 < 行内元素 < z-index:0/auto < z-index为正值

#### 居中布局：
##### 水平居中: 
* 行内元素(text-align: center) 
* 块级元素(margin: 0 auto) 
* absoulte: absoulte + left: 50% + transform: translateX(-50%) 
* display: flex + justify-content: center
##### 垂直居中: 
* line-height: height 
* position: absolute + top: 50% + transform: translateY(-50%) 
* display： flex + align-items: center 
* table
##### 水平垂直居中： 
* position: absoulte + top: 50% + left: 50% + transform: translate(-50%, -50%) 
* dislpay: flex + justify-centent: center + align-items: center

#### 选择器优先级：
答：!important > 内联样式 > ID选择器 > 类选择器 = 伪类选择器 = 属性选择器 > 元素选择器 > 通配选择器

#### 清除浮动影响，防止父级高度塌陷
* 通过增加尾元素清除浮动(:after/br/clear:both) 
* 创建父级BFC 
* 父级设置高度

#### link&@import的区别
* link功能较多，可定义RSS/Rel等作用，而@import只能加载css 
* 当解析到link时，页面会同步加载所引的css，而@import所引用的css会等到页面加载完才被加载 
* @import需要IE5以上才能使用 
* link可使用js动态引入，@import不行

#### 如何实现高度自适应
* 使用绝对定位，设置top，bottom属性
* 使用flex布局
* float + height: 100%

#### base64为什么能提升性能以及它的缺点是什么 
* 优点：
    * 无额外请求
    * 适用于很小或者很简单的图片
    * 可像单独图片一样使用，如背景图等
    * 没有跨域问题，不需要考虑缓存、文件头或者cookie问题
* 缺点：
    * CSS文件体积的增大，造成CRP(关键渲染路径)阻塞
    * 页面解析CSS生成的CSSOM时间增加