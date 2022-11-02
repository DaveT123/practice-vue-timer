<template>
  <div></div>
  <div class="fakeBlock" v-if="!showBlock">Play area</div>
  <div class="block" v-if="showBlock" @click="stopTimer">
    Click Now!
  </div>
</template>

<script>
export default {
  props: ['delay'],
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0
    }
  },
  mounted() {
    console.log('mounted');
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay)
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
      }, 10)
    },
    stopTimer() {
      clearInterval(this.timer);
      this.$emit('end', this.reactionTime)
    }
  }
}
</script>

<style>
.block {
  width: 400px;
  border-radius: 20px;
  background:  #0faf87;;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}

.fakeBlock {
  width: 400px;
  border-radius: 20px;
  border-style: solid;
  border-color:  #0faf87;;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>