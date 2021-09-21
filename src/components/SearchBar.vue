<template>
    <div class="search">
      <input type="text" v-model="search" placeholder="Search.."/>
      <button>
        <img src="../assets/search.png" alt="search" class="searchButton" />
      </button>
    </div>
</template>

<script>
export default {
 data:() =>({
   search:''
 }),

  watch:{
    search(queryString)
    {
       this.$emit('updateSearch', queryString)
    }
  },
}
</script>

<style scoped>
.search {
  margin-top: 0px;
}
.searchButton {
  max-width: 2em;
  cursor: pointer;
}
.search input {
  margin-bottom: 20px;
  height: 2em;
}
* {
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
}
h1 {
  color: black;
  opacity: 0;
}
</style>