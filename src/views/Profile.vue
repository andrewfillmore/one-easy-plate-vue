<template>
  <div class="users-show">
    <p></p>
    <h1>{{ user.first_name }}'s Profile Page</h1>
    <p>{{ user.first_name }} {{ user.last_name }}</p>
    <p>{{ user.email }}</p>
    <br />
    <h2>You Can Edit Your Profile Here:</h2>
    <form v-on:submit.prevent="updateUser()">
      <label>
        First Name:
        <input type="text" v-model="editUserParams.first_name" />
      </label>
      <br />
      <label>
        Last Name:
        <input type="text" v-model="editUserParams.last_name" />
      </label>
      <br />
      <label>
        Email Address:
        <input type="text" v-model="editUserParams.email" />
      </label>
      <br />
      <label>
        Password:
        <input type="text" v-model="editUserParams.password" />
      </label>
      <br />
      <label>
        Password_confirmation:
        <input type="text" v-model="editUserParams.password_confirmation" />
      </label>
      <br />
      <input type="submit" value="Save Changes" />
      <span v-if="$parent.getUserId() == user.id">
        <button v-on:click="destroyUser()">Delete Account</button>
      </span>
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      user: {},
      errors: [],
      editUserParams: {},
    };
  },
  created: function () {
    axios.get(`/users/${this.$parent.getUserId()}`).then((response) => {
      console.log("User Object", response.data);
      this.user = response.data;
    });
  },
  methods: {
    updateUser: function () {
      axios
        .patch(`/users/${this.$parent.getUserId()}`, this.editUserParams)
        .then((response) => {
          console.log(response.data);
          this.user = response.data;
          this.editUserParams = "";
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          console.log(error.response.data.errors);
        });
    },
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
