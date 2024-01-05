<template>
  <div :class="{'dark': isDarkTheme}">
    <BaseToggle class="toggle" v-model="isDarkTheme">Dark mode</BaseToggle>
    <TodoList />
  </div>
</template>

<script setup lang="ts">
  import TodoList from './components/TodoList.vue';
  import BaseToggle from './components/BaseToggle.vue';
  import { ref } from 'vue';

  const isDarkTheme = ref(false);
</script>

<style scoped>
.toggle {
  position: absolute;
  top: 18px;
  left: 50%;
  transform: translateX(-50%);
}
</style>
