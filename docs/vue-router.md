## 1. 实现方式

```
import {ref,inject} from 'vue'
const ROUTER_KEY = '__router__'
function createRouter(options){
    return new Router(options)
}
function useRouter(){
    return inject(ROUTER_KEY)
}
function createWebHashHistory(){
    function bindEvents(fn){
        window.addEventListener('hashchange',fn)
    }
    return {
        bindEvents,
        url:window.location.hash.slice(1) || '/'
    }
}
class Router{
    constructor(options){
        this.history = options.history
        this.routes = options.routes
        this.current = ref(this.history.url)
        this.history.bindEvents(()=>{
            this.current.value = window.location.hash.slice(1)
        })
    }
    install(app){
        app.provide(ROUTER_KEY,this)
        app.component("router-link",RouterLink)       
        app.component("router-view",RouterView)
    }
}
export {createRouter,createWebHashHistory,useRouter}

```

```vue
// RouterView.vue
<template>
    <component :is="comp"></component>
</template>
<script setup>
import {computed } from 'vue'
import { useRouter } from '../grouter/index'
let router = useRouter()
const comp = computed(()=>{
    const route = router.routes.find(
        (route) => route.path === router.current.value
    )
    return route?route.component : null
})
</script>
```

## 2. vue-router 实战要点
