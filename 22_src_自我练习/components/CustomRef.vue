<template>
  <div class="app-box">
    <h4>使用程序员自定义的ref</h4>
    <div class="div_box">
      <input type="text" v-model="keyWord">
      <span>{{ keyWord }}</span>
    </div>
  </div>
</template>

<script>
import { ref, customRef } from 'vue'
export default {
  name: 'App',
  setup() {
    // let keyWord = ref('hello') //使用Vue提供的ref
    let keyWord = myRef('hello', 500) //使用程序员自定义的ref
    //自定义一个ref——名为：myRef
    function myRef(value, delay) {
      let timer
      return customRef((track, trigger) => {
        return {
          get() {
            console.log(`有人从myRef这个容器中读取数据了，我把${value}给他了`)
            track() //通知Vue追踪value的变化（提前和get商量一下，让他认为这个value是有用的）
            return value
          },
          set(newValue) {
            console.log(`有人把myRef这个容器中数据改为了：${newValue}`)
            clearTimeout(timer)
            timer = setTimeout(() => {
              value = newValue
              trigger() //通知Vue去重新解析模板
            }, delay)
          },
        }
      })
    }



    return { keyWord }
  }
}
</script>

<style lang="less" scoped>
.app-box {
  background-color: skyblue;
  border-radius: 10px;
  padding: 10px;

}

.div_box {
  display: flex;
  flex-direction: column;
}
</style>
