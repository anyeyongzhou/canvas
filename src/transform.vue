<template>
  <canvas ref="canvas" class="canvas" width="600" height="600"></canvas>
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

const draw = () => {
  ctx.transform(1, 1, -1, 1, 100, 100)
  ctx.fillRect(0, 0, 50, 50)
}

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
