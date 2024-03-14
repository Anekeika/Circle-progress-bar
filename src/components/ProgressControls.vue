<template>
  <div>
    <div>
      <input type="range" min="0" max="100" step="5" :value="progressValue" @input="updateProgressValue"/>
      <input type="number" min="0" max="100" :value="progressValue" @input="updateProgressValue"/>
      <div>
        <button :class="{ active: progressValue === 0 }" @click="setProgress(0)">0</button>
        <button :class="{ active: progressValue === 30 }" @click="setProgress(30)">30</button>
        <button :class="{ active: progressValue === 75 }" @click="setProgress(75)">75</button>
        <button :class="{ active: progressValue === 100 }" @click="setProgress(100)">100</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    progressValue: {
      type: Number,
      required: true
    }
  },
  methods: {
    updateProgressValue(event) {
      this.$emit('updateProgress', parseInt(event.target.value));
    },
    setProgress(value) {
      this.$emit('updateProgress', value);
    }
  }
}
</script>

<style>
input {
  margin: 10px;
}
button {
  margin: 5px;
}
.active {
  outline: 2px solid yellow;
}
</style>
