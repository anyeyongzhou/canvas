<template>
  <div class="ggk">
    <p>{{ innerContext }}</p>
  </div>
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
  ctx.fillStyle = 'rgba(0,0,255,1)'
  ctx.fillRect(300, 200, 100, 100)
  ctx.globalCompositeOperation = 'source-in'
  ctx.fillStyle = 'rgba(255,0,0,1)'
  ctx.fillRect(250, 150, 100, 100)
}
const draw1 = () => {
  let img = new Image()
  img.src = '../public/guaguajiang.webp.jpg'
  img.onload = () => {
    ctx.drawImage(img, 120, 150, 400, 117)
  }
  let isDraw = false
  canvas.value!.onmousedown = () => {
    isDraw = true
  }
  canvas.value!.onmouseup = () => {
    isDraw = false
  }
  canvas.value!.onmousemove = (e) => {
    if (isDraw) {
      let x = e.pageX
      let y = e.pageY
      ctx.globalCompositeOperation = 'destination-out'
      ctx.arc(x, y, 20, 0, Math.PI * 2)

      ctx.fill()
    }
  }
}

let innerContext = ref('')

const dosomething = () => {
  let random = Math.random()
  console.log(random)
  if (random < 0.1) {
    innerContext.value = '恭喜获得一百万'
  } else if (random < 0.5) {
    innerContext.value = '再来一次'
  } else {
    innerContext.value = '谢谢惠顾'
  }
  console.log(innerContext)
}

onMounted(() => {
  initContext()
  dosomething()
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
.ggk {
  width: 600px;
  height: 600px;
  font-size: 30px;
  font-weight: 900;
  text-align: center;
  line-height: 400px;
  overflow: hidden;
  position: absolute;
  left: 0;
  top: 0;
  // z-index: 11;
}
.btn_container {
  position: absolute;
  right: 0;
}
</style>
