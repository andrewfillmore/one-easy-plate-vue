<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <router-link :to="`/about/`">Get Started</router-link>
    <br />
    <router-link :to="`/login/`">Login</router-link>
    <br />
    <router-link :to="`/signup/`">Sign Up</router-link>
    <br />
  </div>
</template>

<style></style>

<script>
// import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to One Easy Plate!",
    };
  },
  created: function () {},
  methods: {},
};
</script>
