<template>
  <a-card type="inner">
    <h4>{{ post.title }}</h4>
    <p>{{ post.body }}</p>
    <a-card-meta>
      <template #description>{{ post.author }}</template>
    </a-card-meta>
  </a-card>
</template>

<script setup lang="ts">
import { IPost } from './types';

defineProps<{ post: { author: string } & IPost }>();
</script>

<style scoped></style>
