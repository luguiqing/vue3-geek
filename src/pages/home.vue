<script setup lang="ts">
import TodoList from '@/components/TodoList.vue';
import { computed } from 'vue';
import {useStore} from'vuex'
let store = useStore()
let count = computed(()=>store.state.count)
function add(){
  store.commit('add')
}
</script>

<template>
  <h1>这是首页</h1>
  <div @click="add">
    store: {{ count }}
  </div>
  <TodoList/>
</template>