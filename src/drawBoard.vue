<template>
  <canvas ref="canvas" class="canvas" width="800" height="600"></canvas>
  <hr />
  <button id="boldBtn" type="button" ref="boldBtn" @click="boldBtn_click">
    粗线条
  </button>
  <button id="thinBtn" type="button" ref="thinBtn" @click="thinBtn_click">
    细线条
  </button>
  <button id="saveBtn" type="button" ref="saveBtn" @click="saveBtn_click">
    保存签名
  </button>
  <input
    type="color"
    name=""
    id="color"
    value=""
    ref="color"
    @input="colorChnage"
  />
  <button id="clearBtn" ref="clearBtn" @click="clearBtn_click">橡皮擦</button>
  <button id="nullBtn" ref="nullBtn" @click="nullBtn_click">清空画布</button>
</template>

<script setup lang="ts">
import { ref, onMounted, reactive, Ref } from 'vue'
//1.获取画布和上下文对象
const canvas = ref<HTMLCanvasElement | null>(null)
let ctx = reactive<any>(null)
//2.获取输入框和按钮
//设置画笔的粗细：粗
const boldBtn = ref()
//设置画笔的粗细：细
const thinBtn = ref()
//保存签名
const saveBtn = ref()
//签名颜色选择
const color = ref()
//橡皮擦按钮
const clearBtn = ref()
//清空画布
const nullBtn = ref()
//设置允许绘制的变量
let isDraw = false

const initContext = () => {
  if (canvas.value?.getContext) {
    ctx = canvas.value.getContext('2d')
    //画笔线条圆润
    ctx.lineJoin = 'round'
    ctx.lineCap = 'round'
  }
}

const mouseListner = () => {
  //获取鼠标落下点的位置，将画笔移动到该处
  canvas.value!.onmousedown = (e) => {
    isDraw = true
    ctx.beginPath()
    let x = e.pageX - canvas.value!.offsetLeft
    let y = e.pageY - canvas.value!.offsetTop
    ctx.moveTo(x, y)
    //console.log(x, y)
  }
  canvas.value!.onmousemove = (e) => {
    if (isDraw) {
      let x = e.pageX - canvas.value!.offsetLeft
      let y = e.pageY - canvas.value!.offsetTop
      ctx.lineTo(x, y)
      ctx.stroke()
    }
  }
  //鼠标离开画布结束绘画
  canvas.value!.onmouseleave = () => {
    isDraw = false
    ctx.closePath()
  }
  //鼠标弹起结束绘画
  canvas.value!.onmouseup = () => {
    isDraw = false
    ctx.closePath()
  }
}

const boldBtn_click = () => {
  ctx.globalCompositeOperation = 'source-over'
  ctx.lineWidth = 20
  addClassStyle(boldBtn.value)
}

const thinBtn_click = () => {
  ctx.globalCompositeOperation = 'source-over'
  ctx.lineWidth = 2
  addClassStyle(thinBtn.value)
}

const saveBtn_click = () => {
  let urlData: string | undefined = canvas.value!.toDataURL()
  // let image: HTMLImageElement | undefined = new Image()
  // image.src = urlData
  // document.body.appendChild(image)

  let downloadA = document.createElement('a')
  downloadA.setAttribute('download', '炫酷签名')
  downloadA.href = urlData
  downloadA.click()
}

const clearBtn_click = () => {
  ctx.globalCompositeOperation = 'destination-out'
  ctx.lineWidth = 30
  addClassStyle(clearBtn.value)
}

const nullBtn_click = () => {
  ctx.clearRect(0, 0, 800, 600)
  addClassStyle(nullBtn.value)
}

const addClassStyle = (thisBtn: any) => {
  //console.log(typeof thisBtn)
  boldBtn.value.classList.remove('active')
  thinBtn.value.classList.remove('active')
  clearBtn.value.classList.remove('active')
  nullBtn.value.classList.remove('active')
  thisBtn.classList.add('active')
}

const colorChnage = () => {
  console.log(color.value.value)
  ctx.strokeStyle = color.value.value
}

const draw = () => {}

onMounted(() => {
  initContext()
  mouseListner()
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
button.active {
  color: #fff;
  background-color: orange;
}
</style>
