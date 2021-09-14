<template>
  <div class="hello">
    <h1>StarPedia</h1>

    <div class="search">
      <input type="text" />
      <button>
        <img src="../assets/search.png" alt="search" class="searchButton" />
      </button>
    </div>


    </div>
</template>

<script>
export default {
  name: "Main",
  props: {
    msg: String,
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
}
h1 {
  color: black;
  opacity: 0;
}
.search {
  margin-top: 2em;
}
.searchButton {
  max-width: 2em;
  cursor: pointer;
}
.search input {
  height: 2em;
}
</style>
