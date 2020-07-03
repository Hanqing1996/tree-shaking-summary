#### 啥是 Tree Shaking
* [webpack 对 Tree Shaking 的相关介绍](https://webpack.docschina.org/guides/tree-shaking/)
* 我的理解
> 删除没用到的代码。日常开发经常需要引用各种库。但大多时候仅仅使用了这些库的某些部分，并非需要全部，此时Tree-Shaking如果能帮助我们删除掉没有使用的代码，将会大大缩减打包后的代码量。比如我们只用到用 Element-UI 的部分组件，那么我们就会希望打包后的代码中不包括那些没用到的组件代码

#### Tree Shaking 的实现
* ES6的模块引入是静态分析（被 parse 成 AST 时，可以分析出依赖了哪些模块，哪些接口）的，故而可以在编译时正确判断到底加载了什么代码。因此我们可以借助ES6的模块机制实现 Tree Shaking 
* Common.js 的 require 是动态加载的，因此实现不了 Tree Shaking 
* [ES6如何进行模块静态分析](https://www.zhihu.com/question/63240671)
