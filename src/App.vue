

<template>
 <div class="triangle"></div>
 <div style="background: lightblue;">
  <p style="margin-top: 20px;">Hello</p>
</div>
</template>
<script setup lang="ts">
import { ref , onMounted , onUnmounted } from 'vue'
/**
 * onBeforeMount 组件挂载前执行
 * onMounted 组件挂载完成后执行
 * onUpdated 组件更新完成后执行
 * onBeforeUpdate 组件更新前执行
 * onBeforeUnmount 组件卸载前执行
 * onUnmounted 组件卸载完成后执行
 * 
 */
const arr = [1, 2, 6, 4, 5]
JSON.parse(JSON.stringify(arr))

function t(ms: number) {
  return new Promise((resolve) => {
    setTimeout(resolve, ms)
  })
}

async function test() {
  await t(10000)
  console.log(arr)
}
const proxy = new Proxy(arr, {
  set(target, key, value) {
    console.log('set', key, value)
    target[key] = value
    return true
  },
  get(target, key) {
    console.log('get', key)
    return target[key]
  }
})
proxy[0] = 100
console.log(proxy[0]);

const sum = arr.reduce((pre, cur) => {
  return pre + cur
}, 0)
console.log(sum)
const sortedArr = arr.sort((a, b) => a - b)
console.log(sortedArr)
onMounted(() => {
  test()
})
</script>
<style scoped>
.triangle {
  width: 0;
  height: 0;
  border-left: 50px solid #db34c2;   /* 左边框透明 */
  border-right: 50px solid #db34c2;  /* 右边框透明 */
  border-bottom: 100px solid #3498db;    /* 底边有颜色，形成三角形 */
}
.kfj{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  box-sizing: border-box;
}
</style>
