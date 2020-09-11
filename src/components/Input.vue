<template>
  <div class="form-item">
    <label>{{formData.label}}<span v-if="formData.required">*</span></label>
    <div class="input-wrap" :class="{'alert-input': formData.validations.$invalid}">
      <input :type="formData.type"
             :value="formData.value"
             :placeholder="formData.placeholder"
             :required="formData.required"
             v-model.trim="formValue"
             v-on:input="$emit('input', $event.target.value)"
      >
    </div>
    <FormAlert :formValidations = formData.validations></FormAlert>
  </div>
</template>

<script>
import FormAlert from './Form-alert'
export default {
  name: 'Input',
  components: { FormAlert },
  data () {
    return {
      formValue: ''
    }
  },
  props: {
    formData: Object,
    submitted: Boolean
  },
  watch: { // Генерируем искусственный инпут при сабмите всей формы для запуска валидации поля, если оно не было заполнено.
    submitted: function () {
      if (!this.formValue) {
        this.$emit('input')
      }
    }
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
    border: 1px gray solid
    border-radius: 5px

    &.alert-input
      border-color: red

    input
      border: none
      outline: none
      width: 100%
</style>
