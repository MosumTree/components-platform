<template>
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
      <div class="header-layer">
        <div class="header-layer-wrapper">
          <el-input placeholder="请输入内容" v-model="input5" class="input-with-select">
            <el-select v-model="select" slot="prepend" placeholder="请选择">
              <el-option label="餐厅名" value="1"></el-option>
              <el-option label="订单号" value="2"></el-option>
              <el-option label="用户电话" value="3"></el-option>
            </el-select>
            <el-button type="danger" slot="append" icon="el-icon-search"></el-button>
          </el-input>
          <el-button style="margin-left:20px;" round>登录</el-button>
        </div>
      </div>
    </el-header>
    <el-main>
      <div class="header-layer">
        <div class="header-layer-wrapper">
          <componentList :lists="lists"></componentList>
        </div>
        <div class="header-layer-wrapper">
          <div class="layer-introduction">
            <h1 class="layer-large-title">Portal Components</h1>
            <img src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1567968360274&di=8807e4be87bd9e1fb880a52ab0a72cf3&imgtype=0&src=http%3A%2F%2Fhbimg.b0.upaiyun.com%2F17cbe44aa195ee71a14aeb7656586bc0823af1782b0fa-Lp8LxM_fw658"/>
          </div>
        </div>
      </div>
    </el-main>
    <!-- <el-footer height="80px">Footer</el-footer> -->
  </el-container>
</template>

<script>
import componentList from './componentsList';
export default {
  name: "Home",
  components:{componentList},
  data() {
    return {
      input5: "",
      select: "",
      lists:[]
    };
  },
  beforeMount() {
      this.lists = [{
          componentsGroupName: 'TinyMobile',
          componentsGroupLink: 'hi,'
      }, {
          componentsGroupName: 'PortalUI',
          componentsGroupLink: 'hi,'
      }];
  },
  methods: {
    handleSelect(key, keyPath) {
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
}


.el-main {
  color: #333;
  text-align: center;
  height: 179vw;
  background-color: rgba(232,217,217,.3);
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
.el-input-group__append .el-button, .el-input-group__append .el-select, .el-input-group__prepend .el-button, .el-input-group__prepend .el-select {
    display: inline-block;
    margin: -2px -20px;
}
.el-input-group__append, .el-input-group__prepend {
    background-color: #fb3e44;
    color: #fff;
}

.el-main{
  padding: 0;
}

.layer-introduction{
  width: 100%;
  height: 1000px;
  margin-top: 50px;
  background: #fff;
}
.layer-large-title{
  padding: 20px 0;
  font-size: 50px;
  font-family: 'Do Hyeon', sans-serif;
}
</style>