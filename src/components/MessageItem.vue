<template>
  <div style="margin-top: 10px">
    <div class="message-item" :class="{ my: owner === 'me' }">
      <div class="avatar">头像</div>
      <div>
        <AudioMessage
          v-if="msgType === 'audio'"
          :msgContent="msgContent"
          :owner="owner"
          :msgId="msgId"
          ref="audioMsg"
        ></AudioMessage>
        <ImgMessage
          v-if="msgType === 'img'"
          :msgContent="msgContent"
          :msgId="msgId"
        ></ImgMessage>
        <TextMessage
          v-if="msgType === 'text'"
          :msgContent="msgContent"
          :msgId="msgId"
        ></TextMessage>
      </div>
    </div>
  </div>
</template>
<script>
import AudioMessage from "./AudioMessage";
import ImgMessage from "./ImgMessage";
import TextMessage from "./TextMessage";

export default {
  name: "MessageItem",
  components: {
    AudioMessage,
    ImgMessage,
    TextMessage
  },
  props: {
    msgId: {
      type: String,
      default: ""
    },
    msgContent: {
      type: String,
      default: ""
    },
    msgType: {
      type: String,
      default: ""
    },
    owner: {
      type: String,
      default: ""
    }
  },
  mounted() {},
  data() {
    return {
      name: "123"
    };
  },
  methods: {
    closeAnimation() {
      this.$refs.audioMsg.closeAnimation();
      this.$refs.audioMsg.pausePlay()
    },
  }
};
</script>
<style scoped>
.message-container {
  margin-top: 10px;
}
.message-item {
  display: flex;
  align-items: center;
}
.my {
  flex-direction: row-reverse;
}
.avatar {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  background-color: aqua;
  border-radius: 50%;
}
</style>
