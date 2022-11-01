<script setup>
import { convertFileSrc } from '@tauri-apps/api/tauri';
import { open } from '@tauri-apps/api/dialog';

async function openVideo() {
  const selected = await open({
    multiple: false,
    directory: false,
    filters: [{
      name: 'Video',
      extensions: ['mp4', 'webm', 'ogg']
    }]
  });
  if (selected === null) {
    alert('选择为空')
    return
  }
  const assetUrl = convertFileSrc(selected);
  const video = document.getElementById('my-video');
  const sourceList = video.querySelectorAll('source');
  sourceList.forEach(source => source.src = assetUrl)
  video.load();
}
</script>

<template>
  <div class="infos">
    <div class="title">mini播放器</div>
    <div class="button" @click="openVideo">打开视频</div>
  </div>
  <video id="my-video" autoplay controls>
    <source src="" type="video/mp4">
    <source src="" type="video/ogg">
    <source src="" type="video/webm">
  </video>
</template>

<style scoped>
.infos{
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 8px;
  width: 100%;
  height: 50px;
}
.title{
  font-size: 25px;
  line-height: 50px;
}
.button{
  cursor: pointer;
  color: #4980ff;
}
#my-video{
  width: 100%;
  height: calc(100% - 50px);
}
</style>