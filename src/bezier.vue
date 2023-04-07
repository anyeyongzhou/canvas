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
const dracQuadraticBesselCurve = () => {
  ctx.beginPath()
  ctx.moveTo(200, 300)
  ctx.quadraticCurveTo(150, 300, 150, 200)
  ctx.quadraticCurveTo(150, 100, 300, 100)
  ctx.quadraticCurveTo(450, 100, 450, 200)
  ctx.quadraticCurveTo(450, 300, 250, 300)
  ctx.quadraticCurveTo(250, 350, 150, 350)
  ctx.quadraticCurveTo(200, 350, 200, 300)
  ctx.stroke()
  ctx.closePath()
}
const drawCubicBezierCurve = () => {
  ctx.beginPath()
  ctx.moveTo(300, 200)
  ctx.bezierCurveTo(350, 150, 400, 200, 300, 250)
  ctx.bezierCurveTo(200, 200, 250, 150, 300, 200)

  ctx.stroke()
  ctx.closePath()
}
onMounted(() => {
  initContext()
  //dracQuadraticBesselCurve()
  drawCubicBezierCurve()
})
</script>

<style lang="less" scoped>
.canvas {
  border: 1px solid black;
}
</style>
