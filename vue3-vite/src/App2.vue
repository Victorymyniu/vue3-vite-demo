<template>
  <div>{{ count }} {{ object.foo }}</div>
  <p>
    <button @click="myFn">按钮</button>
  </p>
</template>

<script>
import { ref, reactive } from 'vue'
export default {
  name: 'App2',
  // setup函数是组合API的入口函数
  setup() {
    let count = ref(5)
    const object = reactive({foo: 'bar'})
    // 在组合API中定义的变量/方法，要想在外界使用，必须通过return{xxx,xxx} 暴露出去
    function myFn() {
      count.value++
    }
    return {
      count,
      object,
      myFn
    }
  }
}
</script>
