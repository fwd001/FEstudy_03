# 常见的问题

## 1.HTML5 CSS3的新特性
### HTML5的新特性：
1. 用于绘画 canvas 元素。
2. 用于媒介回放的 video 和 audio 元素。
3. 本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失；sessionStorage 的数据在浏览器关闭后自动删除。
4. 语意化更好的内容元素，比如 article、footer、header、nav、section。
5. 表单控件，calendar、date、time、email、url、search。

### CSS3新特性：
1. 选择器。
2. 和透明度。
3. 多栏布局。
4. 多背景图。
5. Word Wrap。
6. 文字阴影。
7. @font-face属性。
8. 圆角(边框半径)。
9. 边框图片。
10. 盒阴影。
11. 盒子大小。
12. 媒体查询。
13. 语音。

## 2.vue的双向绑定原理
- 首先我们为每个vue属性用Object.defineProperty()实现数据劫持，为每个属性分配一个订阅者集合的管理数组dep；然后在编译的时候在该属性的数组dep中添加订阅者，v-model会添加一个订阅者，{{}}也会，v-bind也会，只要用到该属性的指令理论上都会，接着为input会添加监听事件，修改值就会为该属性赋值，触发该属性的set方法，在set方法内通知订阅者数组dep，订阅者数组循环调用各订阅者的update方法更新视图。
- [详情](https://www.cnblogs.com/zhenfei-jiang/p/7542900.html)

## 3.JavaScript如何实践多线程
- 假如我们要执行一些耗时的操作，比如加载一张很大的图片，我们可能需要一个进度条来让用户进行等待，在等待的过程中，整个js线程会被阻塞，后面的代码不能正常运行，这可能大大的降低用户体验，这时候我们就期望拥有一个工作线程来处理这些耗时的操作。在传统的html时代是基本不可能实现的，而现在，我们拥有一种叫做worker的东西。它是js里的一个类，而我们只需要创建它的实例就可以使用它。

- `var worker = new Worker(js file path);`


## 4.前端开发的优化问题()
1. 减少 http 请求次数:CSS Sprites, JS、CSS 源码压缩、图片大小控制合适;网页 Gzip，CDN 托 管，data 缓存 ，图片服务器。
2. 前端模板 JS+数据，减少由于 HTML 标签导致的带宽浪费，前端用变量保存 AJAX 请求结 果，每次操作本地变量，不用请求，减少请求次数
3. 用 innerHTML 代替 DOM 操作，减少 DOM 操作次数，优化 javascript 性能。 
4. 当需要设置的样式很多时设置 className 而不是直接操作 style。
5. 少用全局变量、缓存 DOM 节点查找的结果。减少 IO 读取操作。
6. 避免使用 CSS Expression(css 表达式)又称 Dynamic properties(动态属性)。 
7. 图片预加载，将样式表放在顶部，将脚本放在底部 加上时间戳。
8. 避免在页面的主体布局中使用 table，table 要等其中的内容完全下载之后才会显示出来， 显示比 div+css 布局慢。

## 5.网络七层协议
- 应用层 表示层 会话层 传输层 网络层 数据链路层 物理层

[详细协议](https://www.cnblogs.com/ranyonsue/p/5984001.html)

### http请求过程
- 按下「g」键
- 回车键按下
- 产生中断（非 USB 键盘）
- (Windows) 一个 WM_KEYDOWN 消息被发往应用程序
- (Mac OS X) 一个 KeyDown NSEvent被发往应用程序
- (GNU/Linux)Xorg 服务器监听键码值
- 解析 URL
- 输入的是 URL 还是搜索的关键字？
- 转换非 ASCII 的 Unicode 字符
- 检查 HSTS 列表
- DNS 查询
- ARP 过程
- 使用套接字
- TLS 握手
- HTTP 协议
- HTTP 服务器请求处理
- 浏览器背后的故事
- 浏览器
- HTML 解析
- CSS 解析
- 页面渲染
- GPU 渲染
- Window Server
- 后期渲染与用户引发的处理

## 6.Get请求和Post请求的区别：
1. 参数传递方式不同, 使用Get请求时,参数在URL中显示,而使用Post方式,则不会显示出来
2. 使用Get请求发送数据量小,Post请求发送数据量大
3. 在原生Ajax查询中，post请求必须设置Content-Type值为application/x-form-www-urlencoded，并且参数在send方法中传送

## 7.vue性能优化
1. v-show，v-if 用哪个？

  - 在我来看要分两个维度去思考问题：

    + 第一个维度是权限问题，只要涉及到权限相关的展示无疑要用 v-if，

    + 第二个维度在没有权限限制下根据用户点击的频次选择，频繁切换的使用 v-show，不频繁切换的使用 v-if，

    + 这里要说的优化点在于减少页面中 dom 总数，我比较倾向于使用 v-if，因为减少了 dom 数量，加快首屏渲染，至于性能方面我感觉肉眼看不出来切换的渲染过程，也不会影响用户的体验。

2. 不要在模板里面写过多的表达式与判断

  - v-if="isShow && isAdmin && (a || b)"，这种表达式虽说可以识别，但是不是长久之计，当看着不舒服时，

  - 适当的写到 methods 和 computed 里面封装成一个方法，这样的好处是方便我们在多处判断相同的表达式，其他权限相同的元素再判断展示的时候调用同一个方法即可。

3. 循环调用子组件时添加 key

  - key 可以唯一标识一个循环个体，可以使用例如 item.id 作为 key，

  - 假如数组数据是这样的 ['a' , 'b', 'c', 'a'],使用 :key="item" 显然没有意义，更好的办法就是在循环的时候 (item, index) in arr，然后 :key="index"来确保 key 的唯一性
 
  - 当 Vue.js 用v-for 正在更新已渲染过的元素列表时，它默认用“就地复用”策略。如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序， 而是简单复用此处每个元素，并且确保它在特定索引下显示已被渲染过的每个元素。为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 key 属性。理想的 key 值是每项都有的且唯一的 id。这个特殊的属性相当于 Vue 1.x 的 track-by ，但它的工作方式类似于一个属性，所以你需要用 v-bind 来绑定动态值 (在这里使用简写)：

4. 对路由组件进行懒加载

  - 这里的懒加载是指在访问到对应的组件时才加载它，首屏的时候不加载。这里实现的方法很简单，只要将以前直接import组件的方式改为：

  - `const Login = () => import('@/pages/Login’)`;即可。

## 8.SPA（单页面应用）的简单实现

  - 一是处理#后面的字符， 
  - 二是局部刷新。 
  - [详情](https://blog.csdn.net/u011032902/article/details/54730739?utm_source=itdadao&utm_medium=referral) 

