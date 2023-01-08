<template>
  <div class="box has-text-weight-bold">
    <div class="columns">
      <div class="column is-7">
        {{ task.description }}
      </div>
      <div class="column">
        <Stopwatch :timeInSeconds="task.durationInSeconds" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import type ITask from '@/interfaces/ITask';
import { defineComponent, defineAsyncComponent, type PropType } from 'vue';
const Stopwatch = defineAsyncComponent(() => import('./Stopwatch.vue'));

export default defineComponent({
  name: 'Taks',
  components: {
    Stopwatch,
  },
  props: {
    task: {
      type: Object as PropType<ITask>,
      required: true,
    },
  },
});
</script>

<style scoped>
.box {
  background-color: #FAF0CA;
}
</style>
