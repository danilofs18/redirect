<script setup lang="ts">
import { useAsyncState } from '@vueuse/core';
import Button from '@/components/Button.vue';
import { computed, onBeforeMount, onMounted } from 'vue';

const {
  state: config,
  isLoading,
  execute,
} = useAsyncState(fetchConfig, null, {
  immediate: false,
  resetOnExecute: true,
  throwError: false,
});

async function fetchConfig(): Promise<Config> {
  const response = await fetch('data/config.json');
  return response.json();
}

const src = computed(() => {
  if (!config.value) return null;
  return `http://${config.value.ip}:${config.value.port}`;
});

function navigate() {
  if (src.value) {
    window.location.assign(src.value);
  }
}

onBeforeMount(() => {
  void execute();
});

onMounted(() => {
  setTimeout(() => navigate(), 5000);
});
</script>

<template>
  <div class="fixed inset-0 flex items-center justify-center">
    <Button v-if="!isLoading && src" @click="() => navigate()">Redirecionar</Button>
    <p v-else class="font-bold text-xl">Carregando...</p>
  </div>
</template>
