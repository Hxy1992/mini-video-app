<template>
  <div class="controls">
    <input class="video-url" type="text" placeholder="示例: https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8"
      v-model="videoUrl" />
    <div class="button" @click="openVideo">播放</div>
  </div>
  <video ref="refVideo" class="video-js vjs-big-play-centered vjs-fluid" controls preload="auto">
  </video>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Videojs from 'video.js'
import 'video.js/dist/video-js.css'
import "videojs-flvjs-es6";
import "videojs-flash";

const videoUrl = ref("https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8");
const refVideo = ref();
let videoPlayer = null;

onMounted(() => {
  videoPlayer = Videojs(refVideo.value, {
    autoplay: 'muted',//自动播放
    controls: true,//用户可以与之交互的控件
    loop: true,//视频一结束就重新开始
    muted: false,//默认情况下将使所有音频静音
    aspectRatio: "16:9",//显示比率
    fullscreen: {
      options: { navigationUI: 'hide' }
    },
    techOrder: ["html5", "flvjs"],// 兼容顺序
    html5: {
      hls: {
        withCredentials: true
      }
    },
    // sources: [{ src: "", type: "application/x-mpegURL" }]
  })
});

function openVideo() {
  videoPlayer.pause();
  videoPlayer.src([{ src: videoUrl.value, type: "application/x-mpegURL" }]);
  videoPlayer.play();
}
</script>

<style scoped>
@import url(./style.css);
</style>