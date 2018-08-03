# 3.5
 用React写一个数字华容道，你需要知道的秘密

 最小单元的react组件就是带有render方法的component类实现

 v-if v-for 
 模板逻辑，用变量去做
 react 独有的html模板变量 jsx(js in javaScript)
 在db里面，没有table，用collectio表示表

# 3.6
    app.get('/',function(req,res){})
    req:请求 res:返回
    数据库查询 m
    业务处理 c
    view v

# 3.7
    文件的类型
    text/html png text/css 总称mime
    node 异步无阻塞
# 3.8
1. npm run build
dev => build =>product
dist目录就是等待处理的静态文件
静态服务器：支持dist目录下所有文件都可以被访问
接口

# 3.9
// 异步
Promise .then .catch
file mysql 都是异步的，需要异步转同步
async await  
启动静态服务器
var express = require('express')
var app = express();
var server = require('http').createServer(app);
app.use('/',express.static(__dirname+'/www'))
server.listen(3000);

socket 是实时RealTime核心，
http协议是无法长链接的，一旦送达，立马断开 
如果想跟服务器连接，只能ajax提交（长期轮询,消耗资源），再提交get/post（刷新页面）
后来有人用iframe（内嵌网页用来通讯）

# 3.10
mongodb NOSQL 的数据库
文档数据库 区别于关系型数据库
数据库里面存了一个个文件，doc 这里面的内容就是json（bison文件，进行了优化）
支持全面js的解析 它的命令行（shell）为js风格
mongod --dbpath D:\db\data
mongo shell 
适合存储非结构数据
show dbs 列出数据库
ues tutorial 选用数据库
命名空间的集合
collection 集合
mongodb  不需要先声明，直接保存就可以创建了
column可以允许一些冗余

ssr
页面会输出所有的东西，方便爬虫搜索引擎搜索
vue，只会输出一个挂载点

seo
nuxt的本质是将vue交给后端渲染
在webpack里面有server-side-renderer
react中有next.js
所以vue里面有nuxt
.vue => html/css/js后端渲染
所以这个时候，data可能来自后端或者来自前端，所以要进行区分，所以用asyncData
user-agent判断用户的所使用的浏览器的种类和版本
url/api/user=>router 匹配
=>controller 后端业务逻辑
=>model view 通信

mongoose 是驱动器 数据库抽象

# 3.12
mongodb 操作 支持内部js解析引擎
数据过多的时候加索引
mongodb
.find() 返回的是cursor（游标）
比如查询20000条数据，会展示前20条数据
$开始的运算符， mongodb支持js风格的编译
表达范围 $gt $lt 开始到结尾
用json对象
性能优化，用explain进行操作分析
react 没有帮你实现双向绑定
所以要加上事件监听代码
prefix所有东西前面都会加上/api
md5加密
份额page 每页条limit

# 3.13
reducer 纯函数 旧状态+参数 返回新状态
thunk 允许异步
action处理异步，reducer
由页面触发一个action，在reducer（oldState，data）->返回一个新状态
middleware作为中间件，可以做一个log，根据点击数量，做一张热力图
Schema 设计 电商网站 good是 orders cate user
mongodb给了我们文档NOSQL便利
数据类型 json array
如果在amaze买 农机产品 
{
    _id:ObjectId(),
    name:'Extra Large Wheelballow'
    description:'Heavy duty wheelbarrow...',
    text:'',
    details:{
        weight:47,
        weight_units: "lbs",
	    model_num: 4032983402
        manufacture:'Acme',
        color:"Green"
    },
    pricing:{
        sale:489700,
        retail:589700
    },
    price_history:[{
        {
            retail:529700,
            sale:429700,
            start:new Date(2017,11,11),
            end:new Date(2017,11,12)
        }
    },
    {
        {
            retail:529700,
            sale:429700,
            start:new Date(2018,5,1),
            end:new Date(2018,5,2)
        }
    }],
    total_reviews:4,
    average_review:4.5,
    created_at:,
    updated_at;,
    tags:['tools','gardening','soil'],
    primary_category:ObjectId("fdfdfdfdafs"),
    category_ids:[
        ObjectId("fdfdfdfdafs"),
        ObjectId("ffffff")
    ]
}
# 3.14
redux container 概念 父组件 与redux通信
props，action是=>子组件
Immutable 状态不可变
react state 改变会rerender 
redux 使用immutable来实现不可变的state
业界认为，可变的状态是万恶之源
如果进行操作state没有变，这时候没有必要rerender（性能问题）
浅拷贝，深拷贝
模块化
n个reducer users.js auth article
redux 怎么到ui组件里面去，通过connect
connect在返回的时候加一层redux
react风格，什么东西都喜欢jsx，并且组件化指令
action 负责提交reducer
# 3.16
// co 顺序执行异步，自动化方案
// 生成器函数 async
function* fn(a){
    // 添加一些异步的操作 同步化运行
    a = yield a
    let b= yield 2;
    let c = yield 3;
    return a+b+c;
}
function co(fn,...args){
    let g = fn(...args);
    return new Promise((resolve,reject)=>{
        function next(lastValue){
            // next 参数可以参与yield后面的计算
            let {value,done}=g.next(lastValue)
            if(done){
                resolve(value);
            }else{
                next(value)
            }
        }
        next();
    })
    // fn() 执行才能去迭代
    // next()才能往下走
    // 返回值 done true or false
    // resolve 那一刻
}
// return Promise 
co(fn,100)
.then(value=>{
    console.log(value)
})
// 迭代器
let g = fn();
console.log(g.next())
console.log(g.next())
console.log(g.next())
console.log(g.next())

节流：
        // 函数节流 mousemove scroll 是否加载数据 出现指示
        // 函数执行的太平凡，就有可能导致内存的使用量加大，页面性能下降，减少执行
        // 在一定的时间50ms，执行一次
        // 闭包就是在函数运行的时候可以引用到它定义的时候的函数作用域
        let throttle = (fn,delay=50)=>{
            let stattime = 0;
            return function(...args){
                let curTime = new Date();
                if(curTime-stattime>=delay){
                    fn.apply(this,args);
                    stattime = curTime;
                }

            }
        }
        function doMousemove(event){
            console.log(event.clientX,event.clientY)
        }
        let slowMousemove = throttle(doMousemove,2000)
        const oBox = document.querySelector('.box');
        oBox.addEventListener('mousemove',(event)=>{
            slowMousemove(event)
        })

# 3.17
typescript (2012年推出)微软开发，javascript 超集
js有一个弊病，不太适合企业开发
需要协同，就需要文档，面向对象（opp）的模块化方案
Interface 泛型
class protected
private implements
类化，显示声明 提供了一个js的类型系统
阿里技术栈：React+TypeScript
预编译，将一个.ts->.js
ts 带了了预编译的js，从动态语言，静态，类型检测，杜绝错误。
typescript 类型？
typescript 认为undefined 是其他类型的子类型

泛型
是指在定义函数，接口或类的时候，不预先指定具体的类型，在使用时在制定类型的一种特性

function a() {}
var b = {}
a.prototype = b
b.constructor = a 

# 3.22
extract-text-webpack-plugin webpack必备插件
利用浏览器并发进行http协议下载

# 3.23
reducers 是react的核心，用来改变状态
store 页面全局访问
...state 推平数组，展开所有内容

        case 'DELETE_POST':
            return state.filter(item=>action.id !== item.id)
        default:return state
        删除