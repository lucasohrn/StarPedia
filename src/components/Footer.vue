<template>
  <div class="footer">
    <h3>About Us</h3>
    <ul class="content">
      <div>
        <li><a>Lucas Öhrn</a></li>
        <li><a>Sixten Larsson</a></li>
      </div>
      <div>
        <li><a>.Net4</a></li>
        <li><a>WebbUtveckling</a></li>
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
  margin: 40px 0 0;
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
  padding-top: 2em;
  padding-bottom: 2em;
}
</style>
