## 1. 设置alias

``` javascript
// 方式一
// 对于vscode提示 `__dirname`未定义报错，通过安装 npm install @types/node -D 解决
import path from "path";

export default defineConfig({
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "src")
    },
  },
  plugins: [vue()],
})

// 方式二
// npm install @types/node -D
// 文档：https://nodejs.cn/api/url.html#url
import { fileURLToPath, URL } from 'node:url' // node14版本为 const url = require('url');
export default defineConfig({
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    },
  },
  plugins: [vue()],
})


// ts配置 - tsconfig.js
"compilerOptions": {
  "paths":{
    "@/*": ["src/*"]
  }
}
```