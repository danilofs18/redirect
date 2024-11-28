<script setup lang="ts">
import { useAsyncState } from '@vueuse/core';
import { computed, onBeforeMount } from 'vue';

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
  const response = await fetch('redirect/data/config.json');
  return response.json();
}

const iframeSrc = computed(() => {
  if (!config.value) return null;
  return `http://${config.value.ip}:${config.value.port}`;
});

onBeforeMount(() => {
  void execute();
});
</script>

<template>
  <div class="fixed inset-0">
    <iframe
      v-if="!isLoading && iframeSrc"
      title="De gustibus non est disputandum"
      width="100%"
      height="100%"
      class="border-none border-0"
      :src="iframeSrc"
    ></iframe>

    <div v-else class="fixed inset-0 flex items-center justify-center">
      <p class="font-bold text-xl">Carregando...</p>
    </div>
  </div>
</template>
