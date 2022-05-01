<template>
  <div class="footer">
    <div class="choose">
      <input type="checkbox" v-model="isAll" />
      <span>已完成 {{ finished }} / 全部 {{ all }}</span>
    </div>
    <button @click="deleteFinished">删除已完成的日程</button>
  </div>
</template>

<script>
export default {
  name: "Footer",
  props: ["all", "deleteFinish", "finished", "chooseAllItems", "chooseNoItems"],
  data() {
    return {
      isAll: false,
    };
  },
  methods: {
    deleteFinished() {
      this.deleteFinish();
    },
  },
  watch: {
    isAll() {
      if (this.isAll == true) {
        this.chooseAllItems();
      } else {
        this.chooseNoItems();
      }
    },
  },
};
</script>

<style scoped>
.footer {
  position: relative;
  display: inline-block;
  width: 400px;
  height: 50px;
  justify-content: center;
  align-items: center;
  margin-top: 5px;
  border-radius: 5px;
}
.footer:hover {
  background-color: rgba(0, 0, 0, 0.1);
}
.footer:hover button {
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
  width: 130px;
  height: 30px;
  position: absolute;
  right: 5px;
  border-radius: 5px;
  top: 0;
  bottom: 0;
  margin: auto 0;
  transition: all 1.5s;
}
button:hover {
  background-color: rgb(12, 241, 123);
}
</style>