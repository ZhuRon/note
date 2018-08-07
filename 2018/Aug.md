# 8.1
babel-plugin-transform-react-jsx 插件，可以将jsx翻译成jsonObject
# 8.2
umi 极快 内置了react-router react，以约定代替简化代码，pages/组件即路由
PureComponent：纯组件 没有数据，单纯的做界面输出
函数组件：（）=>(<div>jsx</div>) React.createElement
根据实际情况来使用
layout 负责头部和tabbar umi约定所有页面都会默认引入layout下index.js
layout 业务
navigator.geolocation.getCurrentPosition() lbs 位置定位
vue react 都支持proxy代理
# 8.3
react源码分析
jsx（react-jsx-plugin）->vnode(createElement)->DOM(render)

将虚拟DOM变成真实DOM @params vnode 虚拟DOM，@return 返回DOM
用递归将节点转成DOM，子节点递归。出口就是文本节点
节点类型 3种情况 
文本节点：return createTextNode() 如果有递归也会结束 
标签节点：createElement attr children设置（递归_render）
Component(组件节点) render(return jsx)

响应式setState() 为了达到DOM的更新，将整个DOM片段都替换掉了。
html树更新需要重绘，DOM开销是一般计算开销的100-1000倍
replaceChild 就是重绘
重排：数据顺序发生改变需要重新排列
React DOM diff 算法
核心就是减少DOM操作
setState 对应的DOM部分： setState之后返回一个新的vnode->跟旧的DOM对比，将新的内存（虚拟）DOM，可以跟旧的DOM对比
因为都是树状结构，采用算法就可以比较出差异点，在不同的地方进行真实DOM的操作
# 8.7
node --expose-gc 进入内存
WeakMap，弱引用，对象赋值，相比map，不会造成key=null时内存不清除
前后端都有路由概念
前端路由根据hash实现单页应用，提供组件，走向组件组装 mvvm
后端路由提供服务器端资源的暴露，走向服务器资源获取 mvc
中间件 是一个数组 middlewares 从上到下，用一组中间件（函数）来为用户提供服务
next（） 转交控制权 res.end()结束此次服务
session 会话 一般放在内存里，但是为了避免大规模访问，所以放在mongodb这种数据库里面
## express
koa express
都是node的server frame 
koa egg 用async-await来打理异步请求

单点入口
app的实例化，listen router分发服务器资源
MVC model view controller
router -> controller
controller -> view
view post|get -> controller ->model
/login
- controller login.js
  - login.ejs
  - form
    -controller
    login.js
    -
    models/login // 模型的抽象
    js save
静态服务器
public/
分布式的服务，不止一台服务器 负载均衡
