<template>
  <div class="page">
    <Header></Header>
    <Main></Main>

    <div class="footer">
      <Footer></Footer>
    </div>
    
  </div>
</template>

<script>
import Main from "./components/Main.vue";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  components: {
    Main,
    Header,
    Footer,
  },
  data: () => ({
 
  }),
  methods: {
    
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
