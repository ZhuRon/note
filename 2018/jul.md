#7.4
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


#7.6
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
