<template>
  <div class="form-wrap">
    <form class="form">
      <Input :form-data="secondName"
             :validations="$v.secondName.value"
             v-on:input="secondName.value = $event"
      />
      <Input :form-data="firstName"
             :validations="$v.firstName.value"
             v-on:input="firstName.value = $event"
      />
      <Input :form-data="lastName"
             :validations="$v.lastName.value"
             v-on:input="lastName.value = $event"
      />
      <Input :form-data="birthday"
             :validations="$v.birthday.value"
             v-on:input="birthday.value = $event"
      />
      <Input :form-data="telNumber"
             :validations="$v.telNumber.value"
             v-on:input="telNumber.value = $event"
      />
      <Select :form-data="gender"
              :validations="$v.gender.value"
              v-on:input="gender.value = $event"
      />
      <Select :form-data="clientGroup"
              :validations="$v.clientGroup.value"
              v-on:input="clientGroup.value = $event"
      />
      <Select :form-data="doctor"
              :validations="$v.doctor.value"
              v-on:input="doctor.value = $event"
      />
      <Checkbox :form-data="noSendSms"
                :validations="$v.noSendSms.value"
                v-on:input="noSendSms.value = $event"
      />
      <Input :form-data="address.postcode"
             :validations="$v.address.postcode.value"
             v-on:input="address.postcode.value = $event"
      />
      <Input :form-data="address.country"
             :validations="$v.address.country.value"
             v-on:input="address.country.value = $event"
      />
      <Input :form-data="address.region"
             :validations="$v.address.region.value"
             v-on:input="address.region.value = $event"
      />
      <Input :form-data="address.city"
             :validations="$v.address.city.value"
             v-on:input="address.city.value = $event"
      />
      <Input :form-data="address.street"
             :validations="$v.address.street.value"
             v-on:input="address.street.value = $event"
      />
      <Input :form-data="address.house"
             :validations="$v.address.house.value"
             v-on:input="address.house.value = $event"
      />
      <Select :form-data="passport.type"
              :validations="$v.passport.type.value"
              v-on:input="passport.type.value = $event"
      />
      <Input :form-data="passport.series"
             :validations="$v.passport.series.value"
             v-on:input="passport.series.value = $event"
      />
      <Input :form-data="passport.number"
             :validations="$v.passport.number.value"
             v-on:input="passport.number.value = $event"
      />
      <Input :form-data="passport.whoIssued"
             :validations="$v.passport.whoIssued.value"
             v-on:input="passport.whoIssued.value = $event"
      />
      <Input :form-data="passport.issueDate"
             :validations="$v.passport.issueDate.value"
             v-on:input="passport.issueDate.value = $event"
      />
      <button type="submit" @click.prevent="checkForm">Отправить</button>
    </form>
    <div class="modal" v-if="showModal">
      <div class="message">
        Вы заполнили форму без ошибок
        <button class="okButton" @click="showModal = false">
          OK
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import Input from './molecules/Input'
import Select from './molecules/Select'
import Checkbox from './molecules/Checkbox'
import { validationMixin } from 'vuelidate'
import { required, minLength, numeric, maxLength } from 'vuelidate/lib/validators'
const checkLatinCyrillic = function (value) {
  if (value) {
    return (/^[a-zа-яA-ZА-Я ]+$/i).test(value)
  } else {
    return true
  }
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
      showModal: false,
      firstName: {
        label: 'Имя',
        value: '',
        type: 'text',
        required: true,
        placeholder: 'Введите имя'
      },
      secondName: {
        label: 'Фамилия',
        value: '',
        type: 'text',
        required: true,
        placeholder: 'Введите фамилию'
      },
      lastName: {
        label: 'Отчество',
        value: '',
        type: 'text',
        required: false,
        placeholder: 'Введите отчество'
      },
      birthday: {
        label: 'Дата рождения',
        value: '',
        type: 'date',
        required: true,
        placeholder: ''
      },
      telNumber: {
        label: 'Номер телефона',
        value: '',
        type: 'tel',
        required: true,
        placeholder: ''
      },
      gender: {
        label: 'Пол',
        value: '',
        required: false,
        options: ['Мужской', 'Женский']
      },
      clientGroup: {
        label: 'Группа клиентов',
        value: '',
        required: true,
        options: ['VIP', 'Проблемные', 'ОМС'],
        multipleSelect: true
      },
      doctor: {
        label: 'Лечащий врач',
        value: '',
        required: false,
        options: ['Иванов', 'Захаров', 'Чернышева']
      },
      noSendSms: {
        label: 'Не отправлять SMS',
        value: '',
        type: 'checkbox',
        required: false,
        placeholder: ''
      },
      address: {
        postcode: {
          label: 'Почтовый индекс',
          value: '',
          type: 'number',
          required: false,
          placeholder: ''
        },
        country: {
          label: 'Страна',
          value: '',
          type: 'text',
          required: false,
          placeholder: ''
        },
        region: {
          label: 'Область',
          value: '',
          type: 'text',
          required: false,
          placeholder: ''
        },
        city: {
          label: 'Город',
          value: '',
          type: 'text',
          required: true,
          placeholder: ''
        },
        street: {
          label: 'Улица',
          value: '',
          type: 'text',
          required: false,
          placeholder: ''
        },
        house: {
          label: 'Дом',
          value: '',
          type: 'number',
          required: false,
          placeholder: ''
        }
      },
      passport: {
        type: {
          label: 'Тип документа:',
          value: '',
          required: true,
          options: ['Паспорт', 'Свидетельство о рождении', 'Водительское удостоверение']
        },
        series: {
          label: 'Серия',
          value: '',
          type: 'text',
          required: false,
          placeholder: ''
        },
        number: {
          label: 'Номер',
          value: '',
          type: 'number',
          required: false,
          placeholder: ''
        },
        whoIssued: {
          label: 'Кем выдан',
          value: '',
          type: 'text',
          required: false,
          placeholder: ''
        },
        issueDate: {
          label: 'Дата выдачи',
          value: '',
          type: 'date',
          required: true,
          placeholder: ''
        }
      }
    }
  },
  methods: {
    checkForm: function () {
      this.$v.$touch()
      if (!this.$v.$invalid) {
        this.showModal = true
      }
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
  .form-wrap
    font-family: sans-serif

    .form
      display: flex
      flex-direction: column
      width: 50%
      min-width: 300px
      margin: auto

      button[type='submit']
        width: 100px
        height: 30px
        margin: 15px auto 0 auto

    .modal
      position: fixed
      display: flex
      align-items: center
      top: 0
      width: 100vw
      height: 100vh
      background-color: rgba(0, 0, 0, .5)

      .message
        display: flex
        flex-direction: column
        justify-content: center
        align-items: center
        margin: auto
        width: 300px
        height: 100px
        background-color: #fff

        .okButton
          margin-top: 20px
</style>
