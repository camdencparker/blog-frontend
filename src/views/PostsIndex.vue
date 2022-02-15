<script>
import axios from "axios";

export default {
  data: function () {
    return {
      posts: [],
    };
  },
  created: function () {
    axios.get("/posts").then((response) => {
      console.log(response.data);
      this.posts = response.data;
    });
  },
  methods: {},
};
</script>

<template>
  <div class="login"></div>
  <div v-for="post in posts" v-bind:key="post.id">
    <h1>{{ post.title }}</h1>
    <router-link v-bind:to="`/posts/${this.$route.params.id}`">
      <img :src="post.image" :alt="post.title" />
    </router-link>
  </div>
</template>
