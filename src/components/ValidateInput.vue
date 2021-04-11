<template>
  <div class="validate-input-container pb-3">
    <input type="text" class="form-control" :class="{'is-invalid':inputRef.error}" @blur="validate" :value="inputRef.val" @input="updateValue">
    <div class="invalid-feedback" v-if="inputRef.error">{{inputRef.message}}</div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType, reactive, Ref } from 'vue'
const emailReg = /^([A-Za-z0-9_\-.])+@([A-Za-z0-9_\-.])+\.([A-Za-z]{2,4})$/
interface RuleProp {
  type: 'required'|'email';
  message: string;
}
export type RulesProp = RuleProp[]

export default defineComponent({
  name: 'ValidateInput',
  props: {
    rules: Array as PropType<RulesProp>,
    modelValue: String
  },
  setup (props, context) {
    const inputRef = reactive({
      val: props.modelValue || '',
      error: false,
      message: ''
    })
    const Rules = {
      required: (value:string) => value.trim() !== '',
      email: (value:string) => emailReg.test(value)
    }

    const validate = () => {
      if (props.rules) {
        const allPassed = props.rules.every(
          rule => {
            let passed = true
            inputRef.message = rule.message
            passed = Rules[rule.type](inputRef.val)
            return passed
          }
        )
        inputRef.error = !allPassed
      }
    }
    const updateValue = (e:KeyboardEvent) => {
      const targetValue = (e.target as HTMLInputElement).value
      console.log(e)
      inputRef.val = targetValue
      context.emit('updated:modelValue', targetValue)
    }
    return {
      inputRef,
      validate,
      updateValue
    }
  }
})
</script>
