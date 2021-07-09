<template>
  <div class="signup">
    <section class="bg-alt">
      <div class="container">
        <h2 class="text-center pb-2"></h2>
        <div class="row wow slideInUp">
          <div class="col-lg-6 col-12 pb-3">
            <div class="card h-100">
              <div class="card-img-top"></div>
              <div class="card-body">
                <h1>Sign-up</h1>

                <form v-on:submit.prevent="submit()" role="form">
                  <ul>
                    <li
                      class="text-danger"
                      v-for="error in errors"
                      v-bind:key="error"
                    >
                      {{ error }}
                    </li>
                  </ul>
                  <div class="form-group">
                    <label
                      for="input2EmailForm"
                      class="sr-only form-control-label"
                      >first name</label
                    >
                    <div class="mx-auto col-sm-10">
                      <input
                        type="text"
                        v-model="newUserParams.first_name"
                        class="form-control"
                        id="input2EmailForm"
                        placeholder="first name"
                        required
                      />
                    </div>
                  </div>
                  <div class="form-group">
                    <label
                      for="input2EmailForm"
                      class="sr-only form-control-label"
                      >last name</label
                    >
                    <div class="mx-auto col-sm-10">
                      <input
                        type="text"
                        v-model="newUserParams.last_name"
                        class="form-control"
                        id="input2EmailForm"
                        placeholder="last name"
                        required
                      />
                    </div>
                  </div>
                  <div class="form-group">
                    <label
                      for="input2EmailForm"
                      class="sr-only form-control-label"
                      >email</label
                    >
                    <div class="mx-auto col-sm-10">
                      <input
                        type="text"
                        v-model="newUserParams.email"
                        class="form-control"
                        id="input2EmailForm"
                        placeholder="email"
                        required
                      />
                    </div>
                  </div>
                  <div class="form-group">
                    <label
                      for="input2PasswordForm"
                      class="sr-only form-control-label"
                      >password</label
                    >
                    <div class="mx-auto col-sm-10">
                      <input
                        type="text"
                        v-model="newUserParams.password"
                        class="form-control"
                        id="input2PasswordForm"
                        placeholder="password"
                        required
                      />
                    </div>
                  </div>
                  <div class="form-group">
                    <label
                      for="input2Password2Form"
                      class="sr-only form-control-label"
                      >verify</label
                    >
                    <div class="mx-auto col-sm-10">
                      <input
                        type="text"
                        v-model="newUserParams.password_confirmation"
                        class="form-control"
                        id="input2Password2Form"
                        placeholder="verify password"
                        required
                      />
                    </div>
                  </div>
                  <div class="form-group">
                    <div class="mx-auto col-sm-10 pb-3 pt-2">
                      <button
                        type="submit"
                        class="btn btn-outline-secondary btn-lg btn-block"
                      >
                        Register
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
      newUserParams: {
        first_name: "",
        last_name: "",
        email: "",
        password: "",
        password_confirmation: "",
      },
      errors: [],
    };
  },
  methods: {
    submit: function () {
      axios
        .post("/users", this.newUserParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/login");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
