<template>
  <Box>
    <div class="columns">
      <div class="column is-7">
        {{ task.description || 'Tarefa sem descrição' }}
      </div>
      <div class="column">
        <Stopwatch :timeInSeconds="task.durationInSeconds" />
      </div>
    </div>
  </Box>
</template>

<script lang="ts">
import type ITask from '@/interfaces/ITask';
import { defineComponent, defineAsyncComponent, type PropType } from 'vue';
const Stopwatch = defineAsyncComponent(() => import('./Stopwatch.vue'));
const Box = defineAsyncComponent(() => import('./Box.vue'));

export default defineComponent({
  name: 'Taks',
  components: {
    Stopwatch,
    Box,
  },
  props: {
    task: {
      type: Object as PropType<ITask>,
      required: true,
    },
  },
});
</script>
