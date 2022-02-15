<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
      editPostParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.post = response.data;
      this.editPostParams = this.post;
    });
  },
  methods: {
    updatePost: function () {
      axios
        .patch(`/posts/${this.$route.editPostParams.id}`, this.editPostParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    destroyPost: function () {
      if (confirm("Do You Want to delete this")) {
        axios.delete(`/posts/${this.$route.editPostParams.id}`).then((response) => {
          console.log("Success", response.data);
          this.$router.push("/posts");
        });
      }
    },
  },
};
</script>

<template>
  <div class="posts-edit">
    <form v-on:submit.prevent="updatePost()">
      <h1>Edit Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <p>{{ editPostParams }}</p>
      <img :src="editPostParams.image" alt="" />
      <div>
        <label>Title:</label>
        <input type="text" v-model="editPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="editPostParams.body" />
      </div>
      <div>
        <label>image:</label>
        <input type="text" v-model="editPostParams.image" />
      </div>
      <button v-on:click="destroyPost()">Delete</button>
      <input type="submit" value="Update" />
    </form>
  </div>
</template>
