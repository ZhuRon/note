1. 初始化项目为node项目   npm init -y

2. 修改package.json的scripts，添加"stylus:watch": "stylus -w -m styl/ -o dist/css"

3. 根目录添加stylus    yarn add --dev stylus

4. 运行npm run stylus:watch


styl里变量的原理属于正则替换
styl里的嵌套可以借鉴理解mvvm里的概念，每个组件有单独的嵌套规则

根目录添加normalize、font-awesome
yarn add normalize.css
yarn add font-awesome

index.html引入
<link rel="stylesheet" href="./node_modules/normalize.css/normalize.css">
<link rel="stylesheet" href="./node_modules/font-awesome/font-awesome.css">
<link rel="stylesheet" href="./dist/css/style.css">

修改babelrc中的 "presets" 为 ["env"]，
删除package.json中的es2015那一行，
安装
yarn global add babel-preset-env

注释webpack.config.js中的69行代码块

运行
yarn
npm i babel-preset-env --save-dev  
npm run dev & npm run serve


yarn add webpack --dev
yarn add jquery bootstrap
yarn add webpack babel-core babel-loader babel-preset-env handlebars handlebars-loader --dev


webpack需要一个配置文件，输出webpack  入口main.js、出口bundle.js
{{!-- 源代码和浏览器效果中间的webpack类似编译器，但没有起到编译的作用。
    起到编译作用的是stylus、babel...
    webpack是管理编译器(stylus、babel)的管理者通过loader来管理 --}}
请求
 npm install --save mock axios