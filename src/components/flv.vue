<template>
  <div class="controls">
    <input class="video-url" type="text" v-model="videoUrl" placeholder="示例: https://sf1-hscdn-tos.pstatp.com/obj/media-fe/xgplayer_doc_video/flv/xgplayer-demo-360p.flv" />
    <div class="button" @click="openVideo">播放</div>
  </div>
  <video  ref="refVideo" class="video-js vjs-big-play-centered vjs-fluid" controls preload="auto">
  </video>
</template>

<script setup>
import { ref, onMounted } from "vue";
import Videojs from 'video.js'
import 'video.js/dist/video-js.css'
import "videojs-flvjs-es6";
import "videojs-flash";

const videoUrl = ref("https://sf1-hscdn-tos.pstatp.com/obj/media-fe/xgplayer_doc_video/flv/xgplayer-demo-360p.flv");
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
    flvjs: {
      mediaDataSource: {
        isLive: false,
        cors: true,
        withCredentials: false
      }
    },
    // sources: [{ src: "", type: "video/x-flv" }]
  });
});

function openVideo() {
  videoPlayer.pause();
  videoPlayer.src([{ src: videoUrl.value, type: "video/x-flv" }]);
  videoPlayer.play();
}
</script>

<style scoped>
@import url(./style.css);
</style>