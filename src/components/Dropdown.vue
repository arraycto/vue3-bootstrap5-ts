<template>
  <div class="dropdown" ref="dropdownRef">
    <a href="#" @click.prevent="toggleOpen"  class="btn btn-outline-light my-2 dropdown-toggle">{{title}}</a>
    <ul v-if="isOpen" class="dropdown-menu" :style="{display: 'block'}">
      <slot></slot>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent, watch, ref } from 'vue'
import useClickOutside from '@/hooks/useClickOutside'
export default defineComponent({
  name: 'Dropdown',
  props: {
    title: {
      type: String,
      require: true
    }
  },
  setup () {
    const isOpen = ref(false)
    const dropdownRef = ref<null | HTMLElement>(null)
    const toggleOpen = () => {
      isOpen.value = !isOpen.value
    }
    const isClickOutSide = useClickOutside(dropdownRef)
    watch(
      isClickOutSide,
      () => {
        if (isOpen.value && isClickOutSide.value) {
          isOpen.value = false
        }
      }
    )
    return {
      isOpen,
      toggleOpen,
      dropdownRef
    }
  }
})
</script>
