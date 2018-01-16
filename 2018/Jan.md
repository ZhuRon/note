# 1.2
Webpack：yarn add --dev webpack babel-core babel-loader babel-preset-env
Webpack教学
const webpack = require('webpack');
const path = require('path');
module.exports = {
    //入口
    entry:{
        // bundle 打包
        'tqb-date-picker':'./app/main.js'
    },
    //出口
    output:{
        filename:'[name].bundle.js',
        //windows（c:/）和Linux（var.root） 盘符不同，所以用__dirname,得到一个绝对路径，这是一个node的常量
        path:path.resolve(__dirname,'dist')
    },
    // 负责每一个环节
    module:{
        // 加载器 import .js babel-loaders babel的编译功能
        // stylus
        loaders:[{
            test:/\.js/,
            exclude:/node_modules/,
            loader:"babel-loader"
        }]
    }
}

Stylus 预编译
Npm init –y  初始化 
在pagejson里面加：
    "stylus:watch": "stylus -w -m styl/ -o dist/css",
然后yarn add –dev stylus
Live-server进行监听
yarn add normalize.css

normalize不是一定要打包的，是不是整站开发（东西比较多所以都要打包）
但是新手很少做整站开发，都是模块开发。
有很多个dist目录
对于通用性的模块不要乱打包，会导致资源的重复加载
yarn add font-awesome 安装图标字体库
font-awesome 解决特定问题，10%的页面要用到，按需加载，如果需要再单独加一下
为了减少http数，可以进行单独的打包，dist/bundle1.js…
Sylus变量的本质就是正则替换
# 1.3
Stylus借鉴mvvm中的组件化进行嵌套
Mvvm负责加组件 webpack负责打包组件的js 最后向root挂载组件就好
Dev是开发时候运行的，build是上线时一键运行的
// 将app挂载（mount）到页面root（挂载点）上
new Vue({
    el:'#root',
    template:'<App/>',
    components:{
        App
    }
})
El：指定挂载点

resetful 网站的本质就是提供资源访问
url 跟资源的一一对应关系
？queryString1=a&queryString2=b
backend 来做 路由规则 route rules
以前在后端中，一般是mvc，会负责解析url，映射一个route，跟后端脚本对应的controller
/book/123456(以前)
/api（现在）
fontend 接管一切
前端跟服务器相关性问题
后端开发方式：
url=>资源 缺点：http协议，资源跳转需要点击资源（herf），每次点击都会导致刷新页面。用户体验太差
pc时代可以忍受，移动时代不能忍受
https://m.taobao.com/#index 前端url 标记首页
https://m.taobao.com/#home  标记小家
html5 historyAPI 不会跳转页面，当你点击之后会触发一个事件，然后用ajax动态获取数据
前端url，不再是刷新式跳转，而是切换一张小卡片，就像整个页面都没有动。
这就叫做单页应用 SinglePageApplication
如何动态更新界面？
前端url规则：
    启动，交给ajax
    vue？ url => page => 组件

    <script src="https://cdn.bootcss.com/jquery/2.2.0/jquery.min.js"></script>
    <script>
        (function(){
            $(function(){
                $(document).on('click','a',(event)=>{
                    event.preventDefault()
                    // 显示新的页面 jquery ajax 模块
                    // 发生请求
                    const req =$.ajax(event.target.href);
                    // 异步就好了，等待请求完成
                    req.done(data=>{
                        //字符串=>dom .content
                        $('.content').text($(data).find('.content').text());
                        $('.photo').attr('src',$(data).find('.photo').attr('src'));
                    })
                })
            })
        })();


        (function(){
            $(function(){
                function displayContent(state){
                    $('.content').text(state.content);
                    $('.photo').text('src',state.photo);
                    
                }
                function createState($content){
                    let state = {
                        "content":$content.find('.content').text(),
                        "photo":$content.find('.photo').attr('src'),
                        "title":$content.find('title').text(),
                    }
                    // url 在单页应用中不再一一对应page
                    // 状态对象 检索不同的状态
                    return state;
                }
                $(document).on('click','a',(event)=>{
                    event.preventDefault()
                    // 显示新的页面 jquery ajax 模块
                    // 发生请求
                    const url = event.target.href;
                    const req =$.ajax(url);
                    // 异步就好了，等待请求完成
                    req.done(data=>{
                        //字符串=>dom .content
                        // $('.content').text($(data).find('.content').text());
                        // $('.photo').attr('src',$(data).find('.photo').attr('src'));

                        // 只有一个界面了，我们都4个state 但是url 不工作了
                        // url => state 发生一个映射
                        let state = createState($(data));
                        displayContent(state);
                        // url在浏览器实现里面就是一个栈
                     
                        
                        history.pushState(state,state.title,url);

                    })
                })
            })
        })();

