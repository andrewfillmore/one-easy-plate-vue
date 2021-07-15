<template>
  <div class="login">
    <section class="bg-alt">
      <div class="container">
        <h2 class="text-center pb-2"></h2>
        <div class="row wow slideInUp">
          <div class="col-lg-6 col-12 pb-3">
            <div class="card h-100">
              <div class="card-img-top"></div>
              <div class="card-body">
                <h1>Login</h1>
                <form v-on:submit.prevent="submit()" role="form">
                  <ul>
                    <li v-for="error in errors" v-bind:key="error">
                      {{ error }}
                    </li>
                  </ul>
                  <div class="form-group">
                    <label
                      for="inputEmailForm"
                      class="sr-only form-control-label"
                      >Email</label
                    >
                    <div class="mx-auto col-sm-10">
                      <input
                        type="text"
                        v-model="email"
                        class="form-control"
                        id="inputEmailForm"
                        placeholder="email"
                        required
                      />
                    </div>
                  </div>
                  <div class="form-group">
                    <label
                      for="inputPasswordForm"
                      class="sr-only form-control-label"
                      >Password</label
                    >
                    <div class="mx-auto col-sm-10">
                      <input
                        type="password"
                        v-model="password"
                        class="form-control"
                        id="inputPasswordForm"
                        placeholder="password"
                        required
                      />
                    </div>
                  </div>
                  <div class="form-group"></div>
                  <div class="form-group">
                    <div class="mx-auto col-sm-10 pb-3 pt-2">
                      <button
                        type="submit"
                        class="btn btn-outline-secondary btn-lg btn-block"
                      >
                        Sign-in
                      </button>
                    </div>
                  </div>
                </form>
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
import axios from "axios";

export default {
  data: function () {
    return {
      email: "",
      password: "",
      errors: [],
    };
  },
  methods: {
    submit: function () {
      var params = {
        email: this.email,
        password: this.password,
      };
      axios
        .post("/sessions", params)
        .then((response) => {
          axios.defaults.headers.common["Authorization"] =
            "Bearer " + response.data.jwt;
          localStorage.setItem("jwt", response.data.jwt);
          localStorage.setItem("user_id", response.data.user_id);
          this.$router.push("/about");
        })
        .catch((error) => {
          console.log(error.response);
          this.errors = ["Invalid email or password."];
          this.email = "";
          this.password = "";
        });
    },
  },
};
</script>
