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

socker 是实时RealTime核心，
http协议是无法长链接的，一旦送达，立马断开 
如果想跟服务器连接，只能ajax提交（长期轮询,消耗资源），再提交get/post（刷新页面）
后来有人用iframe（内嵌网页用来通讯）
