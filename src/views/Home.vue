<template>
  <div class="home">
    <h1>Home</h1>
    <div v-if="error">{{ error }}</div>
    <div v-if="posts.length">
      <PostList :posts="posts" />
    </div>
    <div v-else>
      <Spinner />
    </div>

  </div>
</template>

<script lang="ts">
import {
  defineComponent,
} from 'vue';
import PostList from '@/components/PostList.vue';
import getPosts from '@/composables/getPosts';
import Spinner from '@/components/Spinner.vue';

export default defineComponent({
  name: 'Home',
  components: { PostList, Spinner },
  setup() {
    const { posts, error, load } = getPosts();

    load();

    return { posts, error };
  },
});
</script>

<style>
</style>
