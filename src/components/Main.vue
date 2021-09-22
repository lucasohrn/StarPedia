<template>
  <div>
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
          <h3>Show People</h3> 
        </button>
        <button
          class="showButton"
          :disabled="enableDisableFilms"
          v-on:click="myFunction()"
        >
          <h3>Show Films</h3>
        </button>
      </div>
      
      <transition name="fade">
        <div v-if="show"><People :searchQuery="search" v-show="isHidden"></People></div>
        
      </transition>
      <transition name="fade">
        <div v-if="!show">
          <Films v-show="!isHidden"></Films>
        </div>
      </transition>
      
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
      show: true
  }),
  
  methods: {
    onUpdateSearch(queryString) {
      this.search = queryString;
      console.log("main.onUpdateSearch", queryString)
    },
    myFunction: function () {

      if (!this.isHidden) {
        this.show = true;
        this.isHidden = !this.isHidden;
        this.enableDisablePeople = true;
        this.enableDisableFilms = false;
      } else {
        this.show = false;
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
*{
  font-family: Georgia, 'Times New Roman', Times, serif;
}
button{
  border: black;
}
button h3{
  font-size: 1em;
  margin-top: 5px;
  margin-bottom: 5px;
}
.showButton:hover:active{
  box-shadow: -1rem 0 3rem rgba(219, 221, 195, 0.678);
}
.showButton:enabled{
  background-color: rgb(183, 212, 52);
  color: rgb(0, 0, 0);
}
.showButton:active{
  background-color: rgb(238, 255, 0);
}
.fade-enter-from {
  opacity: 0;
}
.fade-enter-to {
  opacity: 1;
}
.fade-enter-active {
  transition-delay: 1s;
  transition: all 2s ease;
}
.fade-leave-from{
  opacity: 1;
}
.fade-leave-to{
  opacity: 0;
}
.fade-leave-active{
  transition: all 0.1s ease;
}
</style>
