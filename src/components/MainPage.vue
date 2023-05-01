<template>
  <div class="main">
    <MyModal @generateText="generateText"></MyModal>
    <div class="main__wrapper" v-if="text">
      <VueInformation :information="{accuracy, speed, countErrors}"></VueInformation>
      <div class="main__wrapperText">
        <div v-if="text.length>0" class="main__text">
          <span v-for="(letter, index) in text" :key="index">{{ letter }}</span>
        </div>
      <textarea v-model="userText" @keydown="onPress"></textarea>
      </div>
    </div>
    <VueLoader v-else></VueLoader>
  </div>
</template>

<script>
import MyModal from './MyModal.vue';
import VueLoader from './VueLoader.vue';
import VueInformation from './VueInformation.vue'

export default {
  name: 'MainPage',
  components: {
    MyModal,
    VueLoader,
    VueInformation,
  }, 
  data() {
    return {
      url: 'https://baconipsum.com/api/?type=meat-and-filler&paras=2',
      text: '',
      userText: '',
      currentIndex: -1,
      countErrors: 0,
      keyPress: null,
      currentLetterUser: null,
      prev: -1,
      speed: 0, 
      accuracy: 100,
      startTime: null,
      endTime: null,
    }
  },
  mounted() {
    this.generateText(),
    setInterval(() => {
      this.calcSpeed();
    }, 1000)
  },
  methods: {
    async generateText() {
      let response = await fetch(this.url);
      this.text = (await response.json()).join("");
    },
    onPress(e) {
      this.keyPress = e.key;
      let index = this.userText.length - 1;
      this.currentLetterUser = this.userText[index];
      if (this.currentLetterUser === this.text[this.prev] && this.keyPress !== 'Backspace') {
        this.prev +=1;
      }
      if (this.keyPress !== this.text[this.prev]) {
        e.preventDefault();
        if (this.keyPress !== 'Shift'  && this.keyPress !== 'Backspace') {
          this.countErrors +=1;
        }
      }
      let accuracy = ((1 - (this.countErrors/this.text.length)) * 100).toFixed(1);

      if (accuracy >= 0 ) {
        this.accuracy = accuracy;
      } else {
        this.accuracy = 0;
      }
    },

    calcSpeed() {
      if (!this.startTime) {
        this.startTime = Date.now();
      }
      this.endTime = this.userText.length ? Date.now() : 0
      const elapsedMinutes = (this.endTime - this.startTime) / 1000 / 60;
      this.speed = this.userText.length ? Math.round(this.userText.length / elapsedMinutes) : 0
    },
    reloadPage() {
      location.reload();
    }
  },
}
</script>

<style scoped>
.main {
  display: flex;
  justify-content: center;
}
.main__wrapper {
  display: flex;
  flex-direction: row-reverse;
  justify-content: center;
  align-items: center;
  padding: 100px 10px 0 10px;
}
.main__text {
  color: rgb(130, 130, 130);
  font-size: 16px;
  font-family: 'Courier New', Courier, monospace;
  width: 70vw;
  word-break:break-all;
  padding: 20px;
}
textarea {
  font-family: 'Courier New', Courier, monospace;
  position: absolute;
  background: none;
  outline: none;
  font-size: 16px;
  resize: none;
  display: inline-table;
  width: 70vw;
  padding: 20px;
  border: none;
  word-break: break-all;
}
.main__wrapperText {
  display: flex;
  padding: 10px;
  background: white;
  border-radius: 15px;
}

.main__information {
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
  .main__wrapper {
    padding: 50px 10px 0 10px;
    flex-direction: column-reverse;
  }

  .main__information {
    margin-top: 20px;
    margin-bottom: 20px;
  }
}
</style>
