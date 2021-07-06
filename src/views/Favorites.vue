<template>
  <div class="favorites">
    <div v-for="favorite in favorites" v-bind:key="favorite.id">
      <h2>{{ favorite.title }}</h2>
      <!-- <img :src="recipe.image" alt="" /> -->
    </div>

    <router-link :to="`/recipes/${recipe.id}`">Go to Recipe</router-link>
    <span v-if="$parent.getRecipeId() == recipe.id">
      <button v-on:click="destroyRecipe()">Delete Recipe</button>
    </span>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      favorites: [],
    };
  },
  created: function () {
    axios.get("/favorites").then((response) => {
      console.log("Favorites Array", response.data);
      this.favorites = response.data;
    });
  },
  methods: {
    destroyRecipe: function () {
      if (confirm("Are you sure you want to delete this Recipe?")) {
        axios.delete(`/recipes/${this.recipe.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/");
        });
      }
    },
  },
};
</script>
