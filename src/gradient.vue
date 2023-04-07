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
let index = 0
const draw = () => {
  ctx.clearRect(0, 0, 600, 400)
  index += 0.01
  if (index > 1) {
    index = 0
  }
  //线性渐变
  let linerGradient = ctx.createLinearGradient(100, 200, 400, 500)
  linerGradient.addColorStop(0, 'red')
  linerGradient.addColorStop(index, '#ffcccc')
  linerGradient.addColorStop(1, 'blue')
  ctx.fillStyle = linerGradient
  ctx.fillRect(100, 200, 300, 300)
  requestAnimationFrame(draw)
}
const draw1 = () => {
  //径向渐变
  let radiaGradient = ctx.createRadialGradient(300, 200, 0, 300, 200, 100)
  radiaGradient.addColorStop(0, 'red')
  radiaGradient.addColorStop(0.3, '#ffcccc')
  radiaGradient.addColorStop(1, 'blue')

  ctx.fillStyle = radiaGradient
  ctx.fillRect(0, 0, 600, 400)
}
//模拟3D球
const draw2 = () => {
  let radiaGradient = ctx.createRadialGradient(250, 150, 10, 300, 200, 100)
  radiaGradient.addColorStop(0, '#ffcccc')
  //radiaGradient.addColorStop(0.3, '#ffcccc')
  radiaGradient.addColorStop(1, 'red')
  ctx.fillStyle = radiaGradient

  ctx.arc(300, 200, 100, 0, Math.PI * 2)

  ctx.fill()
}
//圆锥渐变
const draw3 = () => {
  let coneGradient = ctx.createConicGradient(0, 300, 200)
  coneGradient.addColorStop(0, 'red')
  coneGradient.addColorStop(1, 'blue')
  ctx.fillStyle = coneGradient
  ctx.fillRect(0, 0, 600, 400)
}
onMounted(() => {
  initContext()
  //requestAnimationFrame(draw)
  //draw1()
  //draw2()
  draw3()
})
</script>

<style lang="less" scoped>
.canvas {
  border: 1px solid black;
}
</style>
