<template>
  <div class="recipes-show">
    <h2>{{ recipe.title }}</h2>
    <h4>{{ recipe.servings }} servings</h4>

    <h2>Prep Time: {{ recipe.readyInMinutes }} minutes</h2>
    <img :src="recipe.image" alt="" />
    <h3>Ingredients:</h3>
    <div
      v-for="extendedIngredient in recipe.extendedIngredients"
      v-bind:key="extendedIngredient.id"
    >
      <p>
        {{ extendedIngredient.amount }}
        {{ extendedIngredient.unit }} {{ extendedIngredient.name }}
      </p>
    </div>
    <h3>Summary</h3>
    <div>
      <p><span v-html="recipe.summary"></span></p>
    </div>
    <h3>Instructions</h3>
    <div>
      <p><span v-html="recipe.instructions"></span></p>
    </div>
    <!-- <div v-for="comment in favorite.comments">
     <p> {{comment}}</p>
   </div> -->

    <form v-on:submit.prevent="addFavorite()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Add Comments: </label>
        <input type="text" v-model="comments" />
      </div>
      <input type="submit" value="Add Recipe to Favorites" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      recipe: {},
      comments: "",
      errors: [],
      favorites: [],
      favorite: {},
    };
  },
  created: function () {
    axios.get(`/recipes/${this.$route.params.id}`).then((response) => {
      console.log("Recipe object", response.data);
      this.recipe = response.data;
    });
    axios.get("/favorites").then((response) => {
      console.log("Favorites Array", response.data);
      this.favorites = response.data;
    });
    // for (var i = 0; i < this.favorites.length; i++) {
    //   if (this.favorites[i].recipe == this.recipe) {
    //     this.favorite = this.favorites[i];
    //     console.log(this.favorite);
    //   }
    // }
  },
  methods: {
    addFavorite: function () {
      var params = {
        comments: this.comments,
        spoonacular_api_recipe_id: this.recipe.id,
      };
      axios
        .post("/favorites", params)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/favorites");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
