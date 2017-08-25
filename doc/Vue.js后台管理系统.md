# Vue.js后台管理系统

> [Vue.js](https://cn.vuejs.org) 渐进式 JavaScript 框架

## 环境配置

1. Node.js: <https://nodejs.org/en/download/>
2. vue-cli: <https://github.com/vuejs/vue-cli>

    ```bash
    npm install -g vue-cli
    ```

## Vue.js 使用

### 新建工程

初始化项目时, ESLint 选择 standard 规范, 确认使用 vue-router, 不启用测试相关配置.

```bash
vue init webpack vue-project # 下载 Vue.js 项目模板
cd vue-project
npm install                  # 安装项目依赖
npm run dev                  # 开发环境启动本地服务
# npm run build              # 编译发布, 发布到 dist 目录
```

### 项目结构

```bash
# [Project Structure](https://vuejs-templates.github.io/webpack/structure.html)
├── build/                      # webpack config files
│   └── ...
├── config/
│   ├── index.js                # main project config
│   └── ...
├── src/
│   ├── main.js                 # app entry file
│   ├── App.vue                 # main app component
│   ├── components/             # ui components
│   │   └── ...
│   └── assets/                 # module assets (processed by webpack)
│       └── ...
├── static/                     # pure static assets (directly copied)
├── .babelrc                    # babel config
├── .postcssrc.js               # postcss config
├── .eslintrc.js                # eslint config (JavaScript 规范检查配置)
├── .editorconfig               # editor config (编辑器配置, 包括换行符和缩进空格设置等)
├── index.html                  # index.html template
└── package.json                # build scripts and dependencies (编译命令及安装包依赖等)
```

### 页面编写方式

**单文件**

1. `template`, 模板(HTML), 至少需要一个根节点.
2. `script`, 业务逻辑(JavaScript).
3. `style`, 样式(CSS), 添加`scoped`属性表示只对当前组件有效.

```html
<!-- src/components/Hello.vue  -->
<template>
  <div class="hello">
  </div>
</template>

<script>
export default {
}
</script>

<style scoped>
</style>
```

**独立文件**

```html
<!-- my-component.vue -->
<template src="./my-component.html"></template>
<script src="./my-component.js"></script>
<style src="./my-component.css"></style>
```

## 常用配置

### 环境切换

通过不同的编译配置, 获取不同的请求域名. 以下配置完成后, 可通过`process.env.API_ROOT`获取当前环境请求域名.

**开发**

```javascript
//  config/dev.env.js
module.exports = merge(prodEnv, {
  NODE_ENV: '"development"',
  API_ROOT: '"http://stage.xxxx.com"'
})
```

**生产**

```javascript
//  config/prod.env.js
module.exports = {
  NODE_ENV: '"production"',
  API_ROOT: '"http://xxxx.com"'
}
```

### 代理

开发环境下启动本地服务, 请求存在跨域问题, 通过配置`proxyTable`解决.

```javascript
// config/index.js
proxyTable: {
  '/api': {
      target: 'http://stage.xxxx.com',
      changeOrigin: true,
      pathRewrite: {
      '^/api': '/api'
      }
  }
}
```

## 第三方依赖应用

### 路由 (vue-router)

> vue-router: <https://github.com/vuejs/vue-router>, <https://router.vuejs.org>

通过路由定义不同路径进入的页面.

```html
<!-- use router-link component for navigation. -->
<router-link to="/foo">Go to Foo</router-link>
<router-link to="/bar">Go to Bar</router-link>

<!-- component matched by the route will render here -->
<router-view></router-view>
```

```javascript
const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar }
]
```

### 状态管理 (Vuex)

> Vuex: <https://vuex.vuejs.org>

### 异步请求 (axios)

> axios: <https://github.com/mzabriskie/axios>

请求方式、实例配置、全局配置、通用请求工具包装.

```javascript
import axios from 'axios'

axios.defaults.baseURL = process.env.API_ROOT
axios.get('/api')
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

> 通过创建 axios 实例, 实现用不同的配置进行请求.

```javascript
const axiosIns = axios.create({
	baseURL: '',
	timeout: 60000,
	headers: {'token': 'foo'}
})
axiosIns.get('/api')
```

### UI (Element)

> Element: <http://element.eleme.io>

```javascript
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-default/index.css'

Vue.use(ElementUI)
```

```html
<el-button type="primary">Primary Button</el-button>
```

## Visual Studio Code 配置

**编辑器**

- Vetur: Vue.js语法高亮.
- Vue 2 Snippets: 代码片段
- EditorConfig: 编辑器配置, 提示格式问题.
- ESLint: JS 代码规范问题检测.

**配置**

> .vscode/settings.json

```json
{
  "eslint.enable": true,
  "eslint.options": {
    "extensions": [
      ".html",
      ".js",
      ".vue"
    ]
  },
  "eslint.validate": [{
      "language": "html",
      "autoFix": true
    },
    {
      "language": "vue",
      "autoFix": true
    },
    {
      "language": "javascript",
      "autoFix": true
    }
  ]
}
```

**浏览器**

1. vue-devtools: 浏览器调试. [从源码安装](https://github.com/vuejs/vue-devtools), [Chrome 应用商店下载](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=zh-CN)
