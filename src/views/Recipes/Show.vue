<template>
  <div class="recipes-show">
    <h2>{{ recipe.title }}</h2>
    <img :src="recipe.image" alt="" />
    <p>{{ recipe.directions }}</p>
    <p>{{ recipe.ingredients }}</p>
    <!-- <router-link :to="`/recipes/${recipe.id}/edit`">Edit</router-link> -->
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      recipe: {},
    };
  },
  created: function () {
    axios.get(`/recipes/${this.$route.params.id}`).then((response) => {
      console.log("Recipe object", response.data);
      this.recipe = response.data;
    });
  },
  methods: {},
};
</script>
