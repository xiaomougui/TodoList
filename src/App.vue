<template>
  <div id="app">
    <h1>日程表1.0版</h1>
    <Warning
      v-show="isRepeat"
      :thing="todothing"
      :getCreateSituation="getCreateSituation"
    ></Warning>
    <Header ref="Header" :setInformation="getInformation"></Header>
    <List
      ref="List"
      :todothing="todothing"
      :number="setNumber"
      :isCreated="isCreated"
      :getAll="getAll"
      :finishNumber="getFinish"
      :getRepeatSituation="getRepeatSituation"
      :getCreateSituation="getCreateSituation"
    ></List>
    <Footer
      ref="Footer"
      :finished="finished"
      :all="all"
      :deleteFinish="deleteFinish"
      :chooseAllItems="chooseAllItems"
      :chooseNoItems="chooseNoItems"
    ></Footer>
    <br />
    <br />
    <br />
    <br />
    <br />
    <h1>2.0版本即将发布</h1>
    <h1>敬请期待</h1>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Item from "./components/Item.vue";
import List from "./components/List.vue";
import Footer from "./components/Footer.vue";
import Warning from "./components/Warning.vue";
export default {
  name: "App",
  data() {
    return {
      //日程的信息
      todothing: "",
      //辅助日程数，解决无法连续设置相同日程的问题
      setNumber: 0,
      //全部日程的个数
      all: 0,
      //已完成日程的个数
      finished: 0,
      //是否重复，如果重复，弹出选择框
      isRepeat: false,
      //是否创建，正常情况下，正常创建，有重复，用户决定
      isCreated: false,
    };
  },
  components: {
    Header,
    Item,
    List,
    Footer,
    Warning,
  },
  methods: {
    getInformation(a, b) {
      this.todothing = a;
      this.setNumber = b;
      // console.log(a);
    },
    //得到当前日程的总个数
    getAll(a) {
      // console.log(a);
      this.all = a;
    },
    deleteFinish() {
      // console.log(668);
      this.$refs.List.deleteFinishItems();
    },
    //得到当前已完成日程的个数
    getFinish(a) {
      this.finished = a;
    },
    //得到当前日程是否重复
    getRepeatSituation(isRepeat) {
      this.isRepeat = isRepeat;
    },
    //得到当前日程是否创建
    getCreateSituation(isCreated) {
      this.isCreated = isCreated;
      this.isRepeat = false;
    },
    //选中全部日程
    chooseAllItems() {
      this.$refs.List.chooseAllCheckbox();
    },
    //全部取消选中
    chooseNoItems() {
      this.$refs.List.chooseNoCheckbox();
    },
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  list-style: none;
  text-decoration: none;
}
button {
  padding: 3px 3px;
}
#app {
  font-size: 20px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
