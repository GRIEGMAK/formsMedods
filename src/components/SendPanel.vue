<template>
  <div id="panel_button">
    <div id="cancel_button">
      <a @click="cancel_reset">Отмена</a>
    </div>
    <div id="save_button">
      <a @click="save_reset">Сохранить</a>
    </div>
  </div>
</template>

<script>
import '@/styles/sendpanel.sass'

export default {
  name: 'SendPanel',
  props: ['changeFirstRegistration'],
  methods: {
    cancel_reset() {
      document.querySelectorAll("input").forEach(input=> {
        input.value=""
      })
      document.querySelectorAll("select").forEach(select=> {
        select.value=""
      })
      this.changeFirstRegistration(true)
    },
    save_reset() {
      if(document.querySelectorAll('.invalid_value').length==0) {
        this.changeFirstRegistration(false)
        alert("Дополните данные и попробуйте сохраниться снова")
      } else {
        this.cancel_reset()
        
        alert("Клиент добавлен в базу")
      }
    }
  },
}
</script>
