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
  methods: {
    cancel_reset() {
      document.querySelectorAll("input").forEach(input=> {
        input.value=""
      })
      document.querySelectorAll("select").forEach(select=> {
        select.value=""
      })
    },
    save_reset() {
      this.cancel_reset()
      alert("Клиент создан")
    }
  }
}
</script>
