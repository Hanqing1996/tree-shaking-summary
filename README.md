#### 啥是 Tree Shaking
* [webpack 对 Tree Shaking 的相关介绍](https://webpack.docschina.org/guides/tree-shaking/)
* 我的理解
> 删除没用到的代码。日常开发经常需要引用各种库。但大多时候仅仅使用了这些库的某些部分，并非需要全部，此时Tree-Shaking如果能帮助我们删除掉没有使用的代码，将会大大缩减打包后的代码量。比如我们只用到用 Element-UI 的部分组件，那么我们就会希望打包后的代码中不包括那些没用到的组件代码
* 具体例子
> chrome 的 bundle.js 的 response 部分即为打包后的内容（即浏览器的js引擎负责解析的内容）
```
// source.js
import {a,b} from main.js

console.log(a)
```
使用 Tree Shaking，会判定 b 的引入是多余的（因为没有用到 b），因此在打包后的 bundle 文件中将不会引入 main.js
```
// bundle.js

var _main__WEBPACK_IMPORTED_MODULE_4__ = __webpack_require__(/*! ./main */ "./src/main.js");// 只引入 

```


#### Tree Shaking 的实现
* ES6的模块引入是静态分析（被 parse 成 AST 时，可以分析出依赖了哪些模块，哪些接口）的，故而可以在编译时正确判断到底加载了什么代码。因此我们可以借助ES6的模块机制实现 Tree Shaking 
* Common.js 的 require 是动态加载的，因此实现不了 Tree Shaking 
  * 在用 create-react-app 创建的项目中，如果需要使用 svg-sprite-loader 来识别 svg。当我们不对引入的 symbol 对象做显式调用时，webpack 会默认进行 Tree Shaking，判定引入的 symbol 对象是多余的代码
* [ES6如何进行模块静态分析](https://www.zhihu.com/question/63240671)
