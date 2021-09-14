<template>
  <div class="page">
    <Header></Header>

    <div class="body">
      <Main></Main>
      <People></People>
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
import People from "./components/People.vue"

export default {
  name: "App",
  components: {
    Main,
    Header,
    Footer,
    People
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
*{
    margin: 0;
    padding: 0;
    font-family: sans-serif;
}
.page {
  height: 100vh;
  width: 100%;
  background-image: url(./assets/background.png);
  background-size: cover;
  background-position: center;
  position: relative;
}
.body {
  background-color: rgb(255, 255, 255);
  margin-left: 50px;
  margin-right: 50px;
  height: 590px;
}
.footer {
  background-color: rgb(255, 255, 255);
  margin-left: 50px;
  margin-right: 50px;
}
</style>
