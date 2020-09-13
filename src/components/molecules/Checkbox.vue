<template>
  <div class="form-item">
    <label>{{formData.label}}<span v-if="formData.required">*</span></label>
    <div class="input-wrap">
      <input type="checkbox"
             :value="formData.value"
             :required="formData.required"
             v-model="formValue"
             v-on:input="$emit('input', $event.target.checked)"
      >
    </div>
    <FormAlert :formValidations = validations></FormAlert>
  </div>
</template>

<script>
import FormAlert from '../atoms/Form-alert'
export default {
  name: 'Checkbox',
  components: { FormAlert },
  data () {
    return {
      formValue: ''
    }
  },
  props: {
    formData: Object,
    validations: Object
  }
}
</script>

<style lang="sass" scoped>
.form-item
  display: flex
  flex-direction: column
  padding: 10px

  label
    margin-bottom: 10px

  .input-wrap
    padding: 10px

    input
      border: none
      outline: none
</style>
