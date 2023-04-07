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
  ctx.fillStyle = 'red'
  ctx.fillRect(0, 0, 100, 100)
  ctx.save()

  ctx.fillStyle = 'blue'
  ctx.fillRect(100, 100, 100, 100)
  ctx.save()

  ctx.fillStyle = 'yellow'
  ctx.fillRect(200, 200, 100, 100)
  ctx.save()

  ctx.fillStyle = 'green'
  ctx.fillRect(300, 300, 100, 100)
  ctx.save()

  ctx.restore()
  ctx.restore()
  ctx.restore()
  ctx.fillRect(400, 400, 100, 100)
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
