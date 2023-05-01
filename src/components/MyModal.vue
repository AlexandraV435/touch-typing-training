<template>
  <div class="popup__wrapper" v-if="isVisible">
    <div class="popup__background"></div>
    <div class="popup__content">
      <h1 class="popup__title">Приготовься печатать! Поехали!</h1>
      <button @click="isVisible=false" class="popup-btn btn btn-warning">Начать печатать</button>
    </div>
  </div>

</template>

<script>
  export default {
    name: 'MyModal',
    data() {
      return {
        isVisible: true,
      }
    }
  }

</script>

<style scope>
  .popup__title {
    font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif
  }
  .popup__content {
    display: flex;
    flex-direction: column;
    position: absolute;
    width: 600px;
    height: 300px;
    box-shadow: 0px 0px 51px 11px rgb(77, 165, 220, 0.8);
    border-radius: 10px;
    top: 50%;
    left: 50%;
    margin-right: -50%;
    transform: translate(-50%, -50%);
    z-index: 99;
    background: rgb(255, 255, 255);
    text-align: center;
    justify-content: center;
    justify-items: center;
    align-items: center;
    color: #6b6b6b;
    padding: 10px
  }

  .popup__background {
    position: absolute;
    width: 100vw;
    height: 100vh;
    background: rgba(112, 197, 250, 0.6);
    z-index: 98;
  }

  .popup__btn {
    width: 170px;
    box-shadow: 0px 0px 11px 1px rgba(216, 171, 62, 0.59);
  }

  .popup__btn:active {
    box-shadow: none
  }

@media screen and (max-width: 618px) {
  .popup__content {
    width: 90vw;
  }
}

</style>