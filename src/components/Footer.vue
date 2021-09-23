<template>
  <div class="footer">
    <h3>About Us</h3>
    <ul class="content">
      <div>
        Detta är ett projekt skapat i syfte av att hitta information om karaktärer och filmer från StarWars <br><br>
        Skapat av: <br>
        <li><a>Lucas Öhrn & Sixten Larsson</a></li>
      </div>
      <div>
        <li><a><br>Utbildning: .Net4</a></li>
        <li><a> Kurs: WebbUtveckling</a></li>
      </div>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Footer",
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
}
h3 {
  margin: 80px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #e2e3e5;
}
.content {
  padding-top: 1em;
  padding-bottom: 2em;
}
</style>
