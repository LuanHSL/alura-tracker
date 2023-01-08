<template>
  <header>
    <h1>
      <img src="../assets/logo.svg" alt="logo">
    </h1>
    <button class="button" @click="handleChangeTheme">
      {{ textButton }}
    </button>
  </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'SideBar',
  emits: ['when-changed-theme'],
  data() {
    return {
      isActiveDarkMode: false,
    };
  },
  computed: {
    textButton() {
      return this.isActiveDarkMode ? 'Desativar modo escuro' : 'Ativar modo escuro';
    },
  },
  methods: {
    handleChangeTheme() {
      this.isActiveDarkMode = !this.isActiveDarkMode;
      this.$emit('when-changed-theme', this.isActiveDarkMode);
    },
  }
});
</script>

<style scoped>
header {
  padding: 1rem;
  background: #0d3d66;
  width: 100%;
  height: 100vh;
  text-align: center;
}
h1 > img {
  width: 10rem;
}
@media only screen and (max-width: 768px) {
  header {
    padding: 2.5rem;
    height: auto;
  }
}
</style>