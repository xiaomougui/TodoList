<template>
  <div class="warning">
    <div class="judge">
      <span>已有日程{{ thing }}，确定要创建吗？</span>
      <div class="judge-button">
        <button @click="isCreated(true)">确定</button>
        <button @click="isCreated(false)">取消</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Warning",
  props: ["thing", "getCreateSituation"],
  methods: {
    isCreated(isCreated) {
      this.getCreateSituation(isCreated);
    },
  },
};
</script>

<style scoped>
.warning {
  position: absolute;
  width: 100%;
  height: 1000px;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 5;
}
.judge {
  width: 400px;
  height: 200px;
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  margin: 0 auto;
  margin-top: 300px;
  background-color: skyblue;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  border-radius: 8px;
}
.judge-button {
  display: flex;
  justify-content: space-evenly;
  margin-top: 40px;
}
.judge-button button {
  width: 80px;
  height: 40px;
  border-radius: 5px;
  transition: all 1.5s;
  cursor: pointer;
}
.judge-button button:hover {
  background-color: bisque;
}
</style>