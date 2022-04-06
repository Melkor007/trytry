<template>
  <div class="scroll-wrapper" ref="scroll">
    <div class="scroll-content">
      <chat-item
        v-for="item in chatItems"
        :key="item.message"
        :type="item.type"
        :message="item.message"
        :timestamp="item.timestamp"
        :from="item.from"
      ></chat-item>
    </div>
    <input type="text" v-model="question"
        placeholder="请输入问题" @keyup.enter="qa()">
  </div>

</template>

<script>
import BScroll from "@better-scroll/core";
import MouseWheel from "@better-scroll/mouse-wheel"
import ChatItem from "./ChatItem";
// import chatItems from "../assets/data/items";

BScroll.use(MouseWheel)

export default {
  name: "",
  data() {
    return {
      chatItems:[{
        type:1,
        message:"你好，这里是医疗问答机器人",
        from:1,
        timestamp: new Date()
    }],
      bs: null,
      question:""
    };
  },
  components: {
    "chat-item": ChatItem,
  },

  mounted() {
    this.init();
  },
  beforeUnmount() {
    this.bs.destroy();
  },
  methods: {
    // better-scroll的代码
    init() {
        this.chatItems.push({
        type:2,
        message:"你好,我有一些问题",
        from:2,
        timestamp: new Date()
    })
      this.bs = new BScroll(this.$refs.scroll, {
        scrollY: true, // 上下滚动
        click: true,   // 开启点击事件
        startY: document.querySelector(".scroll-wrapper").clientHeight - this.$refs.scroll.scrollHeight + 5 , // 初始高度
        mouseWheel: true,   // 鼠标滚动
        probeType: 2, // listening scroll hook
      });
      
    },
    clickHandler(item) {
      alert(item);
    },
    qa(){
        this.chatItems.push(
            {
            type:2,
            message:this.question,
            from:2,
            timestamp: new Date() 
            }
        )
    }
  },
};
</script>

<style lang="scss" scoped>
.scroll-wrapper {
  height: calc(100% - 160px);  // 留一些空间给 打字的地方 和 header
  overflow: hidden;    // 非常之关键
}
</style>