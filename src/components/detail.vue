<template>
  <el-container>
    <el-aside class="el-aside-component-list" width="150px">
      <div class="aside-title">组件列表</div>
      <el-main>
        <el-menu
          class="el-menu-vertical-demo"
          @open="handleOpen"
          @close="handleClose"
          :collapse="isCollapse"
        >
          <el-menu-item index="1">
            <i class="el-icon-menu"></i>
            <span slot="title">组件一</span>
          </el-menu-item>
          <el-menu-item index="2">
            <i class="el-icon-menu"></i>
            <span slot="title">组件二</span>
          </el-menu-item>
          <el-menu-item index="3">
            <i class="el-icon-setting"></i>
            <span slot="title">组件三</span>
          </el-menu-item>
        </el-menu>
      </el-main>
    </el-aside>
    <el-container>
      <el-header height="auto">
        <div class="header-layer">
          <div class="header-layer-wrapper">
            <i class="el-icon-menu"></i>
            <p class="header-title">Neoteric Plumbing Mishap</p>
            <ul class="header-navigation">
              <li>npm Enterprise</li>
              <li>Product</li>
              <li>Solutions</li>
              <li>Resources</li>
              <li>Docs</li>
            </ul>
          </div>
        </div>
      </el-header>
      <el-main>
        <el-container class="components-intro-content-container">
          <el-main class="components-intro-content markdown-body">
            <div v-html="compiledMarkdown"></div>
          </el-main>
          <el-aside width="300px"></el-aside>
        </el-container>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
import componentList from "./componentsList";
import testMarkdown from "./../assets/lazyload.md";
let emojify = require("emojify.js");
let marked = require("marked");
let hljs = require("highlight.js");
import "highlight.js/styles/monokai.css";
import "emojify.js/dist/css/data-uri/emojify.min.css";
emojify.setConfig({tag_type : 'div'});
emojify.run();
marked.setOptions({
  renderer: new marked.Renderer(),
  gfm: true,
  tables: true,
  breaks: false,
  pedantic: false,
  sanitize: false,
  smartLists: true,
  smartypants: false,
  highlight: function(code, lang) {
    if (lang && hljs.getLanguage(lang)) {
      return hljs.highlight(lang, code, true).value;
    } else {
      return hljs.highlightAuto(code).value;
    }
  }
});

export default {
  name: "Detail",
  components: { componentList },
  data() {
    return {
      isCollapse: false
    };
  },
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    }
  },
  computed: {
    compiledMarkdown() {
      let detail = testMarkdown;
      console.log(emojify);
      let markedText = marked(detail || "", {
        sanitize: true
      })
      return emojify.replace(markedText);
    }
  }
};
</script>
<style lang="less">
.el-container {
  height: 100%;
  width: 100%;
}
.el-header,
.el-footer {
  background-color: #fff;
  color: #333;
  text-align: center;
  padding: 0;
  z-index: 99;
  box-shadow: 0 2px 5px #ddd;
}

.el-aside-component-list {
  z-index: 199;
  background-color: #d3dce6;
  color: #333;
  text-align: center;
}

.el-main {
  color: #333;
}

body > .el-container {
  margin-bottom: 40px;
}

.el-container:nth-child(5) .el-aside,
.el-container:nth-child(6) .el-aside {
  line-height: 260px;
}

.el-container:nth-child(7) .el-aside {
  line-height: 320px;
}

.header-layer {
  padding: 20px 15px;
}
.header-layer-wrapper {
  margin: 0 auto;
  max-width: 1280px;
  height: 100%;
  display: flex;
  align-items: center;
}
.header-layer + .header-layer {
  border-top: 1px solid rgba(0, 0, 0, 0.1);
}

.header-title {
  padding: 0 50px;
  text-align: left;
  flex: 1;
}
.header-navigation {
}
.header-navigation > li {
  float: left;
  margin-left: 20px;
}

.el-select .el-input {
  width: 130px;
}
.input-with-select .el-input-group__prepend {
  background-color: #fff;
}
.el-input-group__append .el-button,
.el-input-group__append .el-select,
.el-input-group__prepend .el-button,
.el-input-group__prepend .el-select {
  display: inline-block;
  margin: -2px -20px;
}
.el-input-group__append,
.el-input-group__prepend {
  background-color: #fb3e44;
  color: #fff;
}

