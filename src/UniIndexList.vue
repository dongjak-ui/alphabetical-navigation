<script setup lang="ts">
import {computed, onMounted, ref} from "vue";
import "@dongjak-extensions/lang";
import {MapUtil} from "@dongjak-extensions/lang";

export interface IndexListItem {
  [key: string]: any
}

interface Props {
  items: Array<IndexListItem> | (() => Promise<Array<IndexListItem>>),
  indexField?: string,
  labelField?: string
}

const props = withDefaults(defineProps<Props>(), {
  indexField: 'pinyin',
  labelField: 'name'
})
const finalItems = ref<Array<IndexListItem>>([])
const finalItemsGrouped = computed(() => {
  const res = finalItems.value.groupBy$ext(props.indexField)
      .sortByKeys$ext()
  MapUtil.sortByKeys(res)

  let sortedMap = new Map();
  let sortedKeys = [...res.keys()].sort();
  for (let key of sortedKeys) {
    sortedMap.set(key, res.get(key));
  }
  return sortedMap
})
onMounted(async () => {
  if (typeof props.items === 'function') {
    finalItems.value = (await props.items())
  } else {
    finalItems.value = props.items
  }
})
//右侧指示器dom元素
const charBar = ref<HTMLUListElement>()
//列表项主容器dom元素
const itemsContainer = ref<HTMLDivElement>()
//所有的索引键dom元素
const indexKeyDomElements = ref<Array<{
  key: string,
  el: Element
}>>([])

//用于指定当前是否正处于滑动过程中
const isTouching = ref(false)
const lastChar = ref('A')
const boxClientTop = ref(10)
const getChar = (clientY: number) => {
  const charList = [...finalItemsGrouped.value.keys()];
  const charHeight = charBar.value!.offsetHeight / charList.length;
  const index = Math.floor((clientY - boxClientTop.value) / charHeight);
  return charList[index];
}
const touchStart = (e: TouchEvent) => {
  e.preventDefault();
  isTouching.value = true;
  const char = getChar(e.touches[0].clientY);
  gotoChar(char);
}
const touchEnd = (e: TouchEvent) => {
  e.preventDefault();
  isTouching.value = false;
}

const touchMove = (e: TouchEvent) => {
  e.preventDefault();
  const char = getChar(e.touches[0].clientY);
  gotoChar(char);
}
const gotoChar = (char: string) => {
  if (char === lastChar.value) {
    return false;
  }
  lastChar.value = char;
  if (char === '*') {
    itemsContainer.value!.scrollTop = 0;
  } else if (char === '#') {
    itemsContainer.value!.scrollTop = itemsContainer.value!.scrollHeight;
  }
  indexKeyDomElements.value.find(item => item.key === char)?.el?.scrollIntoView()
  // const target = document.querySelector('[data-en="' + char + '"]');
  // console.log(target)
  // if (target) {
  //   target.scrollIntoView();
  // }
}

const setIndexKeyDom = (key: string, el: Element) => {
  if (el) {
    indexKeyDomElements.value.push({
      key, el
    })
  }
}

// const handleWheel = (e: MouseEvent) => {
//   // 获取滚动的距离
//   const deltaY = e.deltaY;
//
//   // 获取当前元素的滚动位置
//   const currentScrollTop = charBar.value!.scrollTop;
//
//   // 更新滚动位置
//   charBar.value!.scrollTop = currentScrollTop + deltaY;
// }
</script>
<script lang="ts">
import {defineComponent} from "vue";

export default defineComponent({
  name: 'UniIndexList',
  options: {
    virtualHost: true,
    addGlobalClass: true,
    styleIsolation: 'shared',
  },
})
</script>
<template>
  <div class="flex flex-col h-full">
    <div class="flex-1 overflow-auto relative" ref="itemsContainer">

      <div v-for="k in finalItemsGrouped.keys()" :key="k">

        <div :ref="(el) => setIndexKeyDom(k,el as Element)">
          <slot name="key" :k="k">
          </slot>
        </div>

        <div class="p-y-10px p-x-20px border-b-1px border-b-solid border-b-#ccc text-left"
             v-for="(item,index) in finalItemsGrouped.get(k)" :key="index">
          <slot name="item" :item="item">
            {{ item[props.labelField] }}
          </slot>
        </div>
      </div>

      <div class="p-t-10px fixed right-0 top-0 w-20px h-full m-0 box-border">
        <ul
            @touchstart="e => touchStart(e)"
            @touchmove="e => touchMove(e)"
            @touchend="e => touchEnd(e)"
            class="list-none p-l-0 m-0 flex flex-col h-full box-border"
            ref="charBar"
        >
          <li
              class="flex-1 flex items-center justify-center fs-14px cursor-auto"
              v-for="(char,index) in finalItemsGrouped.keys()"
              :key="index"
          >{{ char }}
          </li>
        </ul>
      </div>
      <div
          class="fixed w-50px h-50px top-0 left-0 right-0 bottom-0 m-auto bg-gray rd-6px color-#fff fs-24px font-700 line-height-50px text-center"
          v-show="isTouching">{{ lastChar }}
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
