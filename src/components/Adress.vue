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
            <input type="text" pattern="[0-9]{5}" id="index_city" />
        </label>
        <label for="country">Страна:
            <input type="text" id="country" />
        </label>
        <label for="region">Область:
            <input type="text" id="region" />
        </label>
        <label for="city">Город:
            <input type="text" id="city" />
        </label>
        <label for="street">Улица:
            <input type="text" id="street" />
        </label>
        <label for="home">Дом:
            <input type="text" id="home" />
        </label>
    </div>
</div>
</template>

<script>
import '@/styles/adress.sass'

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
      }
  },
  data() {
      return{
          form: {
              
          }
      }
  }
}
</script>
