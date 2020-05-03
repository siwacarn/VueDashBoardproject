<template>
  <div class="auth-page">
    <b-container>
      <h5 class="auth-logo">
        <i class="fa fa-circle text-primary"></i>
        dashboard
        <i class="fa fa-circle text-danger"></i>
      </h5>
      <Widget
        class="widget-auth mx-auto"
        title="<h3 class='mt-0'>Login to your Web App</h3>"
        customHeader
      >
        <p class="widget-auth-info">
          Use your username to sign in.
        </p>
        <form class="mt" @submit.prevent="login">
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
          <b-button
            type="submit"
            size="sm"
            class="auth-btn mb-3"
            variant="inverse"
            >Login</b-button
          >
        </form>
        <p class="widget-auth-info">
          Don't have an account? Sign up now!
        </p>
        <router-link class="d-block text-center" to="login"
          >Create an Account</router-link
        >
      </Widget>
    </b-container>
    <footer class="auth-footer">
      presented by gu
    </footer>
  </div>
</template>

<script>
import Widget from "@/components/Widget/Widget";
import axios from "axios";

export default {
  name: "LoginPage",
  components: { Widget },
  data() {
    return {
      errorMessage: null,
    };
  },
  methods: {
    login() {
      const AxiosAPI = axios.create({
        baseURL: "https://api.inwza.club",
        timeout: 1000,
        headers: { "Content-Type": "application/json" },
      });

      const username = this.$refs.username.value;
      const password = this.$refs.password.value;

      if (username.length !== 0 && password.length !== 0) {
        window.localStorage.setItem("authenticated", true);
        this.$router.push("/app/dashboard");
      }
      let test = {
        "username": username,
        "password": password,
      };

      // eslint-disable-next-line no-console
      console.log(username);
      // eslint-disable-next-line no-console
      console.log(password);

      AxiosAPI.post("/login", test)
        .then((res) => {
          // eslint-disable-next-line no-console
          console.log(res);
        })
        .catch((e) => {
          // eslint-disable-next-line no-console
          console.log(e);
        });
    },
  },
  // created() {
  //   if (window.localStorage.getItem('authenticated') === 'true') {
  //     this.$router.push('/app/main/analytics');
  //   }
  // },
};
</script>