# 1.4
模板
有{n}个用户信息可能要在页面显示，预编译html模板的需求
Webpack 一切皆可打包，包括模板
现在有很多东西能够帮助程序员减少工作量
Js可以用babel
Css可以用stylus
Html（模块）可以用hbs
Webpack管理这些编译器（个人理解）
webpack需要一个配置文件，输出webpack  入口、出口
{{!-- 源代码和浏览器效果中间的webpack类似编译器，但没有起到编译的作用。
    起到编译作用的是stylus、babel...
    webpack是管理编译器(stylus、babel)的管理者
        通过loader来管理 --}}

# 1.5
用js的dom操作可以再html中写东西，
用css在html里面写东西，通过before，after伪元素的content属性来做
  ul,li{
            list-style: none;
            margin: 0;
            padding: 0;
        }
        ul{
            counter-reset: section;
        
        }
        li:after{
            /* content: '第'attr(date-index)'个元素'; */
            content: counter(section);
            counter-increment: section;
        }


Stylus 提供批发生成类的能力
比如stylus中：
table
    for row in (1..10)
        tr:nth-child({row}) td
            height: 50px*row
         
预编译之后会变成：
table tr:nth-child(1) td {
  height: 50px;
}
table tr:nth-child(2) td {
  height: 100px;
}
。。。
table tr:nth-child(10) td {
  height: 500px;
}


