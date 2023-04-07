<template>
  <canvas ref="canvas" class="canvas" width="800" height="600"></canvas>
</template>

<script setup lang="ts">
import { ref, onMounted, reactive } from 'vue'
//1.获取画布和上下文对象
const canvas = ref<HTMLCanvasElement | null>(null)
let ctx = reactive<any>(null)

const initContext = () => {
  if (canvas.value?.getContext) {
    ctx = canvas.value.getContext('2d')
    //画笔线条圆润
    ctx.lineJoin = 'round'
    ctx.lineCap = 'round'
  }
}

const draw = () => {
  ctx.clearRect(0, 0, 800, 600)
  //存档，保持当前坐标位置和上下文对象
  ctx.save()

  ctx.translate(400, 300)
  ctx.rotate(-Math.PI / 2)

  ctx.save()
  //画小时的刻度
  for (let i = 0; i < 12; i++) {
    ctx.beginPath()
    ctx.moveTo(170, 0)
    ctx.lineTo(190, 0)
    ctx.lineWidth = 8
    ctx.strokeStyle = 'gray'
    ctx.stroke()
    ctx.closePath()
    ctx.rotate(Math.PI / 6)
  }
  ctx.restore()

  ctx.save()
  //画数字
  ctx.rotate(Math.PI / 2)
  ctx.font = 'bold 26px 微软雅黑'
  ctx.fillStyle = '#000'
  ctx.textAlign = 'center'
  ctx.textBaseline = 'middle'
  for (let i = 1; i <= 12; i++) {
    let o = ((Math.PI * 2) / 12) * i - Math.PI / 2
    let x = 210 * Math.cos(o)
    let y = 210 * Math.sin(o)
    ctx.fillText(i, x, y)
  }

  ctx.restore()

  ctx.save()
  //画分钟的刻度
  for (let i = 0; i < 60; i++) {
    ctx.beginPath()
    ctx.moveTo(180, 0)
    ctx.lineTo(190, 0)
    ctx.lineWidth = 2
    ctx.strokeStyle = 'gray'
    ctx.stroke()
    ctx.closePath()
    ctx.rotate(Math.PI / 30)
  }
  ctx.restore()

  ctx.save()

  //获取当前时间
  let time = new Date()
  let hour = time.getHours()
  let min = time.getMinutes()
  let sec = time.getSeconds()
  hour = hour >= 12 ? hour - 12 : hour

  //绘制秒针
  ctx.rotate((Math.PI / 30) * sec)
  ctx.beginPath()
  ctx.moveTo(-30, 0)
  ctx.lineTo(190, 0)
  ctx.lineWidth = 2
  ctx.strokeStyle = 'red'
  ctx.stroke()
  ctx.closePath()
  ctx.restore()

  ctx.save()

  //绘制分针
  ctx.rotate((Math.PI / 30) * min + (Math.PI / 1800) * sec)
  ctx.beginPath()
  ctx.moveTo(-20, 0)
  ctx.lineTo(130, 0)
  ctx.lineWidth = 5
  ctx.strokeStyle = 'black'
  ctx.stroke()
  ctx.closePath()
  ctx.restore()

  ctx.save()
  //绘制时针
  ctx.rotate(
    (Math.PI / 6) * hour +
      (Math.PI / 30 / 12) * min +
      (Math.PI / 6 / 60 / 60) * sec
  )
  ctx.beginPath()
  ctx.moveTo(-10, 0)
  ctx.lineTo(80, 0)
  ctx.lineWidth = 8
  ctx.strokeStyle = 'black'
  ctx.stroke()
  ctx.closePath()
  ctx.restore()

  ctx.restore()

  requestAnimationFrame(draw)
}

onMounted(() => {
  initContext()
  draw()
})
</script>

<style lang="less" scoped>
.canvas {
  // position: absolute;
  border: 1px solid black;
  z-index: 10;
  // top: 0;
  // left: 0;
}
</style>
