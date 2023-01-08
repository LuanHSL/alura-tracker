<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <Stopwatch :timeInSeconds="timeInSeconds" />
    <Button
      @when-clicked="handleStartTask"
      title="Play"
      icon="fa-solid fa-play"
      :disabled="stopwatchRunning"
    />
    <Button
      @when-clicked="handleStopTask"
      title="Stop"
      icon="fas fa-stop"
      :disabled="!stopwatchRunning"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, defineAsyncComponent } from 'vue';
const Stopwatch = defineAsyncComponent(() => import('./Stopwatch.vue'));
const Button = defineAsyncComponent(() => import('./Button.vue'));

export default defineComponent({
  name: 'Timer',
  emits: ['when-timer-ended'],
  components: {
    Stopwatch,
    Button,
  },
  data() {
    return {
      timeInSeconds: 0,
      stopwatch: 0,
      stopwatchRunning: false,
    };
  },
  computed: {
    elapsedTime(): string {
      return new Date(this.timeInSeconds * 1000).toISOString().substr(11, 8);
    },
  },
  methods: {
    handleStartTask() {
      this.stopwatchRunning = true;
      this.stopwatch = setInterval(() => {
        this.timeInSeconds++;
      }, 1000);
    },
    handleStopTask() {
      this.stopwatchRunning = false;
      clearInterval(this.stopwatch);
      this.$emit('when-timer-ended', this.timeInSeconds);
      this.timeInSeconds = 0;
    },
  },
});
</script>
