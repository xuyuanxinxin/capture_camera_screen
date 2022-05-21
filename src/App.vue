<script setup lang="ts">
import { onMounted } from "vue";
onMounted(async () => {
  const camera = await navigator.mediaDevices.getUserMedia({
    video: true,
    audio: false,
  });
  const cameraVideo = document.getElementById("camera") as HTMLVideoElement;
  cameraVideo.onloadedmetadata = (_) => {
    cameraVideo.play();
  };
  cameraVideo.srcObject = camera;
});

const getScreen = async () => {
  try {
    const screen = await navigator.mediaDevices.getDisplayMedia({
      video: true,
      audio: true,
    });
    const screenVideo = document.getElementById("screen") as HTMLVideoElement;
    screenVideo.srcObject = screen;
    screenVideo.onloadedmetadata = (_) => {
      screenVideo.play();
    };
  } catch (err) {
    console.error("Error: " + err);
  }
};
</script>

<template>
  <main>
    <div class="inline v-center">
      <h1>摄像头和录屏测试</h1>
      <button @click="getScreen" :style="{ width: '100px', height: '30px' }">
        打开录屏
      </button>
    </div>
    <div class="inline">
      <video id="camera"></video>
      <video id="screen"></video>
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
