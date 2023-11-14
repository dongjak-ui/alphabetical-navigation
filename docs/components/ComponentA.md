---
title: ComponentA
comment: false
editLink: false
prev: false
next: false
order: 1
---

## 示例

::: vue-playground ComponentA
@file App.vue

```vue

<script lang="ts" setup>
  import {ComponentA} from 'alphabetical-navigation'
  import {onMounted} from "vue";

  onMounted(() => {
    console.log(ComponentA)
  })
</script>
<template>
  <ComponentA />
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
