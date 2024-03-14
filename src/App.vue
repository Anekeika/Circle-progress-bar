<template>
  <div class="wrapper">
    <progress-controls :progressValue="progressValue" @updateProgress="updateProgress" />
    <progress-circle :progressValue="progressValue"/>
  </div>
</template>

<script>
import ProgressControls from './components/ProgressControls.vue';
import ProgressCircle from './components/ProgressCircle.vue';

export default {
  components: {
    ProgressControls,
    ProgressCircle
  },
  data() {
    return {
      progressValue: 0
    };
  },
  methods: {
    updateProgress(value) {
      this.progressValue = value;
    }
  }
}
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 10px;
  height: 100vh;
}
</style>
