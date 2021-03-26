<template>
  <div class="post-list">
    <div v-for="post in posts" :key="post.id">
      <SinglePost :post="post" />
    </div>
  </div>
</template>

<script lang="ts">
import {
  defineComponent,
} from 'vue';
import SinglePost from '@/components/SinglePost.vue';

export default defineComponent({
  props: ['posts'],
  components: { SinglePost },

});
</script>

<style>

</style>
