<template>
  <div>
    <el-container class="home-first-screen">
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
        <div class="header-layer home-first-screen-title">
          <div class="header-layer-wrapper">
            <div class="layer-introduction">
              <h1 class="layer-large-title">Portal Components</h1>
              <p
                class="layer-introduction-desc"
              >The components platform of the cui the components platform of the cui</p>
            </div>
          </div>
        </div>
        <div class="header-layer">
          <div class="header-layer-wrapper search-wrapper">
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
        <div class="header-layer components-layer">
          <div class="header-layer-wrapper">
            <componentList :lists="lists"></componentList>
          </div>
        </div>
      </el-main>
      <!-- <el-footer height="80px">Footer</el-footer> -->
    </el-container>
  </div>
</template>

<script>
import componentList from "./componentsList";
import "swiper/dist/css/swiper.css";
import { swiper, swiperSlide } from "vue-awesome-swiper";
export default {
  name: "Home",
  components: {
    componentList,
    swiper,
    swiperSlide
  },
  data() {
    return {
      input5: "",
      select: "",
      lists: [],
      swiperOption: {
        initialSlide: 0,
        direction: "vertical",
        navigation: {
          nextEl: "null",
          prevEl: "null"
        },
        autoplay: true,
        effect: "fade"
        // some swiper options/callbacks
        // 所有的参数同 swiper 官方 api 参数
        // ...
      },
      callback: {}
    };
  },
  beforeMount() {
    this.lists = [
      {
        componentsGroupName: "TinyMobile",
        componentsGroupLink: "hi,",
        componentsGroupDesc:
          "peret sdfasdf sdgas iohi onasefj a aodigguaeee awetf"
      },
      {
        componentsGroupName: "PortalUI",
        componentsGroupLink: "hi,",
        componentsGroupDesc:
          "peret sdfasdf sdgas iohi onasefj a aodigguaeee awetf"
      }
    ];
  },
  methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
    }
  },
  computed: {
    swiper() {
      return this.$refs.mySwiper.swiper;
    }
  },
  mounted() {
    // current swiper instance
    // 然后你就可以使用当前上下文内的swiper对象去做你想做的事了
    console.log("this is current swiper instance object", this.swiper);
    this.swiper.slideTo(3, 1000, false);
  }
};
</script>
<style scoped  lang="less">
.home-first-screen {
  height: 100vh;
  width: 100%;
  background: url("../assets/bg6.jpg");
  background-size: cover;
  .el-icon-menu,.header-title {
    color: lightgreen;
  }
}
.el-header,
.el-footer {
  color: #fff;
  text-align: center;
  padding: 0;
  z-index: 99;
}

.el-main {
  color: #fff;
  text-align: center;
  height: 179vw;
  .home-first-screen-title {
    height: 200px;
    margin-top: 150px;
    .layer-introduction {
      width: 100%;
      text-align: center;
      .layer-large-title {
        padding: 20px 0;
        font-size: 80px;
        font-family: "Do Hyeon", sans-serif;
      }
    }
  }
  .search-wrapper {
    padding: 35px 250px;
    box-sizing: border-box;
    background: #fff;
    border-radius: 10px;
  }
  .components-layer {
    background: #fff;
    position: absolute;
    bottom: 0;
    width: 100%;
    padding: 50px 0;
  }
}
.home-second-screen {
  width: 100%;
  height: 600px;
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
  max-width: 1440px;
  height: 100%;
  display: flex;
  align-items: center;
}
.header-title {
  padding: 0 50px;
  text-align: left;
  flex: 1;
}
.header-navigation {
  li {
    float: left;
    margin-left: 20px;
    cursor: pointer;
  }
  li:hover {
    color: lightgreen;
  }
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
}

.home-swiper-wrapper {
  height: 200px;
  width: 100%;
  height: 100%;
  .swiper-container {
    width: 100%;
    height: 100%;
  }
}
</style>