模板引擎
{{#if static}}static{{/if}}


# 1.6
webpack.config.js内容
const webpack = require('webpack');
const path = require('path');

module.exports = {
  entry: path.resolve(__dirname + '/src/main.js'),
  output: {
    path: path.resolve(__dirname + '/dist/js'),
    filename: 'bundle.js'
  },
  devtool: 'source-map',
  module: {
    loaders: [
      {
        test: /\.vue$/,
        loader: 'vue-loader'
      }
    ]
  },
  resolve: {
    extensions: ['.js', '.vue'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    }
  }
}



return{
      listState:[
        {
          
        }
      ]
    }
计算属性
# 1.8
基础组件：界面ui的基石
功能组件：完成某个功能
集合组建：评论（数据的管理）
页面级别组件
框架级别组件
在vue中，开发任务组件为最小单元
子组件管数据，会导致数据不协同，所以要让父组件来管理子组件的数据
Vue中数据绑定：双向绑定或者ref（找元素或者节点）
子组件向父组件提交事件叫emit
            // 数据驱动界面 单向数据绑定 v-bind：（数据）="" data->template
            // 双向数据绑定 input->data  data<=>template 性能差

# 1.9
    vue renderer
    template ->pre complie
    vue scope

{{}}为占位符，以{{}}开始的地方就是要开始模板替换的地方
实时编译，node
// vm =>Vue 实例 mvvm 虚拟DOM对象 
// 真实DOM非常消耗内存 VM 将很多次的修改集中成为一次DOM修改
生命周期函数，就是在相应的时刻发生的时间钩子


Vue.js双向绑定的实现原理（终极图解版）
源码
function Compile(el, vm) {
    this.vm = vm;
    this.el = document.querySelector(el);
    this.fragment = null;
    this.init();
}

Compile.prototype = {
    init: function () {
        if (this.el) {
            this.fragment = this.nodeToFragment(this.el);
            this.compileElement(this.fragment);
            this.el.appendChild(this.fragment);
        } else {
            console.log('Dom元素不存在');
        }
    },
    nodeToFragment: function (el) {
        var fragment = document.createDocumentFragment();
        var child = el.firstChild;
        while (child) {
            // 将Dom元素移入fragment中
            fragment.appendChild(child);
            child = el.firstChild
        }
        return fragment;
    },
    compileElement: function (el) {
        var childNodes = el.childNodes;
        var self = this;
        [].slice.call(childNodes).forEach(function(node) {
            var reg = /\{\{(.*)\}\}/;
            var text = node.textContent;

            if (self.isElementNode(node)) {  
                self.compile(node);
            } else if (self.isTextNode(node) && reg.test(text)) {
                self.compileText(node, reg.exec(text)[1]);
            }

            if (node.childNodes && node.childNodes.length) {
                self.compileElement(node);
            }
        });
    },
    compile: function(node) {
        var nodeAttrs = node.attributes;
        var self = this;
        Array.prototype.forEach.call(nodeAttrs, function(attr) {
            var attrName = attr.name;
            if (self.isDirective(attrName)) {
                var exp = attr.value;
                var dir = attrName.substring(2);
                if (self.isEventDirective(dir)) {  // 事件指令
                    self.compileEvent(node, self.vm, exp, dir);
                } else {  // v-model 指令
                    self.compileModel(node, self.vm, exp, dir);
                }
                node.removeAttribute(attrName);
            }
        });
    },
    compileText: function(node, exp) {
        var self = this;
        var initText = this.vm[exp];
        this.updateText(node, initText);
        new Watcher(this.vm, exp, function (value) {
            self.updateText(node, value);
        });
    },
    compileEvent: function (node, vm, exp, dir) {
        var eventType = dir.split(':')[1];
        var cb = vm.methods && vm.methods[exp];

        if (eventType && cb) {
            node.addEventListener(eventType, cb.bind(vm), false);
        }
    },
    compileModel: function (node, vm, exp, dir) {
        var self = this;
        var val = this.vm[exp];
        this.modelUpdater(node, val);
        new Watcher(this.vm, exp, function (value) {
            self.modelUpdater(node, value);
        });

        node.addEventListener('input', function(e) {
            var newValue = e.target.value;
            if (val === newValue) {
                return;
            }
            self.vm[exp] = newValue;
            val = newValue;
        });
    },
    updateText: function (node, value) {
        node.textContent = typeof value == 'undefined' ? '' : value;
    },
    modelUpdater: function(node, value, oldValue) {
        node.value = typeof value == 'undefined' ? '' : value;
    },
    isDirective: function(attr) {
        return attr.indexOf('v-') == 0;
    },
    isEventDirective: function(dir) {
        return dir.indexOf('on:') === 0;
    },
    isElementNode: function (node) {
        return node.nodeType == 1;
    },
    isTextNode: function(node) {
        return node.nodeType == 3;
    }
}

# 1.10
Vue的实质，mvvm的数据绑定，es6的defineproperty
异步
Object.defineProperty(a,"b",{
    value:123,
    writable:true
});
Writable：可写的，默认为false
configurable:true
可设置的，默认为false
var a ={}; //被代理或被劫持
Object.defineProperty(a,"b",{
    value:123312,
    enumerable:true
});
for (key in a){
    console.log(key,a[key]);
}
设置为true时，可被遍历。默认false
for (key in a){
    console.log(key,a[key]);
}
For key in 循环遍历每一项

var a = {};
//精细化操作对象的属性访问 读取,设置，是否可配置，是否可读，是否可写
// 三个参数 
// 目标对象 
// 需要定义的属性或方法的名字（对象中要的更新/增加的属性） 
// 目标属性所拥有的特性（属性的相应配置）dscriper
Object.defineProperty(a,"b",{
    value:123,
    writable:true,
    configurable:false
    
});

Object.defineProperty(a,"b",{
    value:123,
    writable:false,
    configurable:true
    
});
a.b=43;
console.log(a.b);

// 回调函数
// node 异端无阻塞 高并发，迅速降低服务器成本
// 异步的好处在于，node提高性能


// 回调地狱
const fs =require("fs");
fs.readFile('input.txt',function(err,data){
    console.log(data.toString());
    fs.readFile('input2.txt',function(err,data){
        console.log(data.toString());
        fs.readFile('input3.txt',function(err,data){
            console.log(data.toString());
				。。。。
        })
    })
});

 
# 1.12
<header class="header" :class="{'header-fixed':headerFixed}">
headerFixed是页面的状态，随着操作状态改变（生命周期）
vue中不推荐dom操作，所以在标签中埋好状态，通过事件或者其他操作改变数据来改变状态从而改变页面。

# 1.13
elementUI源码分析
  mode:'history'
当你使用这个时候，是使用到了js中的history API
:class="[]"
动态绑定，【】里面为js运行区域

# 1.14

vuex(数据管理) vue 三驾马车之一
建立数据中央存储中心 store
数据跟界面分离
数据驱动界面

# 1.15
http://blog.csdn.net/h5_queenstyle12/article/details/75386359
最详细的Vuex教程
 