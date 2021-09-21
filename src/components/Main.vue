<template>
  <div>
    <h1>StarPedia</h1>
    <search-bar
      :search="search"
      @updateSearch="onUpdateSearch"
    ></search-bar>

    <div class="body">
      <div class="buttons">
        <button
          class="showButton"
          :disabled="enableDisablePeople"
          v-on:click="myFunction()"
        >
          Show People
        </button>
        <button
          class="showButton"
          :disabled="enableDisableFilms"
          v-on:click="myFunction()"
        >
          Show Films
        </button>
      </div>

      <People :searchQuery="search" v-show="isHidden"></People>
      <Films v-show="!isHidden"></Films>
    </div>
  </div>
</template>

<script>
import People from "./People.vue";
import Films from "./Films.vue";
import SearchBar from "./SearchBar.vue";
export default {
  components: {
    People,
    Films,
    SearchBar,
  },

  data:() => ({
      search:"",
      enableDisablePeople: true,
      enableDisableFilms: false,
      isHidden: true, 
  }),
  
  methods: {
    onUpdateSearch(queryString) {
      this.search = queryString;
      console.log("main.onUpdateSearch", queryString)
    },
    myFunction: function () {
      if (!this.isHidden) {
        this.isHidden = !this.isHidden;
        this.enableDisablePeople = true;
        this.enableDisableFilms = false;
      } else {
        this.isHidden = !this.isHidden;
        this.enableDisablePeople = false;
        this.enableDisableFilms = true;
      }
    },
  },

  props: {},
};
</script>
<style scoped>
</style>
