<template>
  <div id="app">
    <div
      ref="container"
      style="
        margin-top: 10px;
        border: 1px solid #ccc;
        width: 700px;
        height: 500px;
        overflow-y: scroll;
      "
    >
      <MessageItem
        :class="{ 'first-unread': index === unReadIndex }"
        v-for="(item, index) in messageArr"
        :msgId="`msg${index}`"
        :ref="`msg${index}`"
        :key="`msg${index}`"
        :msgContent="item.msgContent"
        :owner="item.msgOwner"
        :msgType="item.msgType"
      />
    </div>
  </div>
</template>

<script>
import MessageItem from "./components/MessageItem.vue";

export default {
  name: "App",
  components: {
    MessageItem
  },
  data() {
    return {
      unReadIndex: -1,
      messageArr: [
        {
          msgType: "text",
          msgContent: "hello",
          msgOwner: "other",
          isRead: true
        },
        {
          msgType: "text",
          msgContent: "hello",
          msgOwner: "me",
          isRead: true
        },
        {
          msgType: "text",
          msgContent:
            "全情投入、守正出奇、愿等花开。全情投入，就是去享受当前业务，想办法做到极致；守正出奇，就是找准正、奇，奇帮助正，一起达到最佳效果，比如前端领域，业务为正，专业为奇。首先要把业务服务好，要保证客户第一；愿等花开，就是做一个长期主义，很多事情都需要定力和耐心，要快，但绝对不能急。",
          msgOwner: "other",
          isRead: true
        },
        {
          msgType: "text",
          msgContent:
            "全情投入、守正出奇、愿等花开。全情投入，就是去享受当前业务，想办法做到极致；守正出奇，就是找准正、奇，奇帮助正，一起达到最佳效果，比如前端领域，业务为正，专业为奇。首先要把业务服务好，要保证客户第一；愿等花开，就是做一个长期主义，很多事情都需要定力和耐心，要快，但绝对不能急。",
          msgOwner: "me",
          isRead: false
        },
        {
          msgType: "audio",
          msgContent: "http://asr-test.test.upcdn.net/16k.wav",
          msgOwner: "other",
          isRead: false
        },
        {
          msgType: "audio",
          msgContent: "http://asr-test.test.upcdn.net/16k.wav",
          msgOwner: "me",
          isRead: false
        },
        {
          msgType: "img",
          msgContent:
            "https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fnimg.ws.126.net%2F%3Furl%3Dhttp%253A%252F%252Fdingyue.ws.126.net%252F2021%252F1013%252F035f0606j00r0wam60036c000ku00mnm.jpg%26thumbnail%3D650x2147483647%26quality%3D80%26type%3Djpg&refer=http%3A%2F%2Fnimg.ws.126.net&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1669799592&t=b2d480a40e0c00dc351b5fe2b3e5c37d",
          msgOwner: "other",
          isRead: false
        }
      ]
    };
  },
  mounted() {
    // const that = this;
    this.$eventBus.$off("pausePaly");
    this.$eventBus.$on("pausePaly", (data) => {
      for (let i = 0; i < this.messageArr.length; i++) {
        const curMsg = `msg${i}`;
        if ((curMsg !== data.msgId ) && this.messageArr[i].msgType === 'audio') {
          console.log(this.$refs[curMsg][0])
          const target = this.$refs[curMsg][0]
          target.closeAnimation() 
        }
      }
    });
    this.$nextTick(() => {
      const unReadIndex = this.getUnreadIndex();
      this.unReadIndex = unReadIndex;
      this.$refs.container.scrollTop = this.getScrollTop(unReadIndex) + 30;
    });
  },
  methods: {
    // 获取当前对话框的滚动高度
    getScrollTop(param) {
      let res = 0;
      for (let i = 0; i < param; i++) {
        res += this.$refs[`msg${i}`][0].$el.offsetHeight;
      }
      return res;
    },
    // 获取维度消息索引
    getUnreadIndex() {
      for (let i = 0; i < this.messageArr.length; i++) {
        if (!this.messageArr[i].isRead) {
          return i;
        }
      }
      return 0;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.message-container {
  margin-left: 20px;
  border: 1px solid #ccc;
  width: 700px;
  height: 500px;
  overflow-y: scroll;
}
.msg-item {
  margin-top: 20px;
}
.message-img {
  width: 300px;
  height: 300px;
}
/* 首个未读消息：则标红显示 */
.first-unread .message-item {
  color: red;
}
</style>
