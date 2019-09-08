<template>
  <div class="list-wrapper">
    <ul class="list-content">
      <li v-for="(list, index) in getLists" :key="index" >
        <p>{{list.componentsGroupName}}</p>
        <i></i>
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
  mounted(){
    this.getLists.push({
        componentsGroupName: 'TinyUI',
        componentsGroupLink: 'hi,'
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
.list-content{
    display: flex;
    justify-content: center;
    align-items: center;
}
.list-content li{
    flex: 1;
    padding: 0 10px;
    text-align: center;
    height: 100%;
    line-height: 100%;
}
.list-content li>p{
    padding: 10px 0;
}
.list-content li>i{
    display: inline-block;
    margin-top: 10px;
    width: 50px;
    height: 50px;
    border-radius: 5px;
    background: lightcoral;
}
</style>