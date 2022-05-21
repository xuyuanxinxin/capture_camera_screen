<script setup lang="ts">
import { onMounted, ref } from "vue"
const cameraVideo = ref<HTMLVideoElement>()
const screenVideo = ref<HTMLVideoElement>()
onMounted(async () => {
  const camera = await navigator.mediaDevices.getUserMedia({
    video: true,
    audio: false,
  })
  cameraVideo.value!.onloadedmetadata = _ => cameraVideo.value!.play()
  cameraVideo.value!.srcObject = camera
})

const getScreen = async () => {
  try {
    const screen = await navigator.mediaDevices.getDisplayMedia({
      video: true,
      audio: true,
    })
    screenVideo.value!.srcObject = screen
    screenVideo.value!.onloadedmetadata = _ => screenVideo.value!.play()
  } catch (err) {
    console.error("Error: " + err)
  }
}
</script>

<template>
  <main>
    <div class="inline v-center">
      <h1>摄像头和录屏测试</h1>
      <button @click="getScreen" type="button" class="btn btn-primary">
        打开录屏
      </button>
    </div>
    <div class="inline">
      <video id="camera" ref="cameraVideo"></video>
      <video id="screen" ref="screenVideo"></video>
    </div>
  </main>
</template>

<style>
@import "./assets/base.css";
header {
  line-height: 1.5;
}

#screen,
#camera {
  width: 300px;
  height: 300px;
}
.inline {
  width: 100vw;
  display: flex;
  justify-content: center;
}
.v-center {
  align-items: center;
}
.v-center > button {
  margin-left: 15px;
}
</style>
