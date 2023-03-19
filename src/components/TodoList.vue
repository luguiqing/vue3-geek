<script setup lang="ts">
import { ref, reactive } from "vue";
let count = ref(1)
let todos = reactive({
  obj: {
    a: 1
  },
  c: ref(0)
})
function add(){
    count.value++
}
function change(temp:any, num:any){
    temp.a++
    num++
}
</script>

<template>
  <div>
    <h1 @click="add">{{count}}</h1>
    <h2 @click="change(todos.obj, todos.c)">{{todos.obj.a + '----' + todos.c}}</h2>
  </div>
</template>
<style scoped>
h1  {
  color: red;
}
</style>