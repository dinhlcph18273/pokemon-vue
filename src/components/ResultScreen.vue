<template>
  <div class="screen">
    <h1>✨ Congratulations ✨</h1>
    <p>{{ Math.round(timer / 1000) }} seconds</p>
    <button @click="onStartAgain">Start Again</button>
  </div>
</template>

<script>
export default {
  props: {
    timer: {
      type: Number,
      requied: true,
    },
  },

  methods: {
    onStartAgain() {
      this.$emit("startAgain");
    },
  },
};
</script>
