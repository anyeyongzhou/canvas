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

const heartPath = new Path2D()
const draw = () => {
  //console.log(heartPath)
  ctx.beginPath()
  heartPath.moveTo(300, 200)
  heartPath.bezierCurveTo(350, 150, 400, 200, 300, 250)
  heartPath.bezierCurveTo(200, 200, 250, 150, 300, 200)
  //ctx.stroke(heartPath)

  heartPath.moveTo(200, 300)
  heartPath.quadraticCurveTo(150, 300, 150, 200)
  heartPath.quadraticCurveTo(150, 100, 300, 100)
  heartPath.quadraticCurveTo(450, 100, 450, 200)
  heartPath.quadraticCurveTo(450, 300, 250, 300)
  heartPath.quadraticCurveTo(250, 350, 150, 350)
  heartPath.quadraticCurveTo(200, 350, 200, 300)
  ctx.stroke(heartPath)
  //ctx.fill(heartPath)
  heartPath.closePath()
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
