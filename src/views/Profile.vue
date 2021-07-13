<template>
  <div class="users-show">
    <div class="container outer my-2">
      <div class="row">
        <div class="col-lg-12">
          <h2 class="my-1">User Profile</h2>
          <hr />
        </div>
        <div class="col-lg-9 order-lg-2">
          <ul class="nav nav-tabs small text-uppercase">
            <li
              class="nav-item"
              data-target="#editImage"
              data-toggle="collapse"
            >
              <a href="" data-target="#edit" data-toggle="tab" class="nav-link"
                >Edit</a
              >
            </li>
          </ul>
          <div class="tab-content py-3">
            <div class="tab-pane py-2 active" id="profile">
              <div class="row my-2">
                <div class="col-md-6"></div>
              </div>
              <!--/row-->
            </div>
            <div class="tab-pane py-2" id="messages">
              <div class="alert alert-info alert-dismissable">
                <a class="panel-close close" data-dismiss="alert">&#xD7;</a>
                This is an <span class="font-weight-bold">.alert</span>. Use
                this to show important messages to the user.
              </div>
              <table class="table table-hover table-striped">
                <tbody>
                  <tr>
                    <td>
                      <span class="float-right font-weight-bold"
                        >3 hrs ago</span
                      >
                      Here is your a link to the latest summary report from
                      the..
                    </td>
                  </tr>
                  <tr>
                    <td>
                      <span class="float-right font-weight-bold"
                        >Yesterday</span
                      >
                      There has been a request on your account since that was..
                    </td>
                  </tr>
                  <tr>
                    <td>
                      <span class="float-right font-weight-bold">9/10</span>
                      Porttitor vitae ultrices quis, dapibus id dolor. Morbi
                      venenatis lacinia rhoncus.
                    </td>
                  </tr>
                  <tr>
                    <td>
                      <span class="float-right font-weight-bold">9/4</span>
                      Vestibulum tincidunt ullamcorper eros eget luctus.
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
            <div class="tab-pane py-2" id="edit">
              <form v-on:submit.prevent="updateUser()" role="form">
                <div class="form-group row">
                  <label class="col-lg-3 col-form-label form-control-label"
                    >First name</label
                  >
                  <div class="col-lg-9">
                    <input
                      class="form-control"
                      type="text"
                      v-model="editUserParams.first_name"
                      value="John"
                    />
                  </div>
                </div>
                <div class="form-group row">
                  <label class="col-lg-3 col-form-label form-control-label"
                    >Last name</label
                  >
                  <div class="col-lg-9">
                    <input
                      class="form-control"
                      type="text"
                      v-model="editUserParams.last_name"
                      value="Bishop"
                    />
                  </div>
                </div>
                <div class="form-group row">
                  <label class="col-lg-3 col-form-label form-control-label"
                    >Email</label
                  >
                  <div class="col-lg-9">
                    <input
                      class="form-control"
                      type="email"
                      v-model="editUserParams.email"
                      value="email@gmail.com"
                    />
                  </div>
                </div>

                <div class="form-group row">
                  <label class="col-lg-3 col-form-label form-control-label"
                    >Password</label
                  >
                  <div class="col-lg-9">
                    <input
                      class="form-control"
                      type="password"
                      v-model="editUserParams.password"
                      value="11111122333"
                    />
                  </div>
                </div>
                <div class="form-group row">
                  <label class="col-lg-3 col-form-label form-control-label"
                    >Confirm password</label
                  >
                  <div class="col-lg-9">
                    <input
                      class="form-control"
                      type="password"
                      v-model="editUserParams.password_confirmation"
                      value="11111122333"
                    />
                  </div>
                </div>
                <div class="form-group row">
                  <label
                    class="col-lg-3 col-form-label form-control-label"
                  ></label>
                  <div class="col-lg-9">
                    <span v-if="$parent.getUserId() == user.id">
                      <input
                        v-on:click="destroyUser()"
                        type="reset"
                        class="btn btn-secondary"
                        value="Delete Account"
                      />
                    </span>
                    <input
                      type="submit"
                      class="btn btn-primary"
                      value="Save Changes"
                    />
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
        <div class="col-lg-3 order-lg-1 text-center">
          <table class="table table-sm small text-left">
            <tbody>
              <tr>
                <td class="text-uppercase">
                  {{ user.first_name }} {{ user.last_name }}
                </td>
                <td></td>
              </tr>

              <tr>
                <td class="text-uppercase">{{ user.email }}</td>
                <td></td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- <form v-on:submit.prevent="updateUser()">
      <label>
        First Name:
        <input type="text" v-model="editUserParams.first_name" />
      </label>
      <br />
      <label>
        Last Name:
        <input type="text" v-model="editUserParams.last_name" />
      </label>
      <br />
      <label>
        Email Address:
        <input type="text" v-model="editUserParams.email" />
      </label>
      <br />
      <label>
        Password:
        <input type="text" v-model="editUserParams.password" />
      </label>
      <br />
      <label>
        Password_confirmation:
        <input type="text" v-model="editUserParams.password_confirmation" />
      </label>
      <br />
      <input type="submit" value="Save Changes" />
      <span v-if="$parent.getUserId() == user.id">
        <button v-on:click="destroyUser()">Delete Account</button>
      </span>
    </form> -->
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      user: {},
      errors: [],
      editUserParams: {},
    };
  },
  created: function () {
    axios.get(`/users/${this.$parent.getUserId()}`).then((response) => {
      console.log("User Object", response.data);
      this.user = response.data;
    });
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
          this.$router.push("/home");
        });
      }
    },
  },
};
</script>
