<template>
  <canvas ref="canvas" class="canvas" width="600" height="600"></canvas>
  <video src="../public/波涛.mp4" controls ref="video" hidden></video>
  <button ref="btn" @click="dosomething" id="btn">播放/暂停</button>
</template>

<script setup lang="ts">
import { ref, onMounted, reactive, VideoHTMLAttributes } from 'vue'
const canvas = ref<HTMLCanvasElement | null>(null)
let ctx = reactive<any>(null)
const initContext = () => {
  if (canvas.value?.getContext) {
    ctx = canvas.value.getContext('2d')
  }
}
// let video = document.createElement('video')
// video.src = '../public/波涛.mp4'
let video = ref<HTMLVideoElement>()
let img = new Image()
img.src = '../public/logo1.jpg'
//let btn = ref<HTMLButtonElement>()

const dosomething = () => {
  if (video.value?.paused) {
    video.value?.play()
    render()
  } else {
    video.value?.pause()
  }
}
const render = () => {
  ctx.drawImage(video.value, 0, 0, 600, 400)
  ctx.drawImage(img, 500, 350, 100, 50)
  requestAnimationFrame(render)
}

const draw = () => {}

onMounted(() => {
  initContext()
  draw()
  //playout()
})
</script>

<style lang="less" scoped>
.canvas {
  border: 1px solid black;
}
</style>
