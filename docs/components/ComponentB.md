---
title: ComponentB
comment: false
editLink: false
prev: false
next: false
order: 1
---

## 示例

::: vue-playground ComponentB
@file App.vue

```vue

<script lang="ts" setup>
  import {ComponentB} from 'alphabetical-navigation'
  import {onMounted} from "vue";

  onMounted(() => {
    console.log(ComponentB)
  })
</script>
<template>
  <ComponentB />
</template>

```
@import

```json
{
  "imports": {
    "alphabetical-navigation": "http://localhost:8080/lib/alphabetical-navigation.es.js"
  }
}
```
:::
