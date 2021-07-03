<template>
<div id="adress">
    <div id="header_adress" @click="open_dropdown">
        <div>
            Адрес:
        </div>
        <div id="adress_arrow"></div>
    </div>
    <div id="body_adress">
        <label for="index_city">Индекс:
            <input type="text" 
            id="index_city" 
            v-model.trim="form.index_city"
            :class="$v.form.index_city.$invalid && !firstRegistration ? 'invalid_value' : ''"/>
        </label>
        <label for="country">Страна:
            <input type="text" id="country" v-model.trim="form.country"/>
        </label>
        <label for="region">Область:
            <input type="text" id="region" v-model.trim="form.region"/>
        </label>
        <label for="city">Город:
            <input type="text" id="city" v-model.trim="form.city"/>
        </label>
        <label for="street">Улица:
            <input type="text" id="street" v-model.trim="form.street"/>
        </label>
        <label for="home">Дом:
            <input type="text" id="home" v-model.trim="form.home"/>
        </label>
    </div>
</div>
</template>

<script>
import onlyNumbers from '../valid/onlyNumbers';
import { useVuelidate } from '@vuelidate/core';
import { maxLength } from '@vuelidate/validators';
import '@/styles/adress.sass';

export default {
  name: 'Adress',
  methods: {
      open_dropdown(){
          if(document.querySelector("#adress").classList.contains("passive")) {
              document.querySelector("#adress").classList.remove("passive")
          }
          else {
              document.querySelector("#adress").classList.add("passive")
          }
      },
  },
  props: ['firstRegistration'],
  data() {
      return{
          form: {
              index_city:'',
              country: '',
              region: '',
              city: '',
              street: '',
              home: '',
          },
      }
  },
  setup: () => ({ $v: useVuelidate() }),
  validations: {
    form: {
        index_city: { onlyNumbers, maxLength: maxLength(6) },
    },
  },
}
</script>
