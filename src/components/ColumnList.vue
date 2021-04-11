<template>
  <div class="row">
    <div v-for="column in list" :key="column.id" class="col-4 mb-3">
      <div class="card h-100 shadow-sm">
        <div class="card-body text-center">
          <img :alt="column.title" :src="column.avatar ? column.avatar:'https://portrait.gitee.com/uploads/avatars/namespace/1764/5294595_talelin_1578992685.png!avatar100'" class="rounded-circle border border-light w-25 my-3">
          <h5 class="card-title">{{ column.title }}</h5>
          <p class="card-text text-left">{{ column.description }}</p>
          <a href="#" class="btn btn-outline-primary">{{text?text:"Enter"}}</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'

export interface ColumnProps {
  id: number;
  title: string;
  avatar?: string;
  description: string;
}

export default defineComponent({
  name: 'ColumnList',
  props: {
    list: {
      type: Array as PropType<ColumnProps[]>,
      required: true
    },
    text: {
      type: String,
      required: false
    }
  }
})
</script>
