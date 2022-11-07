<template>
  <!-- 动画设置 -->
  <!-- http://www.javashuo.com/article/p-eidrwqts-wu.html -->
  <div>
    <div
      class="audio-simulation"
      :class="{ 'other-speak': owner === 'other', 'me-speak': owner === 'me' }"
    >
      <button @click="playAudio">点击播放</button>
      <span>{{ duration }}s</span>
      <HornCom v-show="showAnimation" :owner="owner" />
    </div>
    <audio
      ref="audio"
      v-show="showAudio"
      controls="controls"
      :src="msgContent"
    ></audio>
  </div>
</template>
<script>
import HornCom from "./HornCom";
export default {
  name: "AudioMessage",
  components: {
    HornCom
  },
  props: {
    msgId: {
      type: String,
      default: ""
    },
    owner: {
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
      duration: "",
      showAnimation: false,
      showAudio: false,
      name: "语音"
    };
  },
  mounted() {
    this.getTime();
  },
  methods: {
    getTime() {
      const au = document.createElement("audio");
      au.src = this.msgContent;
      au.addEventListener(
        "loadedmetadata",
        () => {
          this.duration = au.duration;
        },
        false
      );
    },
    pausePlay() {
      this.$refs.audio.pause();
    },
    closeAnimation() {
      this.showAnimation = false;
    },
    playAudio() {
      const that = this;
      // 再次播放的时候从头开始播放 https://segmentfault.com/q/1010000019975203
      this.$refs.audio.currentTime = 0;
      this.$refs.audio.play();
      // 通知其他音频停止播放
      this.$eventBus.$emit("pausePaly", { msgId: this.msgId });
      this.showAnimation = true;
      this.$refs.audio.addEventListener(
        "ended",
        function () {
          that.closeAnimation();
        },
        false
      );
    }
  }
};
</script>
<style scoped>
.audio-simulation {
  height: 50px;
  width: 200px;
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
}
.me-speak {
  flex-direction: row-reverse;
}
</style>
