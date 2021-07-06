<template>
  <div class="favorites-index">
    <div v-for="favorite in favorites" v-bind:key="favorite.id">
      <h2>{{ favorite.title }}</h2>
      <img :src="favorite.image" alt="" />
      <p>{{ favorite.comments }}</p>
      <button v-on:click="showFavorite(favorite)">Go to Recipe</button>
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
    };
  },
  created: function () {
    axios.get("/favorites").then((response) => {
      console.log("Favorites Array", response.data);
      this.favorites = response.data;
    });
  },
  methods: {
    showFavorite: function () {
      this.$router.push("/favorites/${favorite.id}");
    },
    destroyFavorite: function (favorite) {
      if (confirm("Are you sure you want to delete this Recipe?")) {
        axios
          .delete(`/favorites/${this.favorite.id}`, favorite)
          .then((response) => {
            console.log(response.data);
            this.$router.push("/");
          });
      }
    },
  },
};
</script>
