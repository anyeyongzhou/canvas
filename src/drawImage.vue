<template>
  <canvas ref="canvas" class="canvas" width="600" height="600"></canvas>
</template>

<script setup lang="ts">
import { ref, onMounted, reactive } from 'vue'
const canvas = ref<HTMLCanvasElement | null>(null)
let ctx = reactive<any>(null)
const initContext = () => {
  if (canvas.value?.getContext) {
    ctx = canvas.value.getContext('2d')
  }
}
let img = new Image()
img.src = '../public/meinv.webp.jpg'
img.onload = () => {
  //ctx.drawImage(img, 0, 0)
  //ctx.drawImage(img, 0, 0, 600, 400)
  ctx.drawImage(img, 117, 50, 70, 70, 0, 0, 600, 400)
}
const draw = () => {}

onMounted(() => {
  initContext()
  draw()
})
</script>

<style lang="less" scoped>
.canvas {
  border: 1px solid black;
}
</style>
