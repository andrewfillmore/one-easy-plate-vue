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
        <input type="text" v-model="starch" />
      </label>

      <br />
      <input type="submit" value="Find Recipes" />
      <span v-if="$parent.getUserId() == user.id">
        <button v-on:click="destroyUser()">Delete Account</button>
      </span>
    </form>
  </div>
</template>

<style></style>

<script>
// import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to One Easy Plate!",
      protein: "",
      veggie: "",
      starch: "",
      recipes: {},
    };
  },
  created: function () {

  },
  methods: {
    updateUser: function () {
      axios
        .patch(`/users/${this.$parent.getUserId()}`, this.editUserParams)
        .then((response) => {
          console.log(response.data);
          this.user = response.data;
          this.editUserParams = "";
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          console.log(error.response.data.errors);
        });
    },
    destroyUser: function () {
      if (confirm("Are you sure you want to delete this User?")) {
        axios.delete(`/users/${this.user.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/");
        });
      }
    },
  },
//   methods: {

      findRecipe: function () {
        query = this.protein +","+ this.veggie +","+ this.starch
        axios
          .get(`/recipes/${this.query}`, query )
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

},
// };
</script>
