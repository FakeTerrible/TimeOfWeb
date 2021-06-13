<template>
  <div class="music" :key="data">
    
    <div class="name">{{ !!data && data.name }}</div>
    <el-image style="width:300px; height:200px; " :src="data.picurl"  :fit="contain"></el-image>
    <audio @ended="overAudio" ref="audioRef" controls autoplay="autoplay">
      <source :src="data.url">
    </audio>
    <el-button @click="btnClick">下一首</el-button>
  </div>
</template>

<script setup>
import {ref,reactive} from 'vue'
import axios from "axios";
import _ from 'lodash'

const data = ref({});
const obj = reactive({ data });

function next(){
  axios.get("https://api.uomg.com/api/rand.music?sort=热歌榜&format=json")
  .then(function(response){
      return response;
  })
  .then(function(d){
      obj.data = d.data.data;
  });
}

next()

const overAudio = function(){
  console.log('播放声音完毕');
  next();
}

const btnClick = _.debounce(next, 500);
</script>

<style scoped>
.music{
  width: 100%;
  display: flex;
  position: absolute;
  bottom: 1vh;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.name{
  width: 100px;
  height: 30px;
  font-size: 28px;
  text-align: center;
  line-height: 30px;
}
</style>