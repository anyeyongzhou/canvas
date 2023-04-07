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
  //文字样式
  ctx.font = '100px Microsoft YaHei'
  ctx.textAlign = 'center'
  ctx.textBaseline = 'top'
  ctx.direction = 'rtl'
  const text = ctx.measureText('Hello!')
  console.log(text)
  //ctx.fillText('汪全玉', 150, 300, 100)
  ctx.strokeText('Hello!', 300, 300)
  ctx.arc(300, 300, 5, 0, Math.PI * 2, true)

  ctx.fill()
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
