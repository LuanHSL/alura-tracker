<template>
  <button class="button" @click="onClick" :disabled="disabled">
    <span v-if="icon" class="icon">
      <i :class="icon"></i>
    </span>
    <span>{{ title }}</span>
  </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Button',
  emits: ['when-clicked'],
  props: {
    title: {
      type: String,
      required: true,
    },
    icon: {
      type: String,
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    onClick(): void {
      this.$emit('when-clicked');
    },
  },
});
</script>
