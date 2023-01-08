<template>
  <div class="box">
    <div class="columns">
      <div
        class="column is-8"
        role="form"
        aria-label="Form for creating of a new task"
      >
        <input
          type="text"
          class="input"
          placeholder="What task do you want to start?"
          v-model="description"
        />
      </div>
      <div class="column">
        <Timer @when-timer-ended="handleTaskEnded" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, defineAsyncComponent } from 'vue';
const Timer = defineAsyncComponent(() => import('./Timer.vue'));

export default defineComponent({
  name: 'Form',
  emits: ['when-save-task'],
  components: {
    Timer,
  },
  data() {
    return {
      description: ''
    };
  },
  methods: {
    handleTaskEnded(elapsedTime: number): void {
      this.$emit('when-save-task', {
        durationInSeconds: elapsedTime,
        description: this.description,
      });
      this.description = '';
    },
  },
});
</script>
