<template>
  <div>
    <el-button @click="show = !show">Time</el-button>

    <div
      style="
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 20px;
        margin-left: 20px;
        height: 100px;
      "
      :key="time"
    >
      <transition name="el-fade-in-linear">
        <div v-show="show" class="transition-box">
          {{ time.toLocaleTimeString() }}
        </div>
      </transition>
      <transition name="el-fade-in">
        <div v-show="show" class="transition-box">
          {{ time.toLocaleDateString() }}
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    show: true,
    time: new Date(),
  }),
  mounted() {
    let _this = this; // 声明一个变量指向Vue实例this，保证作用域一致
    this.timer = setInterval(() => {
      _this.time = new Date(); // 修改数据date
    }, 1000)
  },
  unmounted() {
    if (this.timer) {
      clearInterval(this.timer); // 在Vue实例销毁前，清除我们的定时器
    }
  },
};
</script>

<style>
.transition-box {
  margin-bottom: 10px;
  width: 200px;
  height: 100px;
  border-radius: 4px;
  background-color: #409eff;
  text-align: center;
  color: #fff;
  padding: 40px 20px;
  box-sizing: border-box;
  margin-right: 20px;
}
</style>
