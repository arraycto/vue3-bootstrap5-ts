<template>
  <li class="dropdown-option" :class="{'is-disabled':disabled}">
    <slot></slot>
  </li>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'DropdownItem',
  props: {
    disabled: {
      type: Boolean,
      require: false
    }
  }
})
</script>
<style>
.dropdown-option.is-disabled *{
  pointer-events: none;
  color: grey;
  background-color: transparent;
}
</style>
