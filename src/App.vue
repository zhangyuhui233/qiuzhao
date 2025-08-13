<template>
  <div class="triangle"></div>
  <div style="background: lightblue;">
    <p style="margin-top: 20px;">Hello</p>
  </div>
  <div class="zhengfangx">
    <div class="zhengfangx1"></div>
    <p id="p1"> 123</p>


  </div>
</template>
<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
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

const obj = {
  name: "zhangsan"

}
function yu(greet: string) {

  console.log(greet, this.name);
}
yu.prototype.say = function () {
  console.log("hello");
}
yu.say()
yu.call(obj, "hello")
const bind = yu.bind(obj)
bind("hello")

yu.apply(obj, ["hello"])
console.log(11);




screen.width
screen.height
console.log(screen.width, screen.height);
window.setTimeout(() => {
  console.log("hello");
}, 1000);

const p = new Promise((resolve) => {
  let time = setTimeout(() => {
      resolve("")
      clearTimeout(time)
    }, 1000);

})

const p1 = window.document.getElementById("p1")
console.log("p1",p1);


function createBatchFetch(batchFn, wait = 50) {
  let queue = [];
  let timer = null;

  return function batchFetch(id) {
    return new Promise((resolve, reject) => {
      queue.push({ id, resolve, reject });

      if (!timer) {
        timer = setTimeout(() => {
          // 收集所有请求的 id
          const ids = queue.map(item => item.id);
          // 拷贝当前队列，防止新请求进来时影响本次批量请求
          const currentQueue = queue;
          queue = [];
          timer = null;

          // 调用批量接口
          batchFn(ids)
            .then(results => {
              // 假设 results 是数组，按 id 顺序对应返回
              results.forEach((result, index) => {
                currentQueue[index].resolve(result);
              });
            })
            .catch(err => {
              currentQueue.forEach(item => item.reject(err));
            });
        }, wait);
      }
    });
  };
}

// 模拟批量请求的函数
function fetchUsersBatch(ids) {
  return new Promise(resolve => {
    setTimeout(() => {
      const results = ids.map(id => ({ id, name: `User${id}` }));
      resolve(results);
    }, 100);
  });
}

// 创建 batchFetch 实例
const batchFetchUsers = createBatchFetch(fetchUsersBatch);

// 调用示例
batchFetchUsers(1).then(console.log); // { id: 1, name: "User1" }
batchFetchUsers(2).then(console.log); // { id: 2, name: "User2" }
batchFetchUsers(3).then(console.log); // { id: 3, name: "User3" }

class Person{
  name:string
  age:number
  constructor(name:string,age:number){
    this.name = name
    this.age = age
  }
  say(){
    console.log("hello");
  }
}
Person.prototype.sayHello = function(){
  console.log("hello4546465",this.name);
}

const p5 = new Person("zhangsan",18)

document.cookie = "name=zhangsan; path=/; max-age=10; Secure; SameSite=Lax";


onMounted(() => {

const p2 = window.document.getElementById("p1")
console.log("p2",p2)
if(p2){
  p2.addEventListener("click",()=>{
    console.log("点击了p1");
  })
}
})

onUnmounted(()=>{
  const p2 = window.document.getElementById("p1")
if(p2){
  p2.removeEventListener("click",()=>{
    console.log("点击了p1");
  })
}
})

const p3 =  {
  value:100,
  add: function add(){
    this.value++
    return this
  }
}
p3.value = 1000

console.log("p3",p3.add().add().value);


function makeCounter() {
  let count = 0;
  return function() {
    count++;
    return count;
  }
}

const counter = makeCounter();
console.log(counter()); // 1
console.log(counter()); // 2




</script>
<style scoped>
.triangle {
  width: 0;
  height: 0;
  border-left: 50px solid #db34c2;
  /* 左边框透明 */
  border-right: 50px solid #db34c2;
  /* 右边框透明 */
  border-bottom: 100px solid #3498db;
  /* 底边有颜色，形成三角形 */
}

.kfj {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  box-sizing: border-box;
}

.zhengfangx {
  width: 200px;
  height: 200px;
  background: #3498db;
}

.zhengfangx1 {
  width: 50%;
  padding-bottom: 50%;
  background: #2ecc71;

}
</style>
