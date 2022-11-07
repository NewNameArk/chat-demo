<template>
  <img class="msg-img" :src="msgContent">
</template>
<script>
export default {
  name: 'ImgMessage',
  props: {
    msgId: {
      type: String,
      default: ""
    },
    msgContent: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      name: '图片'
    }
  }
}
</script>
<style scoped>
.msg-img {
  width: 300px;
  height: 300px;
}
</style>