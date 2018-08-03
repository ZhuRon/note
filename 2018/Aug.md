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