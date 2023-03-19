> 文档： https://cn.vuejs.org/api/sfc-css-features.html#scoped-css

## 1. 深度选择器

处于 scoped 样式中的选择器如果想要做更“深度”的选择，也即：影响到子组件，可以使用 :deep() 这个伪类：

> tips: 通过 v-html 创建的 DOM 内容不会被作用域样式影响，但你仍然可以使用深度选择器来设置其样式

```
<style scoped>
.a :deep(.b) {
  /* ... */
}
</style>

```

## 2. 插槽选择器

默认情况下，作用域样式不会影响到 <slot/> 渲染出来的内容，因为它们被认为是父组件所持有并传递进来的。使用 :slotted 伪类以明确地将插槽内容作为选择器的目标

```
<style scoped>
:slotted(div) {
  color: red;
}
</style>

```

## 3. 全局选择器

如果想让其中一个样式规则应用到全局，比起另外创建一个 `<style>`，可以使用 :global 伪类来实现 (看下面的代码)：

```
<style scoped>
:global(.red) {
  color: red;
}
</style>
```

## 4. CSS 中的 v-bind()

> 运行时主题切换

单文件组件的 `<style>` 标签支持使用 v-bind CSS 函数将 CSS 的值链接到动态的组件状态：

```
<template>
  <div class="text">hello</div>
</template>

<script>
export default {
  data() {
    return {
      color: 'red'
    }
  }
}
</script>

<style>
.text {
  color: v-bind(color);
}
</style>

```

这个语法同样也适用于 `<script setup>`，且支持 JavaScript 表达式 (需要用引号包裹起来)：

```
<script setup>
const theme = {
  color: 'red'
}
</script>

<template>
  <p>hello</p>
</template>

<style scoped>
p {
  color: v-bind('theme.color');
}
</style>

```