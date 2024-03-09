<template>
  <a-input-search
    allowClear
    v-model:value="value"
    placeholder="Filter by author..."
    enter-button
  />
</template>

<script setup lang="ts">
import { ref } from 'vue';

const value = ref('');
</script>
