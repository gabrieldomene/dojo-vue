<template>
  <div v-if="error">{{ error }}</div>
  <div v-if="post" class="post">
    <h3>{{ post.title }}</h3>
    <p class="pre">{{ post.body }}</p>
  </div>

  <div v-else>
    <Spinner />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import getPost from '@/composables/getPost';
import Spinner from '@/components/Spinner.vue';

export default defineComponent({
  props: ['id'],
  components: { Spinner },
  setup(props) {
    const { post, error, load } = getPost(props.id);
    load();

    return { post, error };
  },
});
</script>

<style>
  .post {
    max-width: 1200px;
  }

  .post p {
    color: #444;
    line-height: 1.5em;
    margin-top: 40px;
  }

  .pre {
    white-space: pre-wrap;
  }
</style>
