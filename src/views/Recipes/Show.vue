<template>
  <div class="recipes-show">
    <!-- <body class="preload"> -->
    <div class="inc_" data-template="./partials/p_header.html"></div>
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-7 py-4">
          <!-- main content -->
          <div>
            <h1 class="display-3 mt-4 mb-2">{{ recipe.title }}</h1>
            <br />
            <br />
            <p>
              <span v-html="recipe.summary"></span>
            </p>
            <br />
            <hr class="accent" />
            <br />
            <h3 class="mb-0 my-2">Directions</h3>
            <p>
              <span v-html="recipe.instructions"></span>
            </p>

            <p></p>
          </div>
          <br />
          <br />
          <div class="card border-secondary" style="border: 0px">
            <div class="card-header" style="padding: 0px"></div>
            <div class="card-body">
              <form
                v-if="!recipe.already_favorite"
                v-on:submit.prevent="addFavorite()"
                class="form"
                role="form"
                autocomplete="off"
              >
                <ul>
                  <li v-for="error in errors" v-bind:key="error">
                    {{ error }}
                  </li>
                </ul>
                <fieldset>
                  <label for="message2" class="mb-0">Leave Comments Here</label>
                  <div class="row mb-1">
                    <div class="col-lg-11">
                      <textarea
                        v-model="comments"
                        rows="3"
                        name="message2"
                        id="message2"
                        class="form-control"
                        required
                      ></textarea>
                    </div>
                  </div>
                  <button
                    type="submit"
                    class="btn btn-secondary btn-md float-right mt-3"
                  >
                    Save Recipe to Favorites
                  </button>
                </fieldset>
              </form>
            </div>
          </div>

          <hr />
        </div>
        <div
          style="background-color: #f6f7f7"
          class="col-lg-4 col-md-5 py-2 bg-alt"
        >
          <!-- sidebar content -->
          <div class="card card-default my-2">
            <div class="card-img-top wow fadeIn">
              <img :src="recipe.image" alt="" class="mx-auto img-fluid" />
            </div>
            <div class="card-body py-2">
              <h2 class="card-title">
                Prep Time: {{ recipe.readyInMinutes }} minutes
              </h2>
              <h6 class="small text-wide">Servings: {{ recipe.servings }}</h6>
            </div>
          </div>
          <br />
          <br />
          <br />
          <div class="card card-default">
            <div class="card-body">
              <h3>Ingredients</h3>
              <div
                v-for="extendedIngredient in recipe.extendedIngredients"
                v-bind:key="extendedIngredient.id"
                class="row p-1"
              >
                <p class="">
                  {{ extendedIngredient.amount }}
                  {{ extendedIngredient.unit }}
                  {{ extendedIngredient.name }}
                </p>

                <!-- <div class="col-12"> -->
                <!-- <img src="" class="img-fluid" /> -->
                <!-- <hr /> -->
                <!-- <p class="">
                    {{ extendedIngredient.amount }}
                    {{ extendedIngredient.unit }}
                    {{ extendedIngredient.name }}
                  </p> -->
                <!-- <button class="btn btn-secondary">Save to Favorites</button> -->
                <!-- </div> -->
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- </body> -->

    <!-- My Original Code -->

    <!-- <h2>{{ recipe.title }}</h2>
    <h4>{{ recipe.servings }} servings</h4> -->

    <!-- <h2>Prep Time: {{ recipe.readyInMinutes }} minutes</h2>
    <img :src="recipe.image" alt="" />
    <h3>Ingredients:</h3> -->
    <!-- <div
      v-for="extendedIngredient in recipe.extendedIngredients"
      v-bind:key="extendedIngredient.id"
    >
      <p>
        {{ extendedIngredient.amount }}
        {{ extendedIngredient.unit }} {{ extendedIngredient.name }}
      </p>
    </div> -->
    <!-- <h3>Summary</h3> -->
    <!-- <div>
      <p><span v-html="recipe.summary"></span></p>
    </div> -->
    <!-- <h3>Instructions</h3> -->
    <!-- <div> -->
    <!-- <p><span v-html="recipe.instructions"></span></p> -->
    <!-- </div> -->
    <!-- <div v-for="comment in favorite.comments" v-bind:key="comment.id"> -->
    <!-- <p>{{ comment }}</p> -->
    <!-- </div> -->

    <!-- <form v-if="!recipe.already_favorite" v-on:submit.prevent="addFavorite()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Add Comments: </label>
        <input type="text" v-model="comments" />
      </div>
      <input type="submit" value="Add Recipe to Favorites" />
    </form> -->
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
