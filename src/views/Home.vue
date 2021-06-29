<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h1>New User</h1>
    <div>
      First Name:
      <input type="text" v-model="newUser.first_name" />
      <br />
      Last Name:
      <input type="text" v-model="newUser.last_name" />
      <br />
      Email:
      <input type="text" v-model="newUser.email" />
      <br />
      Password:
      <input type="text" v-model="newUser.password" />
      <br />
      Password Confirmation:
      <input type="text" v-model="newUser.password_confirmation" />
      <br />
      <button v-on:click="createUser()">Create User</button>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to One Easy Plate!",
      newUser: {},
    };
  },
  created: function () {},
  methods: {
    createUser: function () {
      var params = {
        first_name: this.newUser.first_name,
        last_name: this.newUser.last_name,
        email: this.newUser.email,
        password: this.newUser.password,
        password_confirmation: this.newUser.password_confirmation,
      };
      axios
        .post("/users", params)
        .then((response) => {
          console.log("users create", response);
          this.users.push(response.data);
          this.newUser = {};
        })
        .catch((error) => {
          console.log("users create error", error.response);
        });
    },
  },
};
</script>
