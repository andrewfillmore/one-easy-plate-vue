<template>
  <div id="app">
    <!-- navbar -->
    <nav
      id="topNav"
      class="navbar navbar-default mb-3 navbar-expand-lg fixed-top"
      data-toggle="affix"
    >
      <!-- this toggler only displays on offcanvas layout -->
      <a
        href="#"
        class="
          navbar-toggler-anim
          toggler-offcanvas
          my-auto
          collapsed
          border-0
          mr-2
        "
        data-toggle="collapse"
        data-target="#offcanvasNavbar"
      >
        <span></span>
        <span></span>
        <span></span>
      </a>
      <!-- text brand or logo image goes here -->
      <router-link
        class="navbar-brand page-scroll text-uppercase wide-space link"
        to="/"
        >One Easy Plate</router-link
      >
      <button
        class="navbar-toggler collapsed border-0"
        type="button"
        data-toggle="collapse"
        data-target="#collapsingNavbar"
      >
        <span></span>
        <span></span>
        <span></span>
      </button>
      <div class="collapse navbar-collapse border-0" id="collapsingNavbar">
        <ul class="nav navbar-nav ml-auto">
          <li class="nav-item">
            <router-link class="nav-link page-scroll" to="/about"
              >Find Recipes</router-link
            >
          </li>
          <li v-if="isLoggedIn()" class="nav-item">
            <router-link class="nav-link page-scroll" to="/favorites"
              >My Favorites</router-link
            >
          </li>
          <li v-if="isLoggedIn()" class="nav-item">
            <router-link class="nav-link page-scroll" to="/profile"
              >Profile</router-link
            >
          </li>
          <li v-if="isLoggedIn()" class="nav-item">
            <router-link class="nav-link page-scroll" to="/logout"
              >Logout</router-link
            >
          </li>
          <li v-if="!isLoggedIn()" class="nav-item">
            <router-link class="nav-link page-scroll" to="/login"
              >Login</router-link
            >
          </li>
          <li v-if="!isLoggedIn()" class="nav-item">
            <router-link class="nav-link page-scroll" to="/signup"
              >Signup</router-link
            >
          </li>
        </ul>
      </div>
    </nav>
    <!-- /navbar -->

    <router-view />

    <section class="bg-alt">
      <div class="container wow fadeInUp">
        <h2 class="pb-2">Andrew Fillmore Studio</h2>
        <div class="row">
          <div class="col-lg-3 col-md-6 col-12">
            <div class="card h-100">
              <div class="card-img-top"></div>
              <div class="card-body">
                <a href="mailto: andrew.fillmore@gmail.com"
                  ><i class="icon-lg ion-ios-email-outline"></i
                ></a>
                <h3>Email</h3>
                <p>andrew.fillmore@gmail.com</p>
              </div>
            </div>
          </div>
          <div class="col-lg-3 col-md-6 col-12">
            <div class="card h-100">
              <div class="card-img-top"></div>
              <div class="card-body">
                <a href=""><i class="icon-lg ion-ios-telephone-outline"></i></a>
                <h3 class="card-title">Consult</h3>
                <p>503-804-5099</p>
              </div>
            </div>
          </div>
          <div class="col-lg-6 col-md-12 col-12">
            <div class="card h-100">
              <div class="card-img-top"></div>
              <div class="card-body">
                <a href=""><i class="icon-lg ion-ios-location-outline"></i></a>
                <h3 class="card-title">Chicago, IL</h3>
                <p></p>
              </div>
            </div>
          </div>
        </div>
        <hr />
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data: function () {
    return {};
  },
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
    getUserId: function () {
      return localStorage.getItem("user_id");
    },
  },
};
</script>
