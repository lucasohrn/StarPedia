<template>
  <div class="hello">
    <h1>StarPedia</h1>
    <search-bar></search-bar>
  </div>
</template>

<script>
import SearchBar from './SearchBar.vue';
export default {
  components: { 
    SearchBar 
    },
  
  props: {
    msg: String,
  }
};
</script>
<style scoped>

</style>
