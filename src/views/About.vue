<template>
  <div class="about">
    <section id="aboutheader" class="bg-image2">
      <div class="container pt-2">
        <div class="row">
          <div
            class="
              col-xl-7 col-lg-8 col-md-9
              bg-white
              p-4
              mx-1
              wow
              fadeInUp
              hide
            "
          >
            <div class="pt-2 pb-2">
              <h1 class=""><a href="">Choose Your Ingredients</a></h1>
              <div class="card border-secondary">
                <div class="card-body">
                  <form
                    v-on:submit.prevent="findRecipes()"
                    class="form"
                    role="form"
                    autocomplete="off"
                  >
                    <div class="form-group">
                      <label for="inputName">PROTEIN</label>
                      <input
                        type="text"
                        class="form-control"
                        v-model="protein"
                        id="inputName"
                        placeholder="beef? chicken? fish?"
                      />
                    </div>
                    <div class="form-group">
                      <label for="inputName">VEGETABLE</label>
                      <input
                        type="text"
                        class="form-control"
                        v-model="veggie"
                        id="inputName"
                        placeholder="broccoli?"
                      />
                    </div>
                    <div class="form-group">
                      <label for="inputName">CARBOHYDRATE</label>
                      <input
                        type="text"
                        class="form-control"
                        v-model="carb"
                        id="inputName"
                        placeholder="rice? pasta? potato?"
                      />
                    </div>

                    <div class="form-group">
                      <button
                        type="submit"
                        class="btn btn-success btn-lg float-right"
                      >
                        Find Recipes
                      </button>
                    </div>
                  </form>
                </div>
              </div>
            </div>
          </div>
          <div class="col-xl-4 col-lg-4 col-md-3"></div>
        </div>
      </div>
    </section>
    <section class="bg-alt">
      <div class="container py-5">
        <div class="row">
          <div
            class="col-sm-4 col-6 media py-3"
            v-for="recipe in recipes"
            v-bind:key="recipe.id"
          >
            <div class="card card-default text-center">
              <div class="card-img-top card-zoom">
                <router-link :to="`/recipes/${recipe.id}`"
                  ><img class="img-fluid" :src="recipe.image" alt="Card image"
                /></router-link>
              </div>
              <div class="card-body">
                <h6>{{ recipe.title }}</h6>
                <h6>{{ recipe.usedIngredients["originalName"] }}</h6>
                <p class="card-text"></p>
                <hr class="accent my-4" />
                <div
                  class="
                    d-flex
                    justify-content-center
                    flex-column flex-sm-row
                    mt-2
                  "
                ></div>
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
    </section>

    <!-- <div class="container pb-2">
      <div class="row">
        <div class="col-xl-4 col-lg-4 col-md-5 pt-2 pb-2">
          <div class="recipes-index">
            <div v-for="recipe in recipes" v-bind:key="recipe.id">
              <h2>{{ recipe.title }}</h2>
              <br />

              <img :src="recipe.image" alt="" />
              <br />

              <router-link :to="`/recipes/${recipe.id}`"
                >View Recipe</router-link
              >
            </div>
          </div>
        </div>
        <div
          class="
            col-xl-4
            ml-xl-auto
            col-lg-4
            ml-lg-auto
            col-md-5
            ml-md-auto
            pt-2
            pb-2
          "
        >
          <blockquote class="blockquote wow fadeIn">
            <h3 class="text-right pt-2">
              Founded by people that love code &amp; design.
            </h3>
          </blockquote>
        </div>
      </div>
    </div> -->
  </div>
</template>
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
