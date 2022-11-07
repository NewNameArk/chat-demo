<template>
  <div
    class="wifi-symbol"
    :class="{ 'right-horn': owner === 'other', 'left-horn': owner === 'me' }"
  >
    <div class="wifi-circle first"></div>
    <div class="wifi-circle second"></div>
    <div class="wifi-circle third"></div>
  </div>
</template>
<script>
export default {
  name: "HornCom",
  props: {
    owner: {
      type: String,
      default: "other"
    },
  },
  data() {
    return {
      name: "123"
    };
  }
};
</script>
<style scoped>
.wifi-symbol {
  box-sizing: border-box;
  position: relative;
  width: 50px;
  height: 50px;
  /* background: red; */
  box-sizing: border-box;
  overflow: hidden;
}
.right-horn {
  transform: rotate(135deg);
}
.left-horn {
  transform: rotate(315deg);
}
.wifi-circle {
  border: 5px solid #999;
  border-radius: 50%;
  position: absolute;
}
.first {
  width: 5px;
  height: 5px;
  background: #ccc;
  top: 45px;
  left: 45px;
}
.second {
  width: 25px;
  height: 25px;
  top: 35px;
  left: 35px;
  animation: fadeInOut 1s infinite 0.2s;
}
.third {
  width: 40px;
  height: 40px;
  top: 25px;
  left: 25px;
  animation: fadeInOut 1s infinite 0.4s;
}
@keyframes fadeInOut {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
</style>
