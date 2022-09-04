<template>
  <div ref="parent" class="container">
    <div ref="box" class="block" @click="stopTimer" v-show="showBlock">
      click me
    </div>
  </div>
  <p v-show="!showBlock" class="animate__animated animate__pulse animate__infinite	infinite info">Can come at any time!</p>
</template>
  
  <script>
export default {
  props: ["delay"],
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0,
    };
  },
  emits:["end"],
  mounted() {
    this.placeGenerator();
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay);
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        // assign to 'reactionTime' property every 10 milliseconds
        this.reactionTime += 10;
      }, 10);
    },
    stopTimer() {
      clearInterval(this.timer);
      this.$emit("end", this.reactionTime);
    },
    placeGenerator() {
      this.$refs.box.style.left =
        Math.random() * (this.$refs.parent.clientWidth - 100) + "px";
      this.$refs.box.style.top =
        Math.random() * (this.$refs.parent.clientHeight - 100) + "px";
    },
  },
};
</script>
  
  <style scoped>
.block {
  width: 6rem;
  height: 6rem;
  border-radius: 5px;
  background: #0faf87;
  color: #fff;
  text-align: center;
  cursor: pointer;
  line-height: 6rem;
  position: absolute;
}

.container {
  width: 50%;
  height: 50%;
  border: 1px solid lightgray;
  margin: 0 auto;
  margin-top: 30px;
  padding: 10px;
  position: relative;
}

.info{
    display: inline-block;
    color: black;
    font-size: 2rem;
    margin-top: 25px;
    color: #fff;
}
</style>