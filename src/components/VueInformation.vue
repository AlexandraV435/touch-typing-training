<template>
  <div class="information">
    <p>Ошибки: {{ information.countErrors }}</p>
    <p>Точность: {{ information.accuracy }}%</p>
    <p>Скорость: {{ information.speed }} зн./мин</p>
    <button class="btn btn-warning" @click="reloadPage">Начать заново</button>
  </div>
</template>

<script>
export default {
  name: 'VueInformation',
  props: ['information'],
  data() {
    return {}
  }
}

</script>

<style scope>
.information {
  display: flex;
  flex-direction: column;
  margin-left: 20px;
  background: white;
  height: 220px;
  min-width: 230px;
  border-radius: 20px;
  justify-content: center;
  align-items: center;
  color: #454545;
  font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

@media screen and (max-width: 1095px){
  .information {
    margin-top: 20px;
    margin-bottom: 20px;
  }
}
</style>