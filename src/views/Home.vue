<template>
  <div class="home">
    <div id="top" class="bg-white">
      <div class="header-content container py-5">
        <div class="row">
          <div class="col-xl-4 col-lg-4 col-md-5 py-3">
            <h1 class="display-2 pt-3 mb-5">
              <a href="" class="link">
                <span
                  class="text-typing line-1 wow fadeIn"
                  data-wow-delay="1.2s"
                  >Welcome,
                </span>
                <br />
                <span
                  class="text-typing line-2 wow fadeIn"
                  data-wow-delay="1.4s"
                >
                  this is </span
                ><br />
                <span
                  class="text-typing line-3 wow fadeIn text-highlight"
                  data-wow-delay="1.6s"
                  >One Easy Plate.</span
                >
              </a>
            </h1>
          </div>
          <div
            class="
              col-xl-4
              ml-xl-auto
              col-lg-4
              ml-lg-auto
              col-md-5
              ml-md-auto
              py-3
            "
          >
            <blockquote class="blockquote">
              <h3 class="text-right pt-3">
                <!-- {{ message }} -->
              </h3>
              <br />
              <h3 class="text-right">
                <!-- <a href="" class="text-muted link small"
                  >3 ingredients to a healthy meal</a
                > -->
              </h3>
            </blockquote>
          </div>
        </div>
      </div>
    </div>
    <!-- <body class="preload"> -->
    <header id="first" class="bg-image-jungle bg-fixed bg-cover">
      <div class="header-content container py-3">
        <div class="row vcenter">
          <div class="col-xl-5 col-lg-4 col-md-3"></div>
          <div
            class="col-xl-7 col-lg-8 col-md-9 bg-white wow fadeIn"
            style="border-radius: 15px"
          >
            <div class="p-4">
              <h1 class="pt-2">Simple Recipes + Healthy Meals</h1>
            </div>

            <div class="p-3">
              <p class="lead pt-2 pr-2">
                Choose a Protein, a Vegetable, and a Carbohydrate:
              </p>
              <p class="lead pt-2 pr-2">
                We'll give you one easy plate to plan, prepare, and enjoy. Just
                three simple steps for tasty and nutritious recipes you can make
                in no time.
              </p>

              <p class="lead pt-2 pr-2">
                To get started, sign up or login here: <br />
              </p>
              <!-- <br /> -->
              <div class="row pt-2">
                <div class="col-md-12 pt-2 pb-2">
                  <router-link
                    :to="`/signup/`"
                    class="btn btn-outline-secondary btn-lg"
                  >
                    Sign Up </router-link
                  >&nbsp;&nbsp;

                  <router-link
                    :to="`/login/`"
                    class="btn btn-outline-secondary btn-lg"
                    data-toggle="modal"
                    data-target="#contactModal"
                  >
                    Login
                  </router-link>
                </div>

                <div class="col-md-12 pt-2 pb-2">
                  <hr />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- </body> -->
  </div>
</template>

<style></style>

<script>
// import axios from "axios";
export default {
  data: function () {
    return {
      message:
        "We're doing this because we know it can be overwhelming to think of healthy meals. We want to give you a complete meal recipe based on ingredients you have at home. Just choose a Protein, Vegetable, and Carbohydrate, and we'll find you delicious, simple recipes to make in no time.",
    };
  },
  created: function () {},
  methods: {},
};
</script>
