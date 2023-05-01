<template>
  <MainPage/>
</template>

<script>
import MainPage from './components/MainPage.vue'

export default {
  name: 'App',
  components: {
    MainPage
  }
}

</script>

<style>
* {
  margin: 0;
  padding: 0;
}

#app {
  min-height: 100vh;
  background: #70c5fa;
}
</style>
