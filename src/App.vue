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
              >About</router-link
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

    <footer id="footer" class="pt-5">
      <div class="container">
        <div class="row">
          <div class="col-lg-6">
            <p class="display-2 mb-2">Okay, Boss.</p>
          </div>
        </div>
        <div class="row">
          <div class="col-6 col-md-3">
            <h6 class="text-uppercase">Information</h6>
            <ul class="list-unstyled">
              <li><a href="./products.html">Products</a></li>
              <li><a href="./faq.html">FAQ&apos;s</a></li>
              <li><a href="./portfolio.html">Gallery</a></li>
              <li><a href="./clients.html">Clients</a></li>
            </ul>
          </div>
          <div class="col-6 col-md-3 column">
            <h6 class="text-uppercase">About</h6>
            <ul class="list-unstyled">
              <li><a href="./contact.html">Contact Us</a></li>
              <li><a href="./about.html">Our Mission</a></li>
              <li><a href="./legal.html">Privacy Policy</a></li>
              <li><a href="./legal.html">Terms &amp; Conditions</a></li>
            </ul>
          </div>
          <div class="col-12 col-md-3 column">
            <h6 class="text-uppercase">Stay Posted</h6>
            <form>
              <div class="form-group">
                <input
                  type="text"
                  class="form-control"
                  title="Enter your email. No spam, we promise!"
                  placeholder=""
                />
              </div>
              <div class="form-group">
                <button
                  class="btn btn-primary text-uppercase small"
                  data-toggle="modal"
                  data-target="#alertModal"
                  type="button"
                >
                  Subscribe
                </button>
              </div>
            </form>
          </div>
          <div class="col-12 col-lg-2 ml-lg-auto col-md-3 ml-md-0 text-right">
            <h6 class="text-uppercase">Jobs</h6>
            <p>
              <em
                ><a href=""
                  >We&apos;re looking for great talent. Browse the job
                  openings.</a
                ></em
              >
            </p>
          </div>
          <div class="col-12 text-md-right text-center">
            <br />
            <ul class="list-inline">
              <li class="list-inline-item">
                <a
                  rel="nofollow"
                  href="//twitter.com/ThemesGuide"
                  title="Twitter"
                  ><i class="ion-social-twitter-outline"></i></a
                >&#xA0;
              </li>
              <li class="list-inline-item">
                <a rel="nofollow" href="" title=""
                  ><i class="ion-social-instagram-outline"></i></a
                >&#xA0;
              </li>
              <li class="list-inline-item">
                <a rel="nofollow" href="" title="Facebook"
                  ><i class="ion-social-facebook-outline"></i></a
                >&#xA0;
              </li>
              <li class="list-inline-item">
                <a rel="nofollow" href="" title="Dribbble"
                  ><i class="ion-social-dribbble-outline"></i
                ></a>
              </li>
            </ul>
          </div>
        </div>
        <br />
        <br />
        <hr class="light" />
        <div class="text-center text-normal">
          <a href="http://themes.guide"
            >Made by Themes.guide in Little Rhody <i class="ion-location"></i
          ></a>
        </div>
      </div>
    </footer>
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
