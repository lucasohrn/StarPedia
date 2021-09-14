<template>
  <div class="page">
    <Header></Header>

    <div class="body">
      <Main></Main>
      <button class="showPeople" v-on:click="isHidden = true">Show Peoples</button>
      <button class="showFilms" v-show="enabled" v-on:click="isHidden = false">Show Films</button>
      
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
    Films
  },
  data: () => ({
    isHidden: false,
    enabled: true
  }),
  methods: {
        hideText() {
            this.enabled = !this.enabled
        }
    }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #7b7e81;
}
*{
    margin: 0;
    padding: 0;
    font-family: sans-serif;
}
.page {
  background-image: url(./assets/background.png);
  background-size: cover;
}
.body {
  background-color: rgb(255, 255, 255);
  margin-left: 50px;
  margin-right: 50px;
}
.footer {
  position:relative;
  background-color: #2c3e50(0, 0, 0);
  margin-left: 50px;
  margin-right: 50px;
}
.showPeople {
  cursor: pointer;
}
.showFilms {
  cursor: pointer;
}
</style>
