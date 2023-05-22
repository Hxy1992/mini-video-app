<template>
  <div class="infos">
    <div class="title">播放类型：</div>
    <select v-model="videoType">
      <option value="local">本地视频</option>
      <!-- <option value="rtmp">RTMP</option> -->
      <option value="hls">HLS</option>
      <option value="flv">FLV</option>
    </select>
  </div>
  <div class="box-video">
    <local v-if="videoType == 'local'" />
    <rtmp v-else-if="videoType == 'rtmp'" />
    <hls v-else-if="videoType == 'hls'" />
    <flv v-else-if="videoType == 'flv'" />
  </div>
</template>

<script setup>
import { ref } from "vue";
import local from "./local.vue";
import rtmp from "./rtmp.vue";
import hls from "./hls.vue";
import flv from "./flv.vue";
const videoType = ref("local");
</script>

<style scoped>
.infos{
  display: flex;
  justify-content: flex-start;
  align-items: center;
  padding: 0 8px;
  width: 100%;
  height: 50px;
}
.title{
  font-size: 20px;
  line-height: 50px;
}
.box-video{
  width: 100%;
  height: calc(100% - 50px);
}
</style>