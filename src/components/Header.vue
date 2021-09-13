<template>
  <div class="navbar">
    <img class="logo" alt="Vue logo" src="../assets/logo.png" />
    <ul>
      <li><a href="">FILMS</a></li>
      <li><a href="">PEOPLE</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
*{
    margin: 0;
    padding: 0;
    font-family: Arial, Helvetica, sans-serif;
    margin-top: 3em;
}
.navbar{
    width: 88%;
    margin: auto;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-bottom: 4em;
}
.logo{
    margin-top: 2em;
    max-width: 140px;
    cursor: pointer;
}
.navbar ul li{
    list-style: none;
    display: inline-block;
    margin: 0 15px;
}
.navbar ul li a{
    text-decoration: none;
    color: #fdf5c9;
    font-size: 30px;
}
</style>
