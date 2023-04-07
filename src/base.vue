<template>
  <canvas ref="canvas" class="canvas_container" width="600" height="600">
    你的浏览器不支持canvas,请升级浏览器.浏览器不支持
  </canvas>
</template>

<script setup lang="ts">
import { onMounted, ref, reactive } from 'vue'
const canvas = ref<HTMLCanvasElement | null>(null)
let ctx = reactive<any>({})
const initContext = () => {
  if (canvas.value?.getContext) {
    ctx = canvas.value?.getContext('2d')
  }
}
const drawLine = () => {
  ctx.beginPath()
  ctx.moveTo(100, 100)
  ctx.lineTo(200, 100)
  ctx.stroke()
  ctx.closePath()
}
const drawReactangular = () => {
  ctx.beginPath()
  //绘制一个矩形
  ctx.fillRect(25, 25, 100, 100)
  //清空一个矩形
  ctx.clearRect(45, 45, 60, 60)
  //绘制矩形边框
  ctx.strokeRect(50, 50, 50, 50)

  ctx.closePath()
}
const drawReactangular1 = () => {
  ctx.beginPath()
  //ctx.moveTo(25, 25)
  ctx.rect(25, 25, 100, 100)
  ctx.stroke()
  ctx.closePath()
}
const drawTriangle = () => {
  ctx.beginPath()
  ctx.moveTo(100, 100)
  ctx.lineTo(150, 150)
  ctx.lineTo(50, 150)
  ctx.fill()
}
const drawSmilingFace = () => {
  ctx.beginPath()
  ctx.arc(300, 400, 200, 0, Math.PI * 2, true)
  ctx.moveTo(400, 400)
  ctx.arc(300, 400, 100, 0, Math.PI, false)
  ctx.moveTo(300, 350)
  ctx.arc(250, 350, 50, 0, Math.PI * 2)
  ctx.moveTo(400, 350)
  ctx.arc(350, 350, 50, 0, Math.PI * 2)
  ctx.stroke()
  ctx.closePath()
}
const drawArc = () => {
  ctx.setLineDash([])
  ctx.beginPath()
  ctx.moveTo(150, 20)
  ctx.arcTo(150, 100, 50, 20, 30)
  ctx.stroke()

  ctx.fillStyle = 'blue'
  ctx.fillRect(150, 20, 10, 10)

  ctx.fillStyle = 'red'
  ctx.fillRect(150, 100, 10, 10)
  ctx.fillRect(50, 20, 10, 10)

  ctx.setLineDash([5, 5])
  ctx.moveTo(150, 20)
  ctx.lineTo(150, 100)
  ctx.lineTo(50, 20)
  ctx.stroke()
  ctx.beginPath()
  ctx.arc(120, 38, 30, 0, Math.PI * 2)
  ctx.stroke()
}
onMounted(() => {
  initContext()
  //drawLine()
  //drawReactangular()
  //drawReactangular1()
  //drawTriangle()
  //drawSmilingFace()
  drawArc()
})
</script>

<style lang="less" scoped>
.canvas_container {
  border: 1px solid black;
}
</style>
