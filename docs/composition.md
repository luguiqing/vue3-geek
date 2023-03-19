## 1. Composition API 好处

### 1.1 对代码组织方式的好处

因为 ref 和 computed 等功能都可以从 Vue 中全局引入（不依赖于上下文this），所以我们就可以把组件进行任意颗粒度的拆分和组合

### 1.2 &lt;script setup&gt; 让代码更精简

```javascript

<script >
// 原先的需要 手动定义 setup方法，且需要return才能在template中使用
import { ref } from "vue";
export default {
  setup() {
    let count = ref(1)
    function add() {
      count.value++
    }
    return {
      count,
      add
    }
  }
}
</script>
```