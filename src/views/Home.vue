<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h1>Choose Your Protein</h1>
    <h1>Choose Your Vegetable</h1>
    <h1>Choose Your Starch</h1>
    <form v-on:submit.prevent="findRecipes()">
      <label>
        Protein:
        <input type="text" v-model="protein" />
      </label>
      <br />
      <label>
        Veggie:
        <input type="text" v-model="veggie" />
      </label>
      <br />
      <label>
        Starch:
        <input type="text" v-model="carb" />
      </label>

      <br />
      <button>Find Recipes</button>
      <p>{{ recipes }}</p>
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
