<template>
  <div class="qloBox">
    <div class="content">
      <div class="flip-container">
        <div class="flip-items" v-for="(unit, unitIndex) in timeArr" :key="unitIndex">
          <div class="item" v-for="(item, index) in unit.max + 1" :key="index"
            :class="{ current: unit.current == index, past: unit.current - 1 == index || index == unit.max && unit.current == 0 }">
            <div class="up">
              <div class="inner">{{ index }}</div>
              <div class="shadow"></div>
            </div>
            <div class="down">
              <div class="inner">{{ index }}</div>
              <div class="shadow"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref, defineComponent, computed ,onBeforeMount,onBeforeUnmount, onMounted } from 'vue'
function getTimeStr(){
  let time = new Date();
  let hour = ('00' + time.getHours()).slice(-2)
  let minute = ('00' + time.getMinutes()).slice(-2)
  let second = ('00' + time.getSeconds()).slice(-2)
  let result = reactive({
    timeStr:hour + minute + second
  })
  console.log('current time',result.timeStr)
  return {
    timeStr:result.timeStr
  }
}
// let timeStr = reactive({getTimeStr})
let { timeStr } = getTimeStr()
console.log('current timeStr' , timeStr)
let timeRunner = reactive({})
const cssVeriables = ref('black')
// cssVeriables.width = '60px'

function setTimeRunner(){
  // timeRunner = setInterval(() => {
  //   timeStr = getTimeStr()
  // }, 1000)
}
console.log('...str' ,...timeStr )
const timeNew = computed(() => {
  return typeof(timeStr) 
})
const cssBacc = ref('black')
const width = ref('120px')
const backgroundColor = ref('#333')
const color = ref('#ccc')
const time = ref('1s')
const height = ref(width*1.5)
const fontSize = ref(width*1.3)
const lineWidth = ref(width / 60)
const radius = ref(width / 60)
const perspective = ref(width * 5)
const gap = ref(width * 0.2)
// --width: 60px;
// --backgroundColor: #333;
// --color: #ccc;
// --time: 1s;
// --height: var(--width) * 1.5;
// --fontSize: var(--width) *1.3;
// --lineWidth: (var(--width) / 60);
// --radius: (var(--width) / 10);
// --perspective: var(--width) * 5;
// --gap: var(--width) * 0.2
const timeArr = computed(() => {  
  return timeStr.split('').map((unit, index) => {
    let max;
    if (index & 1 == 1) {    //时分秒的个位
      max = 9
    } else if (index == 0) { //时十位
      max = 2
    } else if (index == 2) { //分十位
      max = 5
    } else if (index == 4) { //秒十位
      max = 5
    }
    return {
      max,
      current: Number(unit),
    }
  })
})

const FliqloCo = defineComponent({
  // 组件定义
  setup(props) {
  }
})
onBeforeMount(() => {
  setTimeRunner()
})
onMounted(() =>{
  // console.log('computed timeArr',timeArr)
})
onBeforeUnmount(() => {
  clearInterval(timeRunner)
})
defineExpose({
  FliqloCo
})


</script>

<style  scoped>
.qloBox {
  width: 70%;
  height: 70%;
  margin: auto;
}
.flip-container {
  display: flex;
  justify-content: center;
  padding: 0 20rpx;
  position: relative;
}

.flip-items {
  position: relative;
  width: 60rpx;
  height: 90rpx;
  font-size: 78rpx;
  font-weight: bold;
  border-radius: 6rpx;
  box-shadow: 0 2rpx 18rpx rgba(0, 0, 0, 0.7);
}

.flip-items:nth-of-type(2n+1) {
  margin-right: 12rpx;
}

.flip-items:nth-of-type(2), .flip-items:nth-of-type(4) {
  margin-right: 36rpx;
}

.flip-items::after, .flip-items::before {
  position: absolute;
  right: -18rpx;
  content: '';
  transform: translateX(50%);
  width: 8rpx;
  height: 60rpx;
  border-radius: 50%;
  background-color: #333;
}

.flip-items::before {
  top: 25%;
}

.flip-items::after {
  bottom: 25%;
}


</style>