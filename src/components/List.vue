<template>
  <div>
    <ul class="ul-style">
      <li v-for="(value, index) of items" :key="index" class="li-style">
        <Item
          ref="Item"
          :thing="value"
          :removeItem="removeItem"
          :getFinished="getFinished"
        ></Item>
      </li>
    </ul>
  </div>
</template>


<script>
import Item from "./Item.vue";

export default {
  name: "List",
  props: [
    "todothing",
    "number",
    "isCreated",
    "getAll",
    "finishNumber",
    "getRepeatSituation",
    "getCreateSituation",
  ],
  data() {
    return {
      items: [],
      sub: 0,
      finishedItems: [],
    };
  },
  components: {
    Item,
  },
  methods: {
    //对比新建日程是否重复
    repeatItems() {
      const a = this.items.indexOf(this.todothing);
      //a>=0表示找到了相同的日程
      if (a >= 0) {
        //重复，用户选择
        this.getRepeatSituation(true);
      } else {
        //没有重复，创建日程
        this.getCreateSituation(true);
      }
    },
    //删除日程
    removeItem(thing, isChecked) {
      const b = this.items.indexOf(thing);
      this.items.splice(b, 1);
      console.log(b);
      //判断是否被选中,如果isChecked不为空
      //则被选中，删除时，同时删除被选中数组中的元素
      if (isChecked != "" && isChecked != undefined) {
        const c = this.finishedItems.indexOf(thing);
        this.finishedItems.splice(c, 1);
      }
      // this.deleteItems();
    },
    getFinished() {
      //清空完成数组，这样做是为了避免之前出现过的已完成日程再次出现
      this.finishedItems = [];
      //遍历一遍Items，找出复选框被选中的Item
      for (let i = 0; i < this.$refs["Item"].length; i++) {
        //利用Item中的submitFinished方法得到被选中的Item的值
        const b = this.$refs["Item"][i].submitFinished();
        if (b != "" && b != undefined) {
          this.finishedItems.unshift(b);
        }
      }
    },
    deleteFinishItems() {
      //遍历所有打钩的项目，并且删除
      for (let i = 0; i < this.finishedItems.length; i++) {
        const b = this.items.indexOf(this.finishedItems[i]);
        this.items.splice(b, 1);
      }
      //删除finishedItems已完成日程中的所有元素
      this.finishedItems = [];
    },
    //选中所有复选框
    chooseAllCheckbox() {
      for (let i = 0; i < this.$refs["Item"].length; i++) {
        //调用每个Item组件的选中自己方法
        console.log(666);
        this.$refs["Item"][i].chooseMyself();
      }
    },
    //取消选中所有复选框
    chooseNoCheckbox() {
      for (let i = 0; i < this.$refs["Item"].length; i++) {
        //调用每个Item组件的选中自己方法
        console.log(666);
        this.$refs["Item"][i].noChooseMyself();
      }
    },
  },
  watch: {
    //辅助日程数，解决无法连续设置相同日程的问题
    number(newValue, oldValue) {
      if (newValue > oldValue) {
        //判断是否重复
        this.repeatItems();
        // //关于先执行if，再对isCreated进行修改的问题
        // if (this.isCreated == true) {
        //   console.log(777);
        // }
      }
    },
    //
    isCreated(newValue, oldValue) {
      if (newValue == true) {
        console.log(newValue);
        this.items.unshift(this.todothing);
        //每回创建完成后将isCreated改为false
        this.getCreateSituation(false);
      }
    },
    //items发生变化，重新统计items内元素个数
    items() {
      //通过得到数组的长度，进而得到全部的日程
      this.getAll(this.items.length);
    },
    //finishedItems一旦发生变化，就重新计算数组长度，也就是元素个数
    finishedItems() {
      //返回已完成日程的个数
      this.finishNumber(this.finishedItems.length);
    },
  },
};
</script>

<style scoped>
.li-style {
  margin: 5px 0;
}
</style>