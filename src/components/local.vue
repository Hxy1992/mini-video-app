<template>
  <div class="controls">
    <div class="button" @click="openVideo">打开</div>
  </div>
  <video id="my-video" class="video-js" autoplay controls>
    <source src="" type="video/mp4">
    <source src="" type="video/ogg">
    <source src="" type="video/webm">
  </video>
</template>

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

<style scoped>
@import url(./style.css);
</style>