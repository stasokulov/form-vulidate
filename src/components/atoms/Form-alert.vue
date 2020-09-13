<template>
  <div>
    <!--  Проверка на required запускается только после $dirty=true в Form.vue, а это случается при сабмите формы  -->
    <p v-if="'required' in formValidations && !formValidations.required && formValidations.$dirty" class="alert-subtitle">Обязательное поле</p>
    <!--  Остальные проверки высвечиваются если $invalid=true, т.е. срабатывают при каждом вводе символа в <input>  -->
    <p v-if="'minLength' in formValidations && !formValidations.minLength && formValidations.$invalid" class="alert-subtitle">Мало символов</p>
    <p v-if="'maxLength' in formValidations && !formValidations.maxLength && formValidations.$invalid" class="alert-subtitle">Много символов</p>
    <p v-if="'alpha' in formValidations && !formValidations.alpha && formValidations.$invalid" class="alert-subtitle">Допускаются только латинские буквы</p>
    <p v-if="'latinAndCyrillic' in formValidations && !formValidations.latinAndCyrillic && formValidations.$invalid" class="alert-subtitle">Допускаются только буквы</p>
    <p v-if="'numeric' in formValidations && !formValidations.numeric && formValidations.$invalid" class="alert-subtitle">Допускаются только цифры</p>
    <p v-if="'check7' in formValidations && !formValidations.check7" class="alert-subtitle">Первая цифра должна быть 7</p>
  </div>
</template>

<script>
export default {
  name: 'Form-alert',
  data () {
    return {}
  },
  props: {
    formValidations: Object
  }
}
</script>

<style lang="sass" scoped>
  .alert-subtitle
    color: red
    font-size: 10px
    margin-bottom: 0
</style>
