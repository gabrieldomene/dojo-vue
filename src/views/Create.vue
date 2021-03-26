<template>
  <div class="create">
    <form>
      <label for="">Title</label>
      <input type="text" v-model="title" required>
      <label for="">Content</label>
      <textarea v-model="body" required></textarea>
      <label for="">Tags (hit enter to add a tag)</label>
      <input
        type="text"
        v-model="tag"
        @keydown.enter.prevent="handleKeyDown"
      >
      <div v-for="tag in tags" :key="tag" class="pill">
        #{{ tag }}
      </div>
      <button @click.prevent="submitPost">Add Post</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  setup() {
    const title = ref('');
    const body = ref('');
    const tag = ref('');
    const tags = ref([] as string[]);

    const handleKeyDown = () => {
      if (!tags.value.includes(tag.value)) {
        tag.value = tag.value.replace(/\s/, '');
        tags.value.push(tag.value);
      }
    };

    const submitPost = async () => {
      const post = {
        title: title.value,
        body: body.value,
        tags: tags.value,
      };
      try {
        await fetch('http://localhost:3000/posts', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify(post),
        })
          .then((response) => console.log(response))
          .catch((error) => console.log(error));
      } catch (error) {
        console.log(error);
      }
    };

    return {
      title,
      body,
      tag,
      handleKeyDown,
      tags,
      submitPost,
    };
  },
});
</script>

<style scoped>
  form {
    max-width: 480px;
    margin: 0 auto;
    text-align: left;
  }
  input, textarea {
    display: block;
    width: 100%;
    margin: 10px 0;
    box-sizing: border-box;
    padding: 10px;
    border: 1px solid #eee;
  }

  textarea {
    height: 160px;
  }

  label {
    display: inline-block;
    margin-top: 30px;
    position: relative;
    font-size: 30px;
    color: #fff;
    margin-bottom: 10px;
  }

  label::before {
    content: "";
    display: block;
    width: 100%;
    height: 100%;
    background: #ff8800;
    position: absolute;
    z-index: -1;
    padding-right: 40px;
    left: -30px;
    transform: rotateZ(-1.5deg);
  }

  button {
    display: block;
    margin-top: 30px;
    background: #ff8800;
    color: white;
    border: none;
    padding: 8px 16px;
    font-size: 18px
  }
  .pill {
    display: inline-block;
    margin: 10px 10px 0 0;
    color: #444;
    background: #ddd;
    padding: 8px;
    border-radius: 20px;
    font-size: 14px;
  }
</style>
