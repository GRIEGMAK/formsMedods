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
            <select>
                <option v-for="(type_document, index) in types_document" :value="type_document.value" :key="index">
                    {{type_document.value}}
                </option>
            </select>
        </label>
        <label for="documents_series">Серия:
            <input type="text" id="documents_series" />
        </label>
        <label for="documents_number">Номер:
            <input type="text" id="documents_number" />
        </label>
        <label for="document_issued">Кем выдан:
            <input type="text" id="document_issued" />
        </label>
        <label for="document_date">Дата выдачи*:
            <input type="date" id="document_date" required/>
        </label>
    </div>
</div>
</template>

<script>
import '@/styles/passport.sass'

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
  data() {
      return{
          registerPassportClient: false,
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
  }
}
</script>
