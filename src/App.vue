<template>
  <div id="app">
    <HeaderLogIn v-if="token" :user="user"/>
    <HeaderLogOut v-else/>

    <router-view></router-view>
    <Footer/>
  </div>
</template>

<script>
import HeaderLogIn from "./components/HeaderLogIn";
import HeaderLogOut from "./components/HeaderLogOut";
import Footer from "./components/Footer";
export default {
  name: "App",
  components: {
    HeaderLogIn,
    HeaderLogOut,
    Footer
  },
  data() {
    return {
      token: "",
      user: {}
    };
  },
  created() {
    this.$on("auth", this.updateUserData);
    this.updateUserData();
  },
  methods: {
    updateUserData: function() {
      console.log("here");
      this.token = localStorage.getItem("NOTES_AUTH");

      if (this.token) {
        this.user = {
          username: localStorage.getItem("USER_NAME"),
          fullName: localStorage.getItem("FULL_NAME"),
          id: localStorage.getItem("USER_ID")
        };
      }
    }
  }
};
</script>

<style>

#app {
  font-family: "Roboto", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  min-height: 100vh;
}
</style>
