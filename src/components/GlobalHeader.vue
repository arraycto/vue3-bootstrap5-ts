<template>
  <nav class="navbar navbar-dark bg-primary justify-content-between mb-4 px-4">
    <a href="#" class="navbar-brand">Course</a>
    <ul v-if="!user.isLogin" class="list-inline mb-0">
      <li class="list-inline-item"><a href="#" class="btn btn-outline-light">Login</a></li>
      <li class="list-inline-item"><a href="#" class="btn btn-outline-light">Register</a></li>
    </ul>
    <ul v-else class="list-inline mb-0">
      <li class="list-inline-item">
        <dropdown :title="user.name">
          <dropdown-item>
            <a href="#" class="dropdown-item">新建</a>
          </dropdown-item>
          <dropdown-item disabled>
            <a href="#" class="dropdown-item">编辑</a>
          </dropdown-item>
          <dropdown-item>
            <a href="#" class="dropdown-item">登出</a>
          </dropdown-item>
        </dropdown>
      </li>
    </ul>
  </nav>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import Dropdown from '@/components/Dropdown.vue'
import DropdownItem from '@/components/DropdownItem.vue'
export interface UserProps {
  isLogin:boolean;
  name?:string;
  id?:number;
}

export default defineComponent({
  name: 'GlobalHeader',
  components: { Dropdown, DropdownItem },
  props: {
    user: {
      type: Object as PropType<UserProps>,
      require: true
    }
  }
})
</script>

<style scoped>

</style>
