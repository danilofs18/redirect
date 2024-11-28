<script setup lang="ts">
import type { VNode } from 'vue';

defineSlots<{ default: () => VNode }>();
</script>

<template>
  <button type="button" class="transition-all">
    <slot></slot>
  </button>
</template>

<style scoped>
button {
  border: 1px solid #8a938c;
  border-radius: 6px;
  background-color: transparent;
  padding: 0.4rem 0.75rem;
  min-width: 10ch;
  min-height: 32px;
  color: inherit;
  font-weight: 500;
  font-size: 1rem;
  font-family: inherit;
  text-align: center;
}

button:hover {
  box-shadow: 0 0 1px 1px rgb(0 0 0 / 15%);
  border-color: #6fdba8;
  color: #6fdba8;
}
</style>
