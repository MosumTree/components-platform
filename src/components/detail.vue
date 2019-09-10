<template>
  <el-container>
    <el-aside width="150px">
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
      <el-main></el-main>
    </el-container>
  </el-container>
</template>

<script>
import componentList from "./componentsList";
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
  }
};
</script>
<style>
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

.el-aside {
  z-index: 199;
  background-color: #d3dce6;
  color: #333;
  text-align: center;
}

.el-main {
  color: #333;
  text-align: center;
  background-color: rgba(232, 217, 217, 0.3);
  /* background: url('../assets/bg.jpeg') 100% 100%; */
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
.aside-title{
  padding: 20px 0;
  background: #409EFF;
  color: #fff;
}
.el-menu {
  height: 100%;
}
</style>