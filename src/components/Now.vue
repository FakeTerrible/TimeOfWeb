<template>
  <div class="time">
    {{ time.toLocaleTimeString() }}
    <br>
    {{ time.toLocaleDateString() }}
  </div>
</template>

<script setup>
import { onMounted, onUnmounted, reactive, ref } from "vue";

const time = ref(new Date());
const obj = reactive({ time });

onMounted(function () {
  this.timer = setInterval(function () {
    obj.time = new Date();
  }, 1000);
});

onUnmounted(function(){
  if(this.timer){
    clearInterval(this.timer);
  }
})
</script>

<style scoped>
.time {
  text-align: center;
}
</style>
