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

const heartPath = new Path2D()

class Heart {
  x: number
  y: number
  color: string
  isIn: boolean
  heartPath!: Path2D
  eventMapList: { hover: never[]; leave: never[] }
  constructor(x: number, y: number) {
    this.x = x
    this.y = y
    this.color = 'red'
    this.isIn = false
    this.eventMapList = {
      hover: [],
      leave: []
    }
    canvas.value!.onmousemove = (e) => {
      let x = e.offsetX
      let y = e.offsetY
      this.isIn = ctx.isPointInPath(heartPath, x, y)
      if (this.isIn) {
        this.eventMapList.hover.forEach((item) => {
          item()
        })
      } else {
        this.eventMapList.leave.forEach((item) => {
          item()
        })
      }
    }
  }
  onHover(fn: string) {
    this.eventMapList.hover.push(fn)
  }
  onLeave(fn: string) {
    this.eventMapList.leave.push(fn)
  }
  setPosition(x: number, y: number) {
    this.x = x
    this.y = y
  }
  draw() {
    this.heartPath = new Path2D()
    this.heartPath.moveTo(this.x, this.y)
    this.heartPath.bezierCurveTo(
      this.x + 50,
      this.y - 50,
      this.x + 100,
      this.y,
      this.x,
      this.y + 50
    )
    this.heartPath.bezierCurveTo(
      this.x - 100,
      this.y,
      this.x - 50,
      this.y - 50,
      this.x,
      this.y
    )
    ctx.save()
    ctx.fillStyle = this.color
    ctx.fill(this.heartPath)

    ctx.restore()
  }
}
let heart: any = null
const draw1 = () => {
  heart = new Heart(100, 100)
  heart.onHover(() => {
    heart.color = 'blue'
  })
  render()
}

const render = () => {
  ctx.clearRect(0, 0, canvas.value?.width, canvas.value?.height)

  heart.draw()
  requestAnimationFrame(render)
}

onMounted(() => {
  initContext()
  draw1()
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
