<template>
  <div class="favorites-index">
    <div class="container py-5">
      <div class="row">
        <div
          class="col-sm-4 col-6 media py-3"
          v-for="favorite in favorites"
          v-bind:key="favorite.id"
        >
          <div class="card card-default text-center">
            <div class="card-img-top card-zoom">
              <router-link
                :to="`/recipes/${favorite.spoonacular_api_recipe_id}`"
                ><img
                  class="img-fluid"
                  :src="favorite.recipe.image"
                  alt="Card image"
              /></router-link>
            </div>
            <div class="card-body">
              <h6>{{ favorite.recipe.title }}</h6>
              <p class="card-text">{{ favorite.comments }}</p>
              <button
                class="btn btn-secondary"
                v-on:click="destroyFavorite(favorite)"
              >
                Delete Recipe
              </button>
              <button class="btn btn-secondary">Recipe Saved!</button>
            </div>
          </div>
        </div>
      </div>
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
          for (var i = 0; i < this.favorites.length; i++) {
            if (this.favorites[i] === favorite) {
              this.favorites.splice(i, 1);
            }
          }
        });
      }
    },
  },
};
</script>
