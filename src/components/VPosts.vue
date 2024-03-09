<template>
  <a-list
    :grid="{ xs: 1, sm: 2, md: 2, lg: 3, xl: 4, xxl: 6 }"
    :loading="loading"
    :data-source="dataFiltered"
    :pagination="pagination"
    size="small"
  >
    <template #renderItem="{ item: post }">
      <a-list-item>
        <v-post :post="post" />
      </a-list-item>
    </template>
  </a-list>
</template>

<script setup lang="ts">
import { computed, ref, onBeforeMount } from 'vue';
import { IPost, IUser } from './types';
import VPost from './VPost.vue';

const props = defineProps<{ query: string }>();

const posts = ref<IPost[]>([]);
const users = ref<IUser[]>([]);

const dataMerged = computed(() =>
  posts.value.map((post) => ({
    author: users.value.find(({ id }) => id === post.userId)!.name,
    ...post,
  }))
);

const dataFiltered = computed(() => {
  return props.query
    ? dataMerged.value.filter(({ author }) => {
        return author.toLowerCase().includes(props.query.toLowerCase());
      })
    : dataMerged.value;
});

const loading = ref(true);

onBeforeMount(async () => {
  const url = 'https://jsonplaceholder.typicode.com';

  [posts.value, users.value] = await Promise.all([
    fetch(`${url}/posts`).then((response) => response.json()),
    fetch(`${url}/users`).then((response) => response.json()),
  ]);

  loading.value = false;
});

const current = ref(1);
const size = ref(20);

const pagination = computed(() => ({
  hideOnSinglePage: !dataFiltered.value.length,
  current: current.value,
  // responsive: true,
  pageSize: size.value,
  showSizeChanger: false,
  onChange: (page: number, pageSize: number) => {
    current.value = page;
    size.value = pageSize;
  },
}));
</script>
