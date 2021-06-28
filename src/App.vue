<template>
  <div id="forms_app">
    <div id="app">
      <MainForm />
    </div>
  </div>
</template>

<script>
import MainForm from './components/MainForm.vue'
import '@/styles/app.sass'

export default {
  name: 'App',
  components: {
    MainForm
  }
}
</script>
