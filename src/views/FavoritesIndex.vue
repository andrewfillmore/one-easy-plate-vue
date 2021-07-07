<template>
  <div class="favorites-index">
    <div v-for="favorite in favorites" v-bind:key="favorite.id">
      <h2>{{ favorite.recipe.title }}</h2>
      <img :src="favorite.recipe.image" alt="" />
      <p>{{ favorite.comments }}</p>
      <router-link :to="`/recipes/${favorite.spoonacular_api_recipe_id}`"
        >Go To Recipe</router-link
      >
      <button v-on:click="destroyFavorite(favorite)">Delete Recipe</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      favorites: [],
      recipe: {},
      favorite: [],
    };
  },
  created: function () {
    axios.get("/favorites").then((response) => {
      console.log("Favorites Array", response.data);
      this.favorites = response.data;
    });
  },
  methods: {
    destroyFavorite: function (favorite) {
      if (confirm("Are you sure you want to delete this Recipe?")) {
        axios.delete(`/favorites/${favorite.id}`, favorite).then((response) => {
          console.log(response.data);
          this.$router.push("/");
        });
      }
    },
  },
};
</script>
