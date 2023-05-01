<template>
    <div class="loader">
      <span></span>
      <span></span>
      <span></span>
      <span></span>
    </div>
</template>

<script>
  export default {
    name: 'VueLoader',
    data() {
      return {}
    }
  }

</script>

<style scope>
.loader {
  width: 400px;
  height: 400px;
  display: flex;
  position: relative;
  justify-content: center;
  align-items: center;
  animation: scale 5s linear infinite;
}
.loader span {
  width: 200px;
  height: 200px;
  position: absolute;
  border-left: 3px solid #ff006a;
  border-right: 3px solid #9d00ff;
  border-radius: 37% 61% 63% 35% / 42% 34% 64% 56%;
  animation: rotate 3s linear infinite;
}
.loader span:nth-child(1) {
  animation: rotate 6s linear infinite reverse;
}
.loader span:nth-child(2) {
  animation: rotate 9s linear infinite;
}
.loader span:nth-child(3) {
  animation: rotate 12s linear infinite reverse;
}
@keyframes rotate {
  0% {
    transform: rotate(0);
  }
  100% {
    transform: rotate(360deg);
  }
}
@keyframes scale {
  0% {
    width: 400px;
    height: 400px;
  }
  50% {
    width: 600px;
    height: 600px;
  }
  100% {
    width: 400px;
    height: 400px;
  }
}

</style>