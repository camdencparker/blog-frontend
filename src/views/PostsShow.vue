<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log("Posts Show:", response.data);
      this.posts = response.data;
    });
  },
  methods: {},
};
</script>

<template>
  <div class="posts-show">
    <h1>Title: {{ post.title }}</h1>
    <p>Body: {{ post.body }}</p>
    <img :src="post.image" :alt="post.title" />
  </div>
</template>
