<template>
  <div class="navbar">
    <img class="logo" alt="Vue logo" src="../assets/logo.png" />
    <ul>
      <li><a href="">HOME</a></li>
      <li><a href="">ABOUT</a></li>
      <li><a href="">SPECIFICATIONS</a></li>
      <li><a href="">PRODUCTS</a></li>
      <li><a href="">CONNECT</a></li>
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
    font-family: sans-serif;
}
.navbar{
    width: 88%;
    margin: auto;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.logo{
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
    color: #5f5f5f;
    font-size: 15px;
}
</style>
