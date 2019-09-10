<template>
  <div class="list-wrapper">
    <ul class="list-content">
      <li v-for="(list, index) in getLists" :key="index">
        <router-link :to="{ path: '/detail', params: { userId: 123 }}">
          <a class="components-link">
            <p>{{list.componentsGroupName}}</p>
            <i class="el-icon-star-on"></i>
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
      componentsGroupLink: "hi,"
    });
  }
};
</script>
<style scoped>
.list-wrapper {
  width: 100%;
  height: 100px;
  /* background: rgb(243, 234, 234); */
}
.list-content {
  display: flex;
  justify-content: center;
  align-items: center;
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
.components-link:hover p {
  color: #f56c6c;
}
.components-link:hover i {
  font-size: 50px;
}
.list-content li p {
  font-size: 20px;
  padding: 10px 0;
  font-family: "Do Hyeon", sans-serif;
  color: #000;
  transition: 0.2s all;
}
.list-content li p {
  font-size: 20px;
  padding: 10px 0;
  font-family: "Do Hyeon", sans-serif;
}
.list-content li i {
  display: inline-block;
  margin-top: 10px;
  width: 50px;
  height: 50px;
  font-size: 40px;
  border-radius: 5px;
  transition: 0.2s all;
}
</style>