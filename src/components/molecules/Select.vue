<template>
  <div class="form-item">
    <label>{{formData.label}}<span v-if="formData.required">*</span></label>
    <div class="input-wrap" :class="{'alert-input': validations.$invalid && validations.$dirty}">
      <select :value="formData.value"
              :required="formData.required"
              :multiple="formData.multipleSelect"
              v-model="formValue"
              v-on:input="checkInput($event.target.value)"
      >
        <option v-for="(option, index) in formData.options"
                :key="index"
        >
          {{option}}
        </option>
      </select>
    </div>
    <FormAlert :formValidations = validations></FormAlert>
  </div>
</template>

<script>
import FormAlert from '../atoms/Form-alert'
export default {
  name: 'Select',
  components: { FormAlert },
  data () {
    return {
      formValue: []
    }
  },
  props: {
    formData: Object,
    validations: Object
  },
  methods: {
    checkInput: function (value) {
      this.$emit('input', value)
      this.validations.$touch()
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

      select
        border: none
        outline: none
        width: 100%

    .alert-input
      border-color: red
</style>
