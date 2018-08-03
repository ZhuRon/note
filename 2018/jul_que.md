vue-router 和 vue-route 的区别
$route为当前router跳转对象里面可以获取name、path、query、params等
$router为VueRouter实例，想要导航到不同URL，则使用$router.push方法

params、query的区别
params：/router1/:id ，/router1/123，/router1/789 ,这里的id叫做params
query：/router1?id=123 ,/router1?id=456 ,这里的id叫做query。
query更加类似于我们ajax中get传参，params则类似于post，说的再简单一点，前者在浏览器地址栏中显示参数，后者则不显示

周期函数
https://segmentfault.com/a/1190000008010666

登录界面有了图怎么传数字并进行登录验证
https://github.com/bailicangdu/vue2-elm/blob/master/src/page/login/login.vue

getData数据界面要用async进行替换

函数表达式和函数声明的区别
函数声明就是function xx(){} 就像陈涉之于（陈涉世家）
而函数表达式只是某些js其中的一部分，就像曹操之于（三国演义）

promise
https://www.jianshu.com/p/c98eb98bd00c
