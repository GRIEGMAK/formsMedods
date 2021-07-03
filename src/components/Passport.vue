<template>
<div id="passport">
    <div id="header_passport" @click="open_dropdown">
        <div>
            Паспорт:
        </div>
        <div id="passport_arrow"></div>
    </div>
    <div id="body_passport">
        <label for="type_document">Тип документа*:
            <select  v-model="form.type_document" 
            :class="$v.form.type_document.$invalid && !firstRegistration ? 'invalid_value' : ''">
                <option v-for="(type_document, index) in types_document" :value="type_document.value" :key="index">
                    {{type_document.value}}
                </option>
            </select>
        </label>
        <label for="documents_series">Серия:
            <input type="text" 
            id="documents_series" 
            v-model="form.documents_series" 
            :class="$v.form.documents_series.$invalid && !firstRegistration ? 'invalid_value' : ''"/>
        </label>
        <label for="documents_number">Номер:
            <input type="text" 
            id="documents_number" 
            v-model="form.documents_number" 
            :class="$v.form.documents_number.$invalid && !firstRegistration ? 'invalid_value' : ''"/>
        </label>
        <label for="document_issued">Кем выдан:
            <input type="text" id="document_issued" v-model="form.document_issued" />
        </label>
        <label for="document_date">Дата выдачи*:
            <input type="date" id="document_date" 
            v-model="form.document_date" 
            :class="$v.form.document_date.$invalid && !firstRegistration ? 'invalid_value' : ''"
            />
        </label>
    </div>
</div>
</template>

<script>
import { required, minLength } from '@vuelidate/validators'
import { useVuelidate } from '@vuelidate/core'
import onlyNumbers from '../valid/onlyNumbers';
import '@/styles/passport.sass';

export default {
  name: 'Passport',
  methods: {
    open_dropdown(){
        if(document.querySelector("#passport").classList.contains("passive")) {
            document.querySelector("#passport").classList.remove("passive")
        }
        else {
            document.querySelector("#passport").classList.add("passive")
        }
    }
  },
  props: ['firstRegistration', 'checkFormPassport'],
  data() {
      return{
          registerClient: false,
          form: {
              type_document: '',
              documents_series: '',
              documents_number: '',
              document_issued: '',
              document_date: '',
          },
          types_document: [
              {
                  value: "Паспорт"
              },
              {
                  value: "Свидетельство о рождении"
              },
              {
                  value: "Вод. удостоверение"
              }
          ]
      }
  },
  setup: () => ({ $v: useVuelidate() }),
  validations: {
    form: {
        documents_series: { onlyNumbers, minLength: minLength(4)},
        documents_number: { onlyNumbers, minLength: minLength(6)},
        type_document: { required },
        document_date: { required },
    },
  },
}
</script>
