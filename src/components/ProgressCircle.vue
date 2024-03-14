<template>
  <div class="progress-circle">
    <span class="number">{{ animatedNumberValue }}%</span>
    <svg height="150" width="150" class="circle">
      <circle
          cx="75"
          cy="75"
          r="65"
          stroke="#4f4466"
          stroke-width="15"
          fill="none"
      />
      <circle
          id="progress-bar"
          cx="75"
          cy="75"
          r="65"
          stroke="#f9dc5c"
          stroke-width="15"
          stroke-linecap="round"
          fill="none"
          :style="{ strokeDasharray: '410', strokeDashoffset: (410 - (4.1 * progressValue)) }"
          filter="url(#glow)"
      />
      <defs>
        <filter id="glow">
          <feGaussianBlur in="SourceGraphic" stdDeviation="3" result="glow" />
          <feMerge>
            <feMergeNode in="glow"/>
            <feMergeNode in="SourceGraphic"/>
          </feMerge>
        </filter>
      </defs>
    </svg>
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
  data() {
    return {
      oldValue: 0,
      newValue: 0,
      animatedNumberValue: 0,
      currentValue: 0,
      interval: null
    };
  },
  watch: {
    progressValue(newValue) {
      this.oldValue = this.newValue;
      this.newValue = newValue;
      clearInterval(this.interval);
      this.interval = setInterval(() => {
        if (this.currentValue < this.newValue) {
          this.currentValue++;
        } else if (this.currentValue > this.newValue) {
          this.currentValue--;
        }
        this.animatedNumberValue = this.currentValue;
        if (this.currentValue === this.newValue) {
          clearInterval(this.interval);
        }
      }, 15);
    }
  }
};
</script>

<style scoped>
.progress-circle {
  position: relative;
  width: 150px;
  height: 150px;
  border-radius: 50%;
}
.number {
  font-size: 30px;
}
.progress-circle::after,
.number {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.circle {
  transform: rotate(-90deg);
}
#progress-bar {
  transition: stroke-dashoffset 1s ease;
}
</style>
