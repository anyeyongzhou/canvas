<template>
  <canvas ref="canvas" class="canvas" width="600" height="600"></canvas>
</template>

<script setup lang="ts">
import { ref, onMounted, reactive, VideoHTMLAttributes, Ref } from 'vue'
const canvas = ref<HTMLCanvasElement | null>(null)
let ctx = reactive<any>(null)
const initContext = () => {
  if (canvas.value?.getContext) {
    ctx = canvas.value.getContext('2d')
  }
}

const draw = () => {
  let img = new Image()
  img.src = '../public/meinv.webp.jpg'
  img.onload = () => {
    ctx.drawImage(img, 117, 50, 70, 70, 0, 0, 600, 400)
    let imageDta = ctx.getImageData(0, 0, 600, 400)
    console.log(imageDta)
    for (let i = 0; i < imageDta.data.length; i += 4) {
      // let avg =
      //   (imageDta.data[i] + imageDta.data[i + 1] + imageDta.data[i + 2]) / 3
      // imageDta.data[i] = avg
      // imageDta.data[i + 1] = avg
      // imageDta.data[i + 2] = avg
      // imageDta.data[i + 3] = 255

      imageDta.data[i] = 255 - imageDta.data[i]
      imageDta.data[i + 1] = 255 - imageDta.data[i + 1]
      imageDta.data[i + 2] = 255 - imageDta.data[i + 2]
      imageDta.data[i + 3] = 255
    }
    ctx.putImageData(imageDta, 0, 0)
  }
}

onMounted(() => {
  initContext()
  draw()
})
</script>

<style lang="less" scoped>
.canvas {
  position: absolute;
  border: 1px solid black;
  z-index: 10;
  top: 0;
  left: 0;
}
</style>
