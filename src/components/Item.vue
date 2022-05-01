<template>
  <div class="item">
    <div class="choose">
      <!-- 已选日程表示已完成 -->
      <input type="checkbox" :value="thing" v-model="isChecked" id="check" />
      <span>{{ thing }}</span>
    </div>
    <button @click="deleteItems">删除</button>
  </div>
</template>

<script>
export default {
  name: "Item",
  props: ["thing", "removeItem", "getFinished"],
  data() {
    return {
      //收集checkbox数据，只能使用数组
      //使用普通数据，只会收集到true或false两个布尔值
      // isChecked: [],
      isChecked: "",
      //辅助布尔值变量
      a: false,
      checked: false,
    };
  },
  methods: {
    //将当前日程的值返回给List父组件，进而删除掉此日程
    deleteItems() {
      this.removeItem(this.thing, this.isChecked[0]);
    },
    //提交已完成日程
    // submitFinished(e) {
    //   console.log(e);
    //   //使用辅助布尔值变量，这样一来，当单次点击时
    //   this.a = !this.a;
    //   if (this.a === true) return e.target.value;
    // },
    submitFinished() {
      if (this.isChecked == true) {
        return this.thing;
      }
    },
    //这里不再使用v-model，原因看笔记
    //这里就不手搓v-model方法了，直接使用watch属性

    //选中自己
    chooseMyself() {
      this.isChecked = true;
    },
    //取消选中自己
    noChooseMyself() {
      this.isChecked = false;
    },
  },
  watch: {
    isChecked() {
      //isChecked的之一发生改变，就重新判断checkbox是否勾选
      this.getFinished();
    },
  },
};
</script>

<style scoped>
.item {
  position: relative;
  display: inline-block;
  width: 400px;
  height: 50px;
  justify-content: center;
  align-items: center;
  margin-top: 5px;
  border-radius: 5px;
}
.item:hover {
  background-color: rgba(0, 0, 0, 0.1);
}
.item:hover button {
  display: inline-block;
}
.choose {
  display: inline-block;
  line-height: 50px;
  position: absolute;
  left: 5px;
}
.choose span {
  margin-left: 5px;
}
button {
  display: none;
  width: 50px;
  height: 30px;
  position: absolute;
  right: 5px;
  background-color: white;
  border-radius: 5px;
  top: 0;
  bottom: 0;
  margin: auto 0;
  cursor: pointer;
  transition: all 1.5s;
}
button:hover {
  background-color: rgb(12, 241, 123);
}
</style>