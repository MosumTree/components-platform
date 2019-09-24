<template>
  <div class="list-wrapper">
    <ul class="list-content">
      <li v-for="(list, index) in getLists" :key="index">
        <router-link :to="{ path: '/detail', params: { userId: 123 }}">
          <a class="components-link">
            <i class="components-link-icon"></i>
            <p class="components-link-title">{{list.componentsGroupName}}</p>
            <p class="components-link-desc">{{list.componentsGroupDesc}}</p>
          </a>
        </router-link>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "componentsList",
  props: ["lists"],
  data() {
    console.log(this.lists);
    return {
      getLists: this.lists
    };
  },
  mounted() {
    this.getLists.push({
      componentsGroupName: "TinyUI",
      componentsGroupLink: "hi,",
      componentsGroupDesc: "peret sdfasdf sdgas iohi onasefj a aodigguaeee awetf"
    });
  }
};
</script>
<style lang="less">
.list-wrapper {
  width: 100%;
  /* background: rgb(243, 234, 234); */
}
.list-content {
  display: flex;
  justify-content: center;
  align-items: center;
}
.components-link-icon{
  width: 100px;
  height: 100px;
  background: url("../assets/pc.png");
  background-size: 100% 100%;
}
.components-link-icon::after{
  content: '';
    position: absolute;
    top: 120px;
    width: 0;
    height: 38px;
    // border-left: 1px dashed #42b983;
    border-right: 2px dashed #42b983;
}
.list-content li {
  flex: 1;
  padding: 0 10px;
  text-align: center;
  height: 100%;
  line-height: 100%;
}
.list-content li > p {
  font-size: 20px;
  padding: 10px 0;
  font-family: "Do Hyeon", sans-serif;
}
.components-link {
  display: inline-block;
  cursor: pointer;

}
  .components-link-desc{
    font-size: 12px;
  }
  .components-link-title{
    font-size: 20px;
  }
  .components-link i {
    color: #333;
  font-size: 50px;
}
.components-link:hover p {
  color: #42b983;
}
.components-link:hover i {
  font-size: 50px;
  color: #42b983;
}
.list-content li p {
  padding: 10px 0;
  font-family: "Do Hyeon", sans-serif;
  color: #000;
  transition: 0.2s all;
}
.list-content li i {
  display: inline-block;
  margin-top: 10px;
  width: 50px;
  height: 50px;
  font-size: 40px;
  border-radius: 5px;
  margin-bottom: 50px;
  transition: 0.2s all;
}
</style>