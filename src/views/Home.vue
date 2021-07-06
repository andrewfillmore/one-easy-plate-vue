<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <form v-on:submit.prevent="findRecipes()">
      <label>
        Chooses a Protein:
        <input type="text" v-model="protein" />
      </label>
      <br />
      <label>
        Choose a Veggie:
        <input type="text" v-model="veggie" />
      </label>
      <br />
      <label>
        Choose a Carb:
        <input type="text" v-model="carb" />
      </label>

      <br />
      <button>Find Recipes</button>
      <div class="recipes-index">
        <div v-for="recipe in recipes" v-bind:key="recipe.id">
          {{ recipe.title }}
          <br />
          {{ recipe.cuisine }}
          <router-link :to="`/recipes/${recipe.id}`">View Recipe</router-link>
        </div>
      </div>
      <!-- <span v-if="$parent.getUserId() == user.id">
        <button v-on:click="destroyUser()">Delete Account</button>
      </span> -->
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to One Easy Plate!",
      recipes: [],
      protein: "",
      carb: "",
      veggie: "",
      recipe: {},
    };
  },
  created: function () {},
  methods: {
    findRecipes: function () {
      axios
        .get(`/recipes?query=${this.protein},${this.veggie},${this.carb}`)
        .then((response) => {
          console.log("Recipe Object", response.data);
          this.recipes = response.data;
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
