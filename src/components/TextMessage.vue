<template>
  <div class="msg-text">{{msgContent}}</div>
</template>
<script>
export default {
  name: 'TextMessage',
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
      name: '123'
    }
  }
}
</script>
<style scoped>
.msg-text {
  max-width: 300px;
  text-align: start;
}
</style>