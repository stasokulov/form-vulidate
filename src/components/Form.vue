<template>
  <form class="form">
    <Input :form-data="secondName"
           :submitted="submitted"
           v-on:input="setValidations($event, 'secondName')"
    />
    <Input :form-data="firstName"
           :submitted="submitted"
           v-on:input="setValidations($event, 'firstName')"
    />
    <Input :form-data="lastName"
           v-on:input="setValidations($event, 'lastName')"
    />
    <Input :form-data="birthday"
           :submitted="submitted"
           v-on:input="setValidations($event, 'birthday')"
    />
    <Input :form-data="telNumber"
           :submitted="submitted"
           v-on:input="setValidations($event, 'telNumber')"
    />
    <Select :form-data="gender"
            v-on:input="setValidations($event, 'gender')"
    />
    <Select :form-data="clientGroup"
            :submitted="submitted"
            v-on:input="setValidations($event, 'clientGroup')"
    />
    <Select :form-data="doctor"
            v-on:input="setValidations($event, 'doctor')"
    />
    <Checkbox :form-data="noSendSms"
              v-on:input="setValidations($event, 'noSendSms')"
    />
    <Input :form-data="address.postcode"
           v-on:input="setValidations($event, 'address.postcode')"
    />
    <Input :form-data="address.country"
           v-on:input="setValidations($event, 'address.country')"
    />
    <Input :form-data="address.region"
           v-on:input="setValidations($event, 'address.region')"
    />
    <Input :form-data="address.city"
           :submitted="submitted"
           v-on:input="setValidations($event, 'address.city')"
    />
    <Input :form-data="address.street"

           v-on:input="setValidations($event, 'address.street')"
    />
    <Input :form-data="address.house"
           v-on:input="setValidations($event, 'address.house')"
    />
    <Select :form-data="passport.type"
            v-on:input="setValidations($event, 'passport.type')"
    />
    <Input :form-data="passport.series"
           v-on:input="setValidations($event, 'passport.series')"
    />
    <Input :form-data="passport.number"
           v-on:input="setValidations($event, 'passport.number')"
    />
    <Input :form-data="passport.whoIssued"
           v-on:input="setValidations($event, 'passport.whoIssued')"
    />
    <Input :form-data="passport.issueDate"
           :submitted="submitted"
           v-on:input="setValidations($event, 'passport.issueDate')"
    />

    <button type="submit" @click.prevent="checkRequireds">Отправить</button>
  </form>
</template>