.el-main {
  padding: 0;
  border: none;
}

.el-aside {
  background: #fff;
  overflow: hidden;
  border-right: solid 1px #e6e6e6;
}
.aside-title {
  padding: 20px 0;
  background: #409eff;
  color: #fff;
}
.el-menu {
  height: 100%;
}

.components-intro-content {
  padding: 50px;
}
.components-intro-content-container {
  text-align: left;
  code[class*="language-"],
  pre[class*="language-"] {
    color: #ccc;
    background: none;
    font-family: Consolas, Monaco, Andale Mono, Ubuntu Mono, monospace;
    text-align: left;
    white-space: pre;
    word-spacing: normal;
    word-break: normal;
    word-wrap: normal;
    line-height: 1.5;
    -moz-tab-size: 4;
    -o-tab-size: 4;
    tab-size: 4;
    -webkit-hyphens: none;
    -ms-hyphens: none;
    hyphens: none;
  }
  pre[class*="language-"] {
    padding: 1em;
    margin: 0.5em 0;
    overflow: auto;
  }
  :not(pre) > code[class*="language-"],
  pre[class*="language-"] {
    background: #2d2d2d;
  }
  :not(pre) > code[class*="language-"] {
    padding: 0.1em;
    border-radius: 0.3em;
    white-space: normal;
  }

  .markdown-body code {
    color: #476582;
    padding: 0.25rem 0.5rem;
    margin: 0;
    font-size: 0.85em;
    background-color: rgba(27, 31, 35, 0.05);
    border-radius: 3px;
  }
  .markdown-body pre,
  .markdown-body pre[class*="language-"] {
    background-color: #282c34;
    line-height: 1.4;
    border-radius: 6px;
    padding: 1.25rem 1.5rem;
    margin: 0.85rem 0;
    white-space: pre-wrap;
    word-break: break-word;
    overflow: auto;
    position: relative;
  }
  .markdown-body pre[class*="language-"] code,
  .markdown-body pre code {
    color: #fff;
    padding: 0;
    background-color: none;
    border-radius: 0;
  }
  .markdown-body pre:before,
  .markdown-body pre[class*="language-"]:before {
    position: absolute;
    top: 0.8em;
    right: 1em;
    font-size: 0.75rem;
    color: hsla(0, 0%, 100%, 0.4);
  }
  .markdown-body .highlighted-line {
    background-color: rgba(0, 0, 0, 0.66);
    display: block;
    margin: 0.1rem -1.5rem 0;
    padding: 0.1rem 1.8rem;
  }
  pre[class="language-javascript"]:before,
  pre[class="language-js"]:before {
    content: "js";
  }
  pre[class="language-html"]:before,
  pre[class="language-markup"]:before {
    content: "html";
  }
  pre[class="language-markdown"]:before,
  pre[class="language-md"]:before {
    content: "md";
  }
  pre[class="language-vue"]:before {
    content: "vue";
  }
  pre[class="language-css"]:before {
    content: "css";
  }
  pre[class="language-sass"]:before {
    content: "sass";
  }
  pre[class="language-less"]:before {
    content: "less";
  }
  pre[class="language-scss"]:before {
    content: "scss";
  }
  pre[class="language-stylus"]:before {
    content: "stylus";
  }
  pre[class="language-json"]:before {
    content: "json";
  }
  pre[class="language-ruby"]:before {
    content: "rb";
  }
  pre[class="language-python"]:before {
    content: "py";
  }
  pre[class="language-go"]:before {
    content: "go";
  }
  pre[class="language-java"]:before {
    content: "java";
  }
  pre[class="language-c"]:before {
    content: "c";
  }
  pre[class="language-bash"]:before {
    content: "sh";
  }
  .custom-block .custom-block-title {
    font-weight: 600;
    margin-bottom: -0.4rem;
  }
  .custom-block.danger,
  .custom-block.tip,
  .custom-block.warning {
    padding: 0.1rem 1.5rem;
    border-left-width: 0.5rem;
    border-left-style: solid;
    margin: 1rem 0;
  }
  .custom-block.tip {
    background-color: #f3f5f7;
    border-color: #42b983;
  }
  .custom-block.warning {
    background-color: rgba(255, 229, 100, 0.3);
    border-color: #e7c000;
    color: #6b5900;
  }
  .custom-block.warning .custom-block-title {
    color: #b29400;
  }
  .custom-block.warning a {
    color: #2c3e50;
  }
  .custom-block.danger {
    background-color: #ffe6e6;
    border-color: #c00;
    color: #4d0000;
  }
  .custom-block.danger .custom-block-title {
    color: #900;
  }
  .custom-block.danger a {
    color: #2c3e50;
  }
  .arrow {
    display: inline-block;
    width: 0;
    height: 0;
  }
  .arrow.up {
    border-bottom: 6px solid #2c3e50;
  }
  .arrow.down,
  .arrow.up {
    border-left: 4px solid transparent;
    border-right: 4px solid transparent;
  }
  .arrow.down {
    border-top: 6px solid #2c3e50;
  }
  .arrow.right {
    border-left: 6px solid #2c3e50;
  }
  .arrow.left,
  .arrow.right {
    border-top: 4px solid transparent;
    border-bottom: 4px solid transparent;
  }
  .arrow.left {
    border-right: 6px solid #2c3e50;
  }
  body,
  html {
    padding: 0;
    margin: 0;
  }
  body {
    font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen,
      Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-size: 16px;
    color: #2c3e50;
  }
  .page {
    padding-left: 20rem;
  }
  .navbar {
    z-index: 20;
    top: 0;
    right: 0;
    height: 3.6rem;
    border-bottom: 1px solid #eaecef;
  }
  .navbar,
  .sidebar {
    position: fixed;
    left: 0;
    background-color: #fff;
    box-sizing: border-box;
  }
  .sidebar {
    font-size: 15px;
    width: 20rem;
    z-index: 10;
    margin: 0;
    top: 3.6rem;
    bottom: 0;
    border-right: 1px solid #eaecef;
    overflow-y: auto;
  }
  .markdown-body:not(.custom) {
    margin: 0 auto;
    padding: 2rem 2.5rem;
  }
  .markdown-body:not(.custom) > :first-child {
    margin-top: 3.6rem;
  }
  .markdown-body:not(.custom) a:hover {
    text-decoration: underline;
  }
  .markdown-body:not(.custom) p.demo {
    padding: 1rem 1.5rem;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  .markdown-body:not(.custom) img {
    max-width: 100%;
  }
  .markdown-body.custom {
    padding: 0;
    margin: 0;
  }
  a {
    font-weight: 500;
    text-decoration: none;
  }
  a,
  p a code {
    color: #3eaf7c;
  }
  p a code {
    font-weight: 400;
  }
  kbd {
    background: #eee;
    border: 0.15rem solid #ddd;
    border-bottom: 0.25rem solid #ddd;
    border-radius: 0.15rem;
    padding: 0 0.15em;
  }
  blockquote {
    font-size: 1.2rem;
    color: #2c3e50;
    border-left: 0.25rem solid #dfe2e5;
    margin-left: 0;
    padding: 1rem;
    background-color: #f3f5f7;
    border-color: #42b983;
    p + p {
      margin-top: 1rem;
    }
  }
  ol,
  ul {
    padding-left: 1.2em;
  }
  strong {
    font-weight: 600;
  }
  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    font-weight: 600;
    line-height: 1.25;
  }
  .markdown-body:not(.custom) > h1,
  .markdown-body:not(.custom) > h2,
  .markdown-body:not(.custom) > h3,
  .markdown-body:not(.custom) > h4,
  .markdown-body:not(.custom) > h5,
  .markdown-body:not(.custom) > h6 {
    margin-top: -3.1rem;
    padding-top: 4.6rem;
    margin-bottom: 0;
  }
  .markdown-body:not(.custom) > h1:first-child,
  .markdown-body:not(.custom) > h2:first-child,
  .markdown-body:not(.custom) > h3:first-child,
  .markdown-body:not(.custom) > h4:first-child,
  .markdown-body:not(.custom) > h5:first-child,
  .markdown-body:not(.custom) > h6:first-child {
    margin-top: -1.5rem;
    margin-bottom: 1rem;
  }
  .markdown-body:not(.custom) > h1:first-child + .custom-block,
  .markdown-body:not(.custom) > h1:first-child + p,
  .markdown-body:not(.custom) > h1:first-child + pre,
  .markdown-body:not(.custom) > h2:first-child + .custom-block,
  .markdown-body:not(.custom) > h2:first-child + p,
  .markdown-body:not(.custom) > h2:first-child + pre,
  .markdown-body:not(.custom) > h3:first-child + .custom-block,
  .markdown-body:not(.custom) > h3:first-child + p,
  .markdown-body:not(.custom) > h3:first-child + pre,
  .markdown-body:not(.custom) > h4:first-child + .custom-block,
  .markdown-body:not(.custom) > h4:first-child + p,
  .markdown-body:not(.custom) > h4:first-child + pre,
  .markdown-body:not(.custom) > h5:first-child + .custom-block,
  .markdown-body:not(.custom) > h5:first-child + p,
  .markdown-body:not(.custom) > h5:first-child + pre,
  .markdown-body:not(.custom) > h6:first-child + .custom-block,
  .markdown-body:not(.custom) > h6:first-child + p,
  .markdown-body:not(.custom) > h6:first-child + pre {
    margin-top: 2rem;
  }
  h1:hover .header-anchor,
  h2:hover .header-anchor,
  h3:hover .header-anchor,
  h4:hover .header-anchor,
  h5:hover .header-anchor,
  h6:hover .header-anchor {
    opacity: 1;
  }
  h1 {
    font-size: 2.2rem;
  }
  h2 {
    font-size: 1.65rem;
    padding-bottom: 0.3rem;
    border-bottom: 1px solid #eaecef;
  }
  h3 {
    font-size: 1.35rem;
  }
  a.header-anchor {
    font-size: 0.85em;
    float: left;
    margin-left: -0.87em;
    padding-right: 0.23em;
    margin-top: 0.125em;
    opacity: 0;
  }
  a.header-anchor:hover {
    text-decoration: none;
  }
  code,
  kbd {
    font-family: source-code-pro, Menlo, Monaco, Consolas, Courier New,
      monospace;
  }
  ol,
  p,
  ul {
    line-height: 1.7;
  }
  table {
    border-collapse: collapse;
    margin: 1rem 0;
  }
  tr {
    border-top: 1px solid #dfe2e5;
  }
  tr:nth-child(2n) {
    background-color: #f6f8fa;
  }
  td,
  th {
    border: 1px solid #dfe2e5;
    padding: 0.6em 1em;
  }
  .custom-layout {
    padding-top: 3.6rem;
  }
  .theme-container.no-navbar .markdown-body:not(.custom) h1,
  .theme-container.no-navbar .markdown-body:not(.custom) h2,
  .theme-container.no-navbar .markdown-body:not(.custom) h3,
  .theme-container.no-navbar .markdown-body:not(.custom) h4,
  .theme-container.no-navbar .markdown-body:not(.custom) h5,
  .theme-container.no-navbar .markdown-body:not(.custom) h6 {
    margin-top: 1.5rem;
    padding-top: 0;
  }
  @media (min-width: 720px) {
    .theme-container.no-sidebar .sidebar {
      display: none;
    }
    .theme-container.no-sidebar .page {
      padding-left: 0;
    }
  }
  @media (max-width: 959px) {
    .sidebar {
      font-size: 15px;
      width: 16.4rem;
    }
    .page {
      padding-left: 16.4rem;
    }
    .markdown-body:not(.custom) {
      padding: 2rem;
    }
  }
  @media (max-width: 719px) {
    .sidebar {
      top: 0;
      padding-top: 3.6rem;
      transform: translateX(-100%);
      transition: transform 0.2s ease;
    }
    .page {
      padding-left: 0;
    }
    .theme-container.sidebar-open .sidebar {
      transform: translateX(0);
    }
  }
  @media (max-width: 419px) {
    h1 {
      font-size: 1.9rem;
    }
    .markdown-body:not(.custom) {
      padding: 1.5rem;
    }
    .markdown-body pre,
    .markdown-body pre[class*="language-"] {
      margin: 0.85rem -1.5rem;
      border-radius: 0;
    }
  }
  .example_Ta9ygTaK {
    color: #41b883;
  }
  .emoji{
    display: inline-block;
    min-width: 20px;
    min-height: 20px;
    background-size: cover;
  }
}
</style>