<template>
  <main class="columns is-gapless is-multiline">
    <div class="column is-one-quarter">
      <SideBar />
    </div>
    <div class="column is-three-quarter">
      <Form @when-save-task="saveTask" />
      <div class="list">
        <Task
          v-for="(task, index) in taskList"
          :key="index"
          :task="task"
        />
        <Box v-if="isEmptyTaskList">
          Você não está muito produtivo hoje :(
        </Box>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent, defineAsyncComponent } from 'vue';
const SideBar = defineAsyncComponent(() => import('./components/SideBar.vue'));
const Form = defineAsyncComponent(() => import('./components/Form.vue'));
const Task = defineAsyncComponent(() => import('./components/Task.vue'));
const Box = defineAsyncComponent(() => import('./components/Box.vue'));

import type ITask from './interfaces/ITask';

export default defineComponent({
  name: 'App',
  components: {
    SideBar,
    Form,
    Task,
    Box,
  },
  data() {
    return {
      taskList: [] as ITask[],
    };
  },
  computed: {
    isEmptyTaskList(): boolean {
      return this.taskList.length === 0;
    },
  },
  methods: {
    saveTask(task: ITask) {
      this.taskList.push(task);
    },
  }
});
</script>

<style scoped>
.list {
  padding: 1.25rem;
}

</style>
