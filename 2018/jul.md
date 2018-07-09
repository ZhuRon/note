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
