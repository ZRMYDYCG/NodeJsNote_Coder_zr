# Node.js 模块

模块系统是 Node.js 最基本也是最常用的。一般情况模块可以分为四类:

+ 原生模块
+ 文件模块
+ 第三方模块
+ 自定义模块

## 自定义模块

1. 创建模块(b.js)

```js
//b.js
function FunA(){
    return 'Tom';
}
//暴露方法 FunA
module.exports = FunA;
```

2. 加载模块(a.js)

```js
//a.js
var FunA = require('./b.js');//得到 b.js => FunA
var name = FunA();// 运行 FunA，name = 'Tom'
console.log(name); // 输出结果
```

## module.exports

module.exports 就 Node.js 用于对外暴露，或者说对外开放指定访问权限的一个对象。如上面的案例，如果没有这段代码

```js
module.exports = FunA;
```

那么 require('./b.js') 就会为 undefined。 一个模块中**有且仅有一个 module.exports**，如果有多个那后面的则会覆盖前面的。

## exports

exports 是 module 对象的一个属性，同时它也是一个对象。在很多时候一个 js 文件有多个需要暴露的方法或是对象，module.exports 又只能暴露一个，那这个时候就要用到 exports:

```js
function FunA(){
    return 'Tom';
}

function FunB(){
    return 'Sam';
}

exports.FunA = FunA;
exports.FunB = FunB;
```

引入:

```js
//FunA = exports,exports 是一个对象
var FunA = require('./b.js');
var name1 = FunA.FunA();// 运行 FunA，name = 'Tom'
var name2 = FunA.FunB();// 运行 FunB，name = 'Sam'
console.log(name1);
console.log(name2);
```

当然在引入的时候也可以这样写：

```js
//FunA = exports,exports 是一个对象
var {FunA, FunB} = require('./b.js');
var name1 = FunA();// 运行 FunA，name = 'Tom'
var name2 = FunB();// 运行 FunB，name = 'Sam'
console.log(name1);
console.log(name2);
```

# nrm

```bash
npm -v
```

使用nrm管理npm下载源

```js
npm install -g nrm
```

执行命令nrm ls查看可选的源。

```bash
*npm ---- https://registry.npmjs.org/

cnpm --- http://r.cnpmjs.org/

taobao - http://registry.npm.taobao.org/

eu ----- http://registry.npmjs.eu/

au ----- http://registry.npmjs.org.au/

sl ----- http://npm.strongloop.com/

nj ----- https://registry.nodejitsu.com/
```

其中，带*的是当前使用的源，上面的输出表明当前源是官方源。

切换

如果要切换到`taobao`源，执行命令 `nrm use taobao`。

增加

你可以增加定制的源，特别适用于添加企业内部的私有源，执行命令 `nrm add <registry> <url>`，其中`reigstry`为源名，`url`为源的路径。

```bash
nrm add registry http://registry.npm.frp.trmap.cn/
```

删除

执行命令nrm del <registry>删除对应的源。

测试速度

你还可以通过 nrm test 测试相应源的响应时间。

```bash
nrm test npm  
```

# npm scripts

## 什么是 npm 脚本？

npm 允许在package.json文件里面，使用scripts字段定义脚本命令。package.json 里面的scripts 字段是一个对象。它的每一个属性，对应一段脚本。定义在package.json里面的脚本，就称为 npm 脚本。

## 使用

`npm run` 脚本名称

如果是并行执行（即同时的平行执行），可以使用&符号。 `npm run script1.js & npm run script2.js`

如果是继发执行（即只有前一个任务成功，才执行下一个任务），可以使用&&符号。`npm run script1.js && npm run script2.js`

## 简写形式

npm start 即 npm run start

npm stop 即 npm run stop

npm test 即 npm run test

npm restart 即 npm run stop && npm run restart && npm run start








