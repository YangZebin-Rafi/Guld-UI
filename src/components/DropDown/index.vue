<template>
  <div class="it-select" @click="openSelect">
    <span class="it-select-input">{{ fillName }}</span>
    <icon-quill:chevron-down :class="['triangle-down', { rotate: rotate }]" />
    <div :class="[
      'it-select-options-panel',
      showOptions ? 'show' : 'hidden',
    ]">
      <p class="it-select-option" v-for="(item, idx) in options" :key="idx" @click="getValue(item)">
        {{ item.title }}
      </p>
    </div>
  </div>
</template>

<script setup  lang="ts">
import { ref } from 'vue'
//针对typescript，可以用这种
const { options } = defineProps<{
  options: ({title: string, id: string})[]
}>()

// let options:any=[]
// const props = defineProps({
//   options: {
//     type: Array
//   }
// })

let fillName = ref()
let rotate = ref(false)
let showOptions = ref(false)

const openSelect = ():void => {
  console.log(111);
  showOptions.value = !showOptions.value
  rotate.value = !rotate.value
}
const getValue = (item:any):void => {
  fillName.value = item.title
  console.log('title,id::', item);
}
</script>

<style scoped lang="scss">
.it-select {
  width: 100px;
  height: 30px;
  border: 1px solid rgba(0, 22, 93, 0.2);
  box-shadow: none !important;
  border-radius: 10px;
  position: relative;
  display: flex;

  .it-select-input {
    width: calc(100% - 20px);
    height: 100%;
    line-height: 100%;
    text-align: center;
    cursor: pointer;
    border: none;
    padding: 0 10px;
    display: flex;
    align-items: center;
  }

  .triangle-down {
    width: 10;
    height: 10;
    position: absolute;
    top: 50%;
    right: 8px;
    transform: translateY(-50%) rotate(0deg);
    transition: transform 0.3s ease-in-out;
  }

  .rotate {
    transform: translateY(-50%) rotate(180deg);
  }

  .it-select-options-panel {
    position: absolute;
    width: 100%;
    top: calc(100% + 15px);
    left: 0;
    background: #ffffff;
    box-shadow: 0px 0px 15px rgba(32, 110, 242, 0.15);
    border-radius: 10px;
    max-height: 264px;
    overflow-y: auto;
    overflow-x: hidden;
    z-index: 99;

    .it-select-option {
      padding: 0 22px;
      cursor: pointer;
      height: 44px;
      line-height: 44px;
      font-size: 18px;
      color: #333333;
      text-align: center;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }

    .it-select-option.check {
      color: #206ef2;
      background: #f5f7fe;
    }

    .it-select-option:hover {
      background: #f5f7fe;
      color: #206ef2;
    }
  }

  .show {
    display: block;
    // animation-duration: .4s;
    // animation-name:down;
    // transform: translateY(100%);
  }

  .hidden {
    display: none;
    // animation-duration: .4s;
    // animation-name: up;
    // transform: translateY(0%);
  }

  @keyframes down {
    from {
        transform: translateY(0%);
    }

    to {
        transform: translateY(100%);
    }
  }

  @keyframes up {
    from {
        transform: translateY(100%);
    }

    to {
        transform: translateY(0%);
    }
  }
}
</style>

