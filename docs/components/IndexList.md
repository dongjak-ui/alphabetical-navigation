---
title: IndexList
comment: false
editLink: false
prev: false
next: false
order: 1
---

## 基础用法

::: vue-playground
@file App.vue

```vue

<script lang="ts" setup>
  import {IndexList} from 'vue3-index-list'
  import {ref} from "vue";

  const items = ref([
    {
      "id": 1672,
      "name": "奥迪",
      "pinyin": "A"
    },  {
      "id": 1678,
      "name": "别克",
      "pinyin": "B"
    },   {
      "id": 1895,
      "name": "五十铃",
      "pinyin": "W"
    }, {
      "id": 1705,
      "name": "长城",
      "pinyin": "C"
    },{
      "id": 1727,
      "name": "丰田",
      "pinyin": "F"
    },{
      "id": 1741,
      "name": "广汽传祺",
      "pinyin": "G"
    }, {
      "id": 1779,
      "name": "江淮",
      "pinyin": "J"
    },
    {
      "id": 1695,
      "name": "本田",
      "pinyin": "B"
    },  {
      "id": 1721,
      "name": "大众",
      "pinyin": "D"
    },  {
      "id": 1722,
      "name": "大发",
      "pinyin": "D"
    },  {
      "id": 1723,
      "name": "大运",
      "pinyin": "D"
    },
  ])
</script>
<template>
  <IndexList :items="items" />
</template>
<style>
  @import "http://localhost:8080/lib/style.css";
</style>
```
@import

```json
{
  "imports": {
    "vue3-index-list": "http://localhost:8080/lib/vue3-index-list.es.js"
  }
}
```
:::

## 自定义键模板

::: vue-playground
@file App.vue

```vue

<script lang="ts" setup>
  import {IndexList} from 'vue3-index-list'
  import {ref} from "vue";

  const items = ref([
    {
      "id": 1672,
      "name": "奥迪",
      "pinyin": "A"
    },  {
      "id": 1678,
      "name": "别克",
      "pinyin": "B"
    },   {
      "id": 1895,
      "name": "五十铃",
      "pinyin": "W"
    }, {
      "id": 1705,
      "name": "长城",
      "pinyin": "C"
    },{
      "id": 1727,
      "name": "丰田",
      "pinyin": "F"
    },{
      "id": 1741,
      "name": "广汽传祺",
      "pinyin": "G"
    }, {
      "id": 1779,
      "name": "江淮",
      "pinyin": "J"
    },
    {
      "id": 1695,
      "name": "本田",
      "pinyin": "B"
    },  {
      "id": 1721,
      "name": "大众",
      "pinyin": "D"
    },  {
      "id": 1722,
      "name": "大发",
      "pinyin": "D"
    },  {
      "id": 1723,
      "name": "大运",
      "pinyin": "D"
    },
  ])
</script>
<template>
  <IndexList :items="items" >
    <template v-slot:key="{k}">
      <div :data-en="k">{{k}}</div>
    </template>
  </IndexList>
</template>
<style>
  @import "http://localhost:8080/lib/style.css";
</style>
```
@import

```json
{
  "imports": {
    "vue3-index-list": "http://localhost:8080/lib/vue3-index-list.es.js"
  }
}
```
:::

## 自定义列表项模板

::: vue-playground
@file App.vue

```vue

<script lang="ts" setup>
  import {IndexList} from 'vue3-index-list'
  import {ref} from "vue";

  const items = ref([
    {
      "id": 1672,
      "name": "奥迪",
      "pinyin": "A"
    },  {
      "id": 1678,
      "name": "别克",
      "pinyin": "B"
    },   {
      "id": 1895,
      "name": "五十铃",
      "pinyin": "W"
    }, {
      "id": 1705,
      "name": "长城",
      "pinyin": "C"
    },{
      "id": 1727,
      "name": "丰田",
      "pinyin": "F"
    },{
      "id": 1741,
      "name": "广汽传祺",
      "pinyin": "G"
    }, {
      "id": 1779,
      "name": "江淮",
      "pinyin": "J"
    },
    {
      "id": 1695,
      "name": "本田",
      "pinyin": "B"
    },  {
      "id": 1721,
      "name": "大众",
      "pinyin": "D"
    },  {
      "id": 1722,
      "name": "大发",
      "pinyin": "D"
    },  {
      "id": 1723,
      "name": "大运",
      "pinyin": "D"
    },
  ])
</script>
<template>
  <IndexList :items="items" >
    <template v-slot:item="{item}">
      <a  href="#">{{item}}</a>
    </template>
  </IndexList>
</template>
<style>
  @import "http://localhost:8080/lib/style.css";
</style>
```
@import

```json
{
  "imports": {
    "vue3-index-list": "http://localhost:8080/lib/vue3-index-list.es.js"
  }
}
```
:::


## Props

| 参数         | 说明   | 类型     | 默认值    | 必须 |
|------------|------|--------|--------|----|
| items      | 列表数据 | Array  |        | ✅  |
| indexField | 索引字段 | String | pinyin |    |
| labelField | 显示字段 | String | name   |    |
