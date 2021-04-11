<template>
  <div class="container">
    <global-header :user="user"/>
    <div class="mb-3">
      <label class="form-label">邮箱地址</label>
      <validate-input :rules="emailRules" v-model="emailValue">{{emailValue}}</validate-input>
    </div>
    <column-list :list="list" text='进入'></column-list>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from '@/components/ColumnList.vue'
import GlobalHeader, { UserProps } from '@/components/GlobalHeader.vue'
import ValidateInput, { RulesProp } from '@/components/ValidateInput.vue'

export default defineComponent({
  name: 'App',

  components: {
    ValidateInput,
    GlobalHeader,
    ColumnList
  },

  setup () {
    const currentUser:UserProps = {
      isLogin: true,
      name: 'user',
      id: 2
    }
    const emailRules: RulesProp = [
      { type: 'required', message: '电子邮箱地址不能为空' },
      { type: 'email', message: '电子邮箱格式不正确' }
    ]
    const testData: ColumnProps[] = [
      {
        id: 0,
        title: 'test course',
        description: 'test 专栏， 关注',
        avatar: 'https://i1.wp.com/i.imgur.com/eYA4oAK.png'
      },
      {
        id: 1,
        title: 'test course',
        description: 'test 专栏， 关注',
        avatar: 'https://i1.wp.com/i.imgur.com/eYA4oAK.png'
      },
      {
        id: 2,
        title: 'test course',
        description: 'test 专栏， 关注'
      },
      {
        id: 3,
        title: 'test course',
        description: 'test 专栏， 关注',
        avatar: 'https://i1.wp.com/i.imgur.com/eYA4oAK.png'
      }
    ]
    const emailValue = ref('test@example.com')
    return {
      list: testData,
      user: currentUser,
      emailRules,
      emailValue
    }
  }
})
</script>
