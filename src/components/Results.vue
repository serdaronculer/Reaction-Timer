<template>
  <div class="reactionTime">
    <p>Reaction time : {{ score }} ms</p>
    <p>{{ rank }}</p>
  </div>
</template>

<script>
export default {
  props: ["score"],
  data() {
    return {
      rank: null,
    };
  },
  mounted() {
    if (this.score < 400) {
      this.rank = "You have very fast fingers!";
    }  else if (this.score < 500) {
      this.rank = "You have a rapid reflex";
    } else if(this.score < 600) {
      this.rank = "Not bad at all";
    } else {
        this.rank = "Snail pace..."
    }
  },
};
</script>

<style>
.reactionTime {
  font-size: 1.4rem;
  color: #fff;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>