<script>
import Input from './Input'
import Select from './Select'
import Checkbox from './Checkbox'
import { validationMixin } from 'vuelidate'
import { required, minLength, numeric, maxLength } from 'vuelidate/lib/validators'
const checkLatinCyrillic = function (value) {
  return (/^[a-zа-яA-ZА-Я ]+$/i).test(value)
}
export default {
  name: 'Form',
  mixins: [validationMixin],
  components: {
    Input,
    Select,
    Checkbox
  },
  data () {
    return {
      submitted: false,
      firstName: {
        label: 'Имя',
        value: '',
        type: 'text',
        required: true,
        placeholder: 'Введите имя',
        validations: {}
      },
      secondName: {
        label: 'Фамилия',
        value: '',
        type: 'text',
        required: true,
        placeholder: 'Введите фамилию',
        validations: {}
      },
      lastName: {
        label: 'Отчество',
        value: '',
        type: 'text',
        required: false,
        placeholder: 'Введите отчество',
        validations: {}
      },
      birthday: {
        label: 'Дата рождения',
        value: '',
        type: 'date',
        required: true,
        placeholder: '',
        validations: {}
      },
      telNumber: {
        label: 'Номер телефона',
        value: '',
        type: 'tel',
        required: true,
        placeholder: '',
        validations: {}
      },
      gender: {
        label: 'Пол',
        value: '',
        type: '',
        required: false,
        placeholder: '',
        options: ['Мужской', 'Женский'],
        validations: {}
      },
      clientGroup: {
        label: 'Группа клиентов',
        value: '',
        type: '',
        required: true,
        placeholder: '',
        options: ['VIP', 'Проблемные', 'ОМС'],
        multipleSelect: true,
        validations: {}
      },
      doctor: {
        label: 'Лечащий врач',
        value: '',
        type: '',
        required: false,
        placeholder: '',
        options: ['Иванов', 'Захаров', 'Чернышева'],
        validations: {}
      },
      noSendSms: {
        label: 'Не отправлять SMS',
        value: '',
        type: 'checkbox',
        required: false,
        placeholder: '',
        validations: {}
      },
      address: {
        postcode: {
          label: 'Почтовый индекс',
          value: '',
          type: 'number',
          required: false,
          placeholder: '',
          validations: {}
        },
        country: {
          label: 'Страна',
          value: '',
          type: 'text',
          required: false,
          placeholder: '',
          validations: {}
        },
        region: {
          label: 'Область',
          value: '',
          type: 'text',
          required: false,
          placeholder: '',
          validations: {}
        },
        city: {
          label: 'Город',
          value: '',
          type: 'text',
          required: true,
          placeholder: '',
          validations: {}
        },
        street: {
          label: 'Улица',
          value: '',
          type: 'text',
          required: false,
          placeholder: '',
          validations: {}
        },
        house: {
          label: 'Дом',
          value: '',
          type: 'number',
          required: false,
          placeholder: '',
          validations: {}
        }
      },
      passport: {
        type: {
          label: 'Тип документа:',
          value: '',
          type: '',
          required: true,
          placeholder: '',
          options: ['Паспорт', 'Свидетельство о рождении', 'Водительское удостоверение'],
          validations: {}
        },
        series: {
          label: 'Серия',
          value: '',
          type: 'text',
          required: false,
          placeholder: '',
          validations: {}
        },
        number: {
          label: 'Номер',
          value: '',
          type: 'number',
          required: false,
          placeholder: '',
          validations: {}
        },
        whoIssued: {
          label: 'Кем выдан',
          value: '',
          type: 'text',
          required: false,
          placeholder: '',
          validations: {}
        },
        issueDate: {
          label: 'Дата выдачи',
          value: '',
          type: 'date',
          required: true,
          placeholder: '',
          validations: {}
        }
      }
    }
  },
  methods: {
    setValidations: function (value, fieldName) {
      const path = fieldName.split('.')
      if (path.length === 1) {
        this[fieldName].value = value // Записываем значение из компонента
        this[fieldName].validations = this.$v[fieldName].value // Записываем результат валидации
      }
      if (path.length === 2) {
        this[path[0]][path[1]].value = value // Записываем значение из компонента
        this[path[0]][path[1]].validations = this.$v[path[0]][path[1]].value // Записываем результат валидации
      }
    },
    checkRequireds: function () {
      this.$v.$touch()
      this.submitted = true
    }
  },
  validations: {
    firstName: {
      value: { required, minLength: minLength(3), latinAndCyrillic: checkLatinCyrillic }
    },
    secondName: {
      value: { required, minLength: minLength(3), latinAndCyrillic: checkLatinCyrillic }
    },
    lastName: {
      value: { minLength: minLength(3), latinAndCyrillic: checkLatinCyrillic }
    },
    birthday: {
      value: { required }
    },
    telNumber: {
      value: {
        required,
        numeric,
        maxLength: maxLength(11),
        minLength: minLength(11),
        check7 (value) {
          if (value) {
            return value[0] === '7'
          } else {
            return true
          }
        }
      }
    },
    gender: {
      value: { required }
    },
    clientGroup: {
      value: { required }
    },
    doctor: {
      value: { latinAndCyrillic: checkLatinCyrillic }
    },
    noSendSms: {
      value: {}
    }, // Это поле имеет смысл валидировать только по required
    address: {
      postcode: {
        value: { minLength: minLength(6), numeric }
      },
      country: {
        value: { latinAndCyrillic: checkLatinCyrillic }
      },
      region: {
        value: { latinAndCyrillic: checkLatinCyrillic }
      },
      city: {
        value: { required, latinAndCyrillic: checkLatinCyrillic }
      },
      street: {
        value: { latinAndCyrillic: checkLatinCyrillic }
      },
      house: {
        value: { numeric }
      }
    },
    passport: {
      type: {
        value: { required }
      },
      series: {
        value: {} // Теоретически, серия разных документов может содержать и цифры, и буквы, поэтому проверку на цифры не ставлю.
      },
      number: {
        value: { numeric }
      },
      whoIssued: {
        value: { latinAndCyrillic: checkLatinCyrillic }
      },
      issueDate: {
        value: { required }
      }
    }
  }
}
</script>

<style lang="sass">
  .form
    display: flex
    flex-direction: column
    width: 50%
    min-width: 300px
    margin: auto
    font-family: sans-serif
</style>
