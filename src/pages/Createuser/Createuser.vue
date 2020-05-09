<template>
  <div class="auth-page">
    <b-container>
      <h5 class="auth-logo">
        <i class="fa fa-circle text-primary"></i>
        Create User
        <i class="fa fa-circle text-danger"></i>
      </h5>
      <Widget
        class="widget-auth mx-auto"
        title="<h3 class='mt-0'>Create User</h3>"
        customHeader
      >
        <form class="mt" @submit.prevent="createuser">
          <b-alert class="alert-sm" variant="danger" :show="!!errorMessage">
            {{ errorMessage }}
          </b-alert>
          <div class="form-group">
            <input
              class="form-control no-border"
              ref="username"
              required
              type="taxt"
              name="username"
              placeholder="Username"
            />
          </div>
          <div class="form-group">
            <input
              class="form-control no-border"
              ref="password"
              required
              type="password"
              name="password"
              placeholder="Password"
            />
          </div>
          <div class="form-group">
            <input
              class="form-control no-border"
              ref="email"
              required
              type="email"
              name="email"
              placeholder="email"
            />
          </div>
          <div class="form-group">
            <label
              >Male:
              <input
                type="radio"
                name="male"
                value="male"
                v-model="checkedGroupVModel"
              /> </label
            ><br />
            <label
              >Female:
              <input
                type="radio"
                name="female"
                value="female"
                v-model="checkedGroupVModel"
              /> </label
            ><br />
            <br />
          </div>
          <b-button
            type="submit"
            size="sm"
            class="auth-btn mb-3"
            variant="inverse"
            >submit</b-button
          >
        </form>
      </Widget>
    </b-container>
    <footer class="auth-footer">
      presented by inwzaclub
    </footer>
  </div>
</template>

<script>
/* eslint-disable */
import Widget from "@/components/Widget/Widget";
import axios from "axios";

export default {
  name: "LoginPage",
  components: { Widget },
  data() {
    return {
      errorMessage: null,
      checkedGroupVModel: "male",
    };
  },
  methods: {
    createuser() {
      const AxiosAPI = axios.create({
        baseURL: "https://api.inwza.club",
        timeout: 1000,
        headers: { "Content-Type": "application/json" },
      });

      const username = this.$refs.username.value;
      const password = this.$refs.password.value;
      const email = this.$refs.email.value;

      let payload = {
        username: username,
        password: password,
        email: email,
        gender: this.checkedGroupVModel,
      };
      console.log(payload);

      AxiosAPI.post("/users", payload)
        .then((res) => {
          // if status ok can go!
          if (res.status == 201) {
            window.localStorage.setItem("authenticated", true);
            this.$router.push("/app/dashboard");
          }
        })
        .catch((e) => {
          console.log("cannot login with, " + e);
          this.$toasted.success("connot login with username or password", {
            action: {
              text: "Close",
              onClick: (e, toastObject) => {
                toastObject.goAway(0);
              },
            },
          });
        });
    },
  },
};
</script>
