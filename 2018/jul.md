# 7.4
一像素问题解决
border-1px($color)
  position: relative
  &:after
    display: block
    position: absolute
    left: 0
    bottom: 0
    width: 100%
    border-top: 1px solid $color
    content: ' '

border-none()
  &:after
    display: none

五颗星评分
<template>
  <div class="star" :class="starType">
    <span v-for="(itemClass,index) in itemClasses" :class="itemClass" class="star-item" key="index"></span>
  </div>
</template>

<script>
  const LENGTH = 5;
  const CLS_ON = 'on';
  const CLS_HALF = 'half';
  const CLS_OFF = 'off';
  export default {
    props: {
      size: {
        type: Number
      },
      score: {
        type: Number
      }
    },
    computed: {
      starType() {
        return 'star-' + this.size;
      },
      itemClasses() {
        let result = [];
        let score = Math.floor(this.score * 2) / 2;
        let hasDecimal = score % 1 !== 0;
        let integer = Math.floor(score);
        for (let i = 0; i < integer; i++) {
          result.push(CLS_ON);
        }
        if (hasDecimal) {
          result.push(CLS_HALF);
        }
        while (result.length < LENGTH) {
          result.push(CLS_OFF);
        }
        return result;
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"
  .star
    font-size: 0
    .star-item
      display: inline-block
      background-repeat: no-repeat
    &.star-48
      .star-item
        width: 20px
        height: 20px
        margin-right: 22px
        background-size: 20px 20px
        &:last-child
          margin-right: 0
        &.on
          bg-image('star48_on')
        &.half
          bg-image('star48_half')
        &.off
          bg-image('star48_off')
    &.star-36
      .star-item
        width: 15px
        height: 15px
        margin-right: 6px
        background-size: 15px 15px
        &:last-child
          margin-right: 0
        &.on
          bg-image('star36_on')
        &.half
          bg-image('star36_half')
        &.off
          bg-image('star36_off')
    &.star-24
      .star-item
        width: 10px
        height: 10px
        margin-right: 3px
        background-size: 10px 10px
        &:last-child
          margin-right: 0
        &.on
          bg-image('star24_on')
        &.half
          bg-image('star24_half')
        &.off
          bg-image('star24_off')
</style>


# 7.6
vue设计
vue-router 设置路由
选择rem或者em进行适配
(function(doc,win){
    var docEl = doc.documentElement,
    resizeEvt = 'orientationchange' in window? 'orientationchange':'resize',
    recalc = function(){
        var clientWidth = docEl.clientWidth;
        if(!clientWidth) return;
        console.log(clientWidth)
        docEl.style.fontSize = 20*(clientWidth/320)+'px';
    };
    if(!doc.addEventListener) return;
    win.addEventListener(resizeEvt,recalc,false);
    doc.addEventListener('DOMContentLoaded',recalc,false);

    
})(document,window)

yarn add stylus stylus-loader -D stylus安装，在开发阶段安装，-dev

懒加载 lazyload 
const home = ()=>import('../page/home.vue')
用一个函数把页面封装起来，

slot :扩展组件

wh($width,$height)


vuex:
一个项目中只有一颗单一状态树

lbs
location base servers 在可送范围半径内把显示出来
mutation-types 说明清单

computed 是一个json
mapstate 会借一个state
...mapstate 将新的state json展开到computed的json里面去

ct()
    position absolute
    top 50%
    transform translateY(-50%)
    相对于父元素决定定位在正中间
    获取城市位置不要用生命周期，不准确耗时
    而用created 有时候会阻塞组件渲染

# 7.7
api文档的书写

navigationBar的封装
提供history title 居中 右边的buttons
singnUP 显示是否登录

<section class="head_goback" @click="$router.go(-1)" v-if="goBack">返回</section>

用history返回上一界面
绑一个钩子，然后传入子组件 props里面，用v-if判断是否渲染

盒子在父容器里面绝对居中
center()
    position absolute
    top 50%
    left 50% 
    transform translate(-50%,-50%)

验证码：

异步是不可回避的问题：callback promise 先用thenable 然后用async

动态路由：      path:'/city/:cityid',component:city
fetch 兼容性 api比较原始

# 7.9

前端工作流
- babel js预编译器
- npm  npm run dev   npm install  项目构建的基本流程
- postcss 解决前缀问题 css 变量
- stlus/scss/less
使用最新的js语法来编写，运行的代码可以根据需求编译程相应的版本
{"presets": ["env"]} 将es6 转成 es5 env：根据环境进行自我处理
babel 的工作原理
babel-sore（babel转译的核心）
babel-cli(通过命令行对js代码进行转译)
https://www.jianshu.com/p/e9b94b2d52e2

babel 编译js
source_code .babelrc 通过 cli 到 targets(运行平台)
依赖于presets（预处理集)
babel的预处理只是语法糖 class 没有 把es5里面没有的es6的语法实现一遍，最基本的const之流就在babel-core李
还有一些没有的Object.assign(),promise,async await 这种es6最新语法或者概念，babel里面没有
所以用一种新的做法去做，引入新的插件，plugins
最新的插件就是：transform-runtime

# 7.10
mocha
https://cnodejs.org/topic/59e3873520a1a3647d72ac39

isNaN() 判断非数字
因为js是弱类型语言，所以会做隐形类型转换，比如true false 会认为是1,0所以会报false
而'12'也会被转换所以也是false  
数学计算时，js 会去做强制类型转换
1 + '2' isNaN  3？
''更优先 字符串拼接的优先级大于加法

骨架

scoped原理
PostCSS给一个组件中的所有dom添加了一个独一无二的动态属性，然后，给CSS选择器额外添加一个对应的属性选择器来选择该组件中dom，这种做法使得样式只作用于含有该属性的dom——组件内部dom。

虚拟节点，从mvvm的数据改变到界面更新是一个异步操作，因为要经过vnode（用js语法描述一个节点），从而产生一个新的节点，去更新dom节点，然后把dom节点和原来的dom节点进行对面，更新没有的东西。所以性能高
在vue里面，有没有一种语法让我们等待这个过程结束，数据改变完了界面也更新完了



双向绑定：vue采用的是发布-订阅者模式加数据劫持。通过Object.defineProperty()进行数据劫持，为了实现mvvm，需要一个Observer，负责监听数据的变化，一个
eventbus：
nexttick：因为vue
vuex：

# 7.11
webpack
把src里面的文件打包到dist目录下面
webpack 是一个打包（build）工具，
常规的落后的开发方式，jQuery，html，css交给后端上线
mvvvm 开发时代，一切皆可打包

webpack将现代js开发中的各种新鲜技术，集合打包，打包前无法运行（js，es6 module，stylus不支持浏览器直接运行，.hbs 模板编译,.vue)
在目标容器上运行
一切静态资源 =>打包 目标项目
path.resolve(__dirname,'dist')
找到绝对路径然后把在该路径下建立dist文件夹

$正则表达式里面表示匹配结束

const ExtractTextPlugin = require('extract-text-webpack-plugin')
引入插件，将打包好的js里面的css抽离出来
html-webpack-plugin将模板相应的头部和尾部融合进生成js和css代码
lodash 作为工具，是很多组建会使用的，省去了到处import
    new CopyWebpackPlugin.ProvidePlugin({
      '_':'lodash'
    })

# 7.13
eventbus
能够将兄弟组件之间的事件进行简单处理并进行传递，其实就是一个发布订阅者模式的vue实现
事件会沿着bus进行查找，有没有谁订阅了这个事件
专属npm包：vue-event-proxy 事件代理器

watch的深入使用
监听所有想监听的东西，watch（）
https://www.imooc.com/article/28187

# 7.14
action要去做数据请求，
设计稿 psd用来取图
产品原型设计稿 可以再pc和手机上的预览图
跟接口的一些设计及沟通

# EventBus
能够将兄弟组件之间的事件进行简单处理并进行传递，其实就是一个发布订阅者模式的vue实现
同一个事件有组件订阅，当发布这个事件的时候订阅组件得到相应，摆脱了兄弟组件需要父组件进行传达的语法复杂的问题。
除此之外，还可以用vuex，通过引入数据流概念解决。在订阅者和发布者之间都引用eventbus，其实就是vue的实例，都是由一个eventbus对他们进行服务，当事件发生，专车就会把消息通知订阅者，Vue实例对象是具有emit和on这两个api的。由同一个对象在不同组件之间都进行斡旋、
# 7.23
'postcss-loader' css前缀兼容性问题
devtool: 'inline-source-map' 解决调试代码挤在一行的问题
yarn add babel-core babel-loader babel-preset-env babel-preset-react -D 自行搭建react相关的东西
yarn add react react-dom
一张图片，如果命名相同，但是图片内容改了，就要在[name]后面加上[hash:8].[ext]
# 7.24
js 请求有一个同源机制
后端解决跨域问题 koa-cors
前端解决方案 jsonp
利用了script标签可以访问外部跨域脚本或地址
改造一下后端接口，让它实现jsonp json with padding
返回的数据，data封装一下callback（data）
  const callback = ctx.query.callback;
  if(callback){
     ctx.body ='callback(' + JSON.stringify(data)+')';
  }else{
    ctx.body = data;
  }

})
yarn add rewire 对webpack进行重新设置 proxyquire
react-router-dom 把路由对应的东西挂载到页面上去
# 7.25
Object.assign 添加数据
albumList.sort((a,b)=>{return new Date(b.public_time).getTime()-new Date(b.public_time).getTime()}
把json数据进行string转换，然后冒泡排序
react 的modul层，把数据进行处理，然后统一格式输出需要的数据
better-scroll 最好的滚动插件

# 7.25
redux 
store 单一状态树
redux state,actions,没有直接的map,提出一个需求，将组建分成两部分，原来的ui组建部分保留，新增一个container的容器，redux 将数据给container，container再将数据给component