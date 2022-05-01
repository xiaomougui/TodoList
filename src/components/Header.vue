<template>
  <div class="schedule">
    <input
      type="text"
      v-model="information"
      @keydown.enter="setItem"
      required
    />
    <label>输入并按下回车创建日程</label>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: ["setInformation"],
  data() {
    return {
      information: "",
      //设置日程的个数，独立于未完成的个数
      //辅助日程数，解决无法连续设置相同日程的问题
      setNumber: 0,
    };
  },
  methods: {
    //设置日程，通过父组件，将日程的信息传递出去
    setItem() {
      this.setNumber++;
      this.setInformation(this.information, this.setNumber);
    },
  },
};
</script>

<style scoped>
.schedule {
  display: inline-block;
  margin-top: 60px;
  position: relative;
}
.schedule input {
  font-size: 20px;
  width: 400px;
  height: 40px;
  border: none;
  outline: none;
  color: green;
  border-bottom: 2px solid skyblue;
}
.schedule label {
  position: absolute;
  top: 0;
  left: 0;
  padding: 10px 0;
  color: black;
  pointer-events: none;
  transition: all 0.6s;
}
.schedule input:focus + label,
.schedule input:valid + label {
  top: -18px;
  font-size: 12px;
  color: skyblue;
}
</style>