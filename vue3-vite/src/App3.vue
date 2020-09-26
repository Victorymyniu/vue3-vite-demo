<template>
  <!-- 实现一个todolist功能 -->
  <div>
    <form>
      <input type="text" v-model="state2.stu.id">
      <input type="text" v-model="state2.stu.name">
      <input type="text" v-model="state2.stu.age">
      <input type="submit" @click="addStu">
    </form>
    <ul>
      <li v-for="(stu,index) in state.stus" :key="stu.id" @click="remStu(index)">
        {{stu.name}}-{{stu.age}}
      </li>
    </ul>
  </div>
</template>

<script>
import { ref, reactive } from 'vue'
export default {
  name: 'App3',
  // setup函数是组合API的入口函数
  setup() {
    // ref函数注意点：
    // ref只能监听简单类型的变化，不能监听复杂类型的变化（对象/数组）

    // let state = reactive({
    //   stus:[
    //     {id:1,name:'zs',age:10},
    //     {id:2,name:'ww',age:20},
    //     {id:3,name:'cc',age:30}
    //   ]
    // })
    // function remStu(index) {
    //   state.stus = state.stus.filter((stu,idx) => idx != index)
    // }
    let {state,remStu} = useRemoveStudent()
    let {state2, addStu} = useAddStudent(state)
    return{state,remStu,state2, addStu}
  }
}
// 上面数据和业务逻辑放进下面方法中，解决vue2.0数据和业务逻辑分散的问题
function useAddStudent(state) {
  let state2 = reactive({
    stu:{
      id: '',
      name: '',
      age: ''
    }
  })
  function addStu(e) {
    e.preventDefault()
    console.log(state2.stu)
    const stu = Object.assign({},state2.stu)
    state.stus.push(stu)
    state2.stu = {
      id: '',
      name: '',
      age: ''
    }
  }
  return{state2, addStu}
}
function useRemoveStudent() {
  let state = reactive({
    stus:[
      {id:1,name:'zs',age:10},
      {id:2,name:'ww',age:20},
      {id:3,name:'cc',age:30}
    ]
  })
  function remStu(index) {
    state.stus = state.stus.filter((stu,idx) => idx != index)
  }
  return{state, remStu}
}
</script>
