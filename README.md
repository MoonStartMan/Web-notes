# Web-notes

<p align="center">
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white" alt="HTML5">
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white" alt="CSS3">
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black" alt="JavaScript">
  <img src="https://img.shields.io/badge/Vue.js-4FC08D?style=flat-square&logo=vue.js&logoColor=white" alt="Vue.js">
  <img src="https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black" alt="React">
  <img src="https://img.shields.io/badge/Webpack-8DD6F9?style=flat-square&logo=webpack&logoColor=black" alt="Webpack">
</p>

<p align="center">
  <b>Web开发问题解决方案与技巧笔记库</b>
</p>

## 项目简介

Web-notes 是一个专注于记录Web开发过程中遇到的各种问题及其解决方案的知识库。本仓库汇集了前端开发中常见的技术难点、最佳实践和实用技巧，涵盖HTML、CSS、JavaScript、Vue.js、React、Webpack等多种前端技术。

## 功能特性

- 全面的问题解决方案：涵盖前端开发各类常见问题
- 实用的代码示例：每个问题都配有详细的代码说明
- 多技术栈覆盖：涉及主流前端框架和工具
- 持续更新：随着技术演进不断补充新内容
- 中文文档：所有内容均为中文，便于国内开发者阅读

## 技术栈

| 类别 | 技术 |
|------|------|
| 基础技术 | HTML5, CSS3, JavaScript (ES6+) |
| 前端框架 | Vue.js, React |
| 构建工具 | Webpack 4.x |
| 版本控制 | Git |
| 后端技术 | Express.js |

## 项目结构

```
Web-notes/
├── vue组件之间的传值/          # Vue组件通信相关笔记
├── CSS相关技巧/               # CSS布局与样式技巧
├── JavaScript技巧/            # JS编程技巧
├── Git操作指南/               # Git版本控制技巧
├── 前端工程化/                # Webpack等工具配置
└── 其他问题解决方案/           # 各类杂项问题
```

## 内容分类

### CSS 技巧
- fixed定位居中高度自适应
- 当高度为百分比时如何使用line-height使文字垂直居中
- td标签文字超出部分省略

### JavaScript 技巧
- jQuery动态创建元素绑定点击事件注意事项
- 原生JS动态修放播放音乐
- 前端下载二进制乱码解决方法

### Vue.js 技巧
- Vue组件之间的传值方法
- 父子组件通信
- 兄弟组件通信
- 跨级组件通信

### Git 操作
- git-clone单个文件夹
- github版本回退
- git取消本地commit以及修改git的url

### 工程化配置
- 利用webpack4.x创建react项目
- webpack添加mp3文件配置
- express解决本地接口跨域问题

### 多媒体处理
- video全屏解决方法

### 页面传值
- 新闻页面传值

## 使用示例

### 1. 查看特定问题的解决方案

每个Markdown文件都是一个独立的问题解决方案，直接点击即可查看详细内容。

例如：`fixed定位居中高度自适应.md`

```css
/* 使用transform实现fixed定位居中 */
.center-fixed {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

### 2. Vue组件传值示例

在 `vue组件之间的传值` 文件夹中，包含完整的缓冲了多种Vue组件通信方式的详细说明：

```javascript
// 父组件向子组件传值 (Props)
// 子组件向父组件传值 ($emit)
// 兄弟组件通信 (Event Bus / Vuex)
```

##3 3. Webpack配置示例

`利用webpack4.x创建react项目.md` 提供了从零开始配置React项目的完整步骤：

```javascript
// webpack.config.js 基础配置
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: 'babel-loader'
      }
    ]
  }
};
``@

## 安装与使用

本仓库为纯文档仓库，无需安装任何依赖。您可以通过以下方式使用：

### 方式一：在线浏览器（Chrome、Firefox、Safari、Edge）
- 本地服务器（部分DEMO需要）

### 方式二：本地克隆
```bash
# 克隆仓库到本地
git clone https://github.com/MoonStartMan/Web-notes.git

# 进入项目目录
cd Web-notes

# 使用任意Markdown阅读器查看
```

### 方式三：克隆单个文件
```bash
# 使用svn克隆单个文件（无需下载整个仓库）
svn export https://github.com/MoonStartMan/Web-notes/trunk/fixed定位居中高度自适应.md
```

## 贡献指南

我们欢迎所有开发者为本仓库贡献内容！

### 提交Issue
如果您发现了问题或有新的建议，欢迎提交Issue：
1. 点击仓库的 "Issues" 标签
2. 点击 "New issue" 按钮
3. 描述您的问题或建议

### 提交Pull Request
1. Fork 本仓库到您的账号
2. 创建新的分支：`git checkout -b feature/your-feature-name`
3. 添加或修改内容
4. 提交更改：`git commit -m 'Add: 新增XX\问题解决方案'`
5. 推送到分支：`git push origin feature/your-feature-name`
6. 创建 Pull Request

##3 内容规范
- 使用清晰的标题描述问题
- 提供详细的解决步骤
- 包含完整的代码示例
- 添加必要的注释说明
- 使用Markdown格式编写

## 许可证

本项目采用 [MIT License](LICENSE) 开源许可证。

## 联系方式

- 作者：MoonStartMan
- GitHub：[https://github.com/MoonStartMan](https://github.com/MoonStartMan)
- 邮箱：请通过GitHub联系

## 致谢

感谢所有为本仓库贡献内容的开发者！

---

<p align="center">
  如果本项目对您有帮助，请给个 Star ⭐
</p>
