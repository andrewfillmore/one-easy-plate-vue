<template>
  <div class="users-show">
    <p>
      Current logged in user: {{ typeof $parent.getUserId() }}
      {{ $parent.getUserId() }}
    </p>
    <p>{{ user.first_name }}</p>
    <p>{{ user.email }}</p>

    <span v-if="$parent.getUserId() == user.id">
      <router-link :to="`/users/${user.id}/edit`">Edit</router-link> |
      <button v-on:click="destroyUser()">Delete Account</button>
    </span>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      user: { id: 6 },
    };
  },
  created: function () {
    axios.get("/users/${this.params.id}").then((response) => {
      console.log("User Object", response.data);
      this.user = response.data;
    });
  },
  methods: {
    destroyUser: function () {
      if (confirm("Are you sure you want to delete this User?")) {
        axios.delete(`/users/${this.user.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/");
        });
      }
    },
  },
};
</script>
