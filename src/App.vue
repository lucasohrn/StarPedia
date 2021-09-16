<template>
  <div class="page">
    <Header></Header>

    <div class="body">
      <div class="buttons">
        <button
          class="showButton"
          :disabled="enableDisablePeople"
          v-on:click="myFunction()"
        >
          Show People
        </button>
        <button
          class="showButton"
          :disabled="enableDisableFilms"
          v-on:click="myFunction()"
        >
          Show Films
        </button>
      </div>

      <Main></Main>

      <People v-if="isHidden"></People>
      <Films v-if="!isHidden"></Films>
    </div>

    <div class="footer">
      <Footer></Footer>
    </div>
  </div>
</template>

<script>
import Main from "./components/Main.vue";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import People from "./components/People.vue";
import Films from "./components/Films.vue";

export default {
  name: "App",
  components: {
    Main,
    Header,
    Footer,
    People,
    Films,
  },
  data: () => ({
    enableDisablePeople: true,
    enableDisableFilms: false,
    isHidden: true,
  }),
  methods: {
    myFunction: function () {
      if (!this.isHidden) {
        this.isHidden = !this.isHidden;
        this.enableDisablePeople = true;
        this.enableDisableFilms = false;
      } else {
        this.isHidden = !this.isHidden;
        this.enableDisablePeople = false;
        this.enableDisableFilms = true;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fafafa;
}
* {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
}
.page {
  background-image: url(./assets/background.png);
  background-size: cover;
  min-height: 849px;
}
.body {
  background-color: rgba(88, 100, 107, 0);
  margin-left: 50px;
  margin-right: 50px;
}
.footer {
  position: relative;
  background-color: #ffffff(0, 0, 0);
  margin-left: 50px;
  margin-right: 50px;
}
.showButton {
  cursor: pointer;
  margin: 0.3em;
  width: 8em;
}
.buttons {
}
</style>
