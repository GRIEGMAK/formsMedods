<template>
  <div id="main_form">
    <div id="name_form">
        АНКЕТА
    </div>
    <label for="surname">Фамилия*:
        <input type="text" 
        id="surname" 
        v-model.trim="form.surname" 
        tabindex="1" 
        class=""
        :class="$v.form.surname.$invalid && !firstRegistration ? 'invalid_value' : ''"
        />
    </label>
    <label for="name">Имя*:
        <input type="text" 
        id="name" 
        tabindex="2" 
        v-model.trim="form.name" 
        :class="$v.form.name.$invalid && !firstRegistration ? 'invalid_value' : ''"
        />
    </label>
    <label for="last_name">Отчество:
        <input type="text" id="last_name" v-model.trim="form.last_name" tabindex="3" />
    </label>
    <label for="birthday">Дата рождения*:
        <input type="date" 
        id="birthday" 
        v-model.trim="form.birthday" 
        tabindex="4" 
        :class="$v.form.birthday.$invalid && !firstRegistration ? 'invalid_value' : ''"/>
    </label>
    <label for="number_phone">Номер телефона*:
        <input type="tel" 
        id="number_phone" 
        placeholder="11 цифр, с 7" 
        v-model.trim="form.number_phone" 
        tabindex="5" 
        :class="$v.form.number_phone.$invalid && !firstRegistration ? 'invalid_value' : ''"/>
    </label>
    <label for="sex">Пол:
        <input type="text" id="sex" v-model.trim="form.sex" tabindex="6"/>
    </label>
    <label for="group_client">Группа клиентов*:
        <select multiple 
        size=3 
        v-model.trim="form.group_client" 
        id="group_client"
        :class="$v.form.group_client.$invalid && !firstRegistration ? 'invalid_value' : ''">
            <option>VIP</option>
            <option>Проблемные</option>
            <option>ОМС</option>  
        </select>
    </label>
    <label>Лечащий врач:
        <select>
            <option v-for="(doctor, index) in doctors" :value="doctor.value" :key="index">
                {{doctor.value}}
            </option>
        </select>
    </label>
    <div id="div_sms">Не отправлять СМС:
        <input type="checkbox" id="sms" v-model="form.sms" />
    </div>
    <Adress :firstRegistration="firstRegistration" />
    <Passport :firstRegistration="firstRegistration" />
    <note></note>
    <send-panel :changeFirstRegistration="changeFirstRegistration"></send-panel>
  </div>
</template>

<script>
import "@/styles/mainform.sass";
import Passport from './Passport.vue';
import Adress from './Adress.vue';
import SendPanel from './SendPanel.vue';
import Note from './Note.vue';
import { required } from '@vuelidate/validators'
import { useVuelidate } from '@vuelidate/core'
import onlyNumbers from '../valid/onlyNumbers';
import validPhone from '../valid/validPhone';


export default {
  name: 'MainForm',
  components: {
    Passport, 
    Adress,
    SendPanel,
    Note
  },
  data() {
      return {
        firstRegistration: true,
        form: {
          surname: '',
          name: '',
          last_name: '',
          birthday: '',
          number_phone: '',
          sex: '',
          group_client: [],
          doctor: '',
          sms: false,
        },
        doctors: [
            {
              value: 'Иванов'
            },
            {
              value: 'Захаров'
            },
            {
              value: 'Чернышева'
            }
        ]
    }
  },
  setup: () => ({ $v: useVuelidate() }),
  validations: {
    form: {
        surname: { required } ,
        name: { required },
        birthday: { required },
        number_phone: { required, onlyNumbers, validPhone },
        group_client: { required },
    },
  },
  methods: {
    changeFirstRegistration(value) {
      this.firstRegistration = value;
    }
  },
}
</script>