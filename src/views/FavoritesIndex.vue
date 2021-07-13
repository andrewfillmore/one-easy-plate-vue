<template>
  <div class="favorites-index">
    <div class="row my-4 pt-1">
      <div class="col-12 col-md-4 ml-md-auto ml-auto">
        <div class="input-group add-on">
          <input
            type="text"
            class="form-control"
            v-model="searchTerm"
            list="titles"
            placeholder=" "
          />
          <div class="input-group-btn">
            <button
              class="
                btn btn-secondary
                border-left-0 border-right-0 border-top-0
              "
              type="submit"
            >
              <i class="ion-ios-search-strong"></i>
            </button>
          </div>
        </div>
        <small class="ml-2">search your favorites</small>
      </div>
    </div>
    <div class="container py-5">
      <div class="row">
        <datalist id="titles">
          <option v-for="favorite in favorites" v-bind:key="favorite.id">
            {{ favorite.recipe.title }}
          </option>
        </datalist>
        <div
          class="col-sm-4 col-6 media py-3"
          v-for="favorite in filterBy(favorites, searchTerm)"
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
              <hr class="accent my-4" />
              <div
                class="
                  d-flex
                  justify-content-center
                  flex-column flex-sm-row
                  mt-2
                "
              >
                <button v-on:click="destroyFavorite(favorite)" class="btn mr-1">
                  Delete Recipe
                </button>
              </div>
              <!-- <h5 class="mt-2">
                <a
                  href=""
                  v-on:click="destroyFavorite(favorite)"
                  class="badge badge-pill badge-warning"
                  >Delete Recipe</a
                >
              </h5> -->
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      favorites: [],
      recipe: {},
      favorite: [],
      searchTerm: "",
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
