<template>
  <a-flex vertical class="layout">
    <a-row justify="center">
      <a-col :xxl="4" class="search">
        <v-search @search="onSearch" />
      </a-col>
    </a-row>
    <a-row align="middle" class="list">
      <a-col :span="24">
        <v-posts :query="query" />
      </a-col>
    </a-row>
  </a-flex>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import VSearch from './components/VSearch.vue';
import VPosts from './components/VPosts.vue';

const query = ref('');

const onSearch = (value: string) => (query.value = value);
</script>

<style scoped>
.header {
  color: white;
  text-align: center;
}

.layout {
  height: 100vh;
}

.search {
  padding: 1rem;
}

.list {
  flex-grow: 1;
  padding: 0 1rem 1rem;
}
</style>
