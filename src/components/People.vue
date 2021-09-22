<template>
  <div>
    <h1>People in StarWars</h1>

    <button @click="changePage">click me</button>

    <div class="container">
      <ul>
        <li v-for="person in people" v-bind:key="person.name">
          <div class="card">
            <p>{{ person.name }}</p>
            <br />
            <h4>BirthYear:</h4>
            {{ person.birth_year }} <br />
            <h4>Eyecolor:</h4>
            {{ person.eye_color }} <br />
            <li
              v-for="film in dataFromApi.results.films"
              v-bind:key="film.name"
            >
              <p>{{ film.name }}</p>
            </li>
            <!-- <button class="readMore">Read More</button> -->
          </div>
        </li>
      </ul>
    </div>
    <button class="previous">Previous</button>
    <button v-on:click="getNext">next</button>
  </div>
</template>

<script>
export default {
  data: () => ({
    errorMessage: "No results yet",
    dataFromApi: {},
    peopleFromApi: [],
    people: [],
    index: 0,
    url: `https://swapi.dev/api/people`,
  }),
  props: ["searchQuery"],

  watch: {
    searchQuery: function (newVal, oldVal) {
      console.log("people.getnext searchqury:", this.searchQuery);
      this.onSearchBarChange();
      console.log("people Watch Values: old:", oldVal, "new:", newVal);
    },
  },

  methods: {
    getNext() {},

    getPrevious() {
      if (this.dataFromApi.previous != null) {
        this.url = this.dataFromApi.previous;
      }
    },

    onSearchBarChange() {
      let query = this.searchQuery;
      this.people = this.filterItems(this.dataFromApi.results, query);
      return this.people;
    },

    async getAPIData() {
      if (!this.dataFromApi) {
        return "";
      } else {
        while (this.peopleFromApi.length < this.dataFromApi.count -1) {
          let safety = 0;
          if (safety > this.dataFromApi.count / 10 + 1) {
            console.log("People, getApiData something is proably broken");
            break;
          }

          for (
            let index = 0;
            index < this.dataFromApi.results.length;
            index++
          ) {
            const person = this.dataFromApi.results[index];
            this.peopleFromApi[this.peopleFromApi.length + 1] = person;
          }
          if (this.dataFromApi.next != null) {
            console.log("people getApiData", this.dataFromApi.next)
          }
          console.log("people getApiData", this.peopleFromApi.length)
          safety++;
        }
        console.log("loop done1", this.films);
        return this.films;
      }
    },

    filterItems(arr, query) {
      console.log("array:", arr);
      return arr.filter((person) => {
        return person.name.toLowerCase().indexOf(query.toLowerCase()) !== -1;
      });
    },
  },
  //methods

  async mounted() {
    console.log("mountedPeople");
    const url = this.url;
    let response;
    this.errorMessage = "";
    this.getAPIData()
    try {
      response = await fetch(url);
      const data = await response.json();
      this.dataFromApi = data;
      this.onSearchBarChange()
    } catch (error) {
      if (response) {
        this.errorMessage = "Data is in the wrong format. Try again later.";
      } else {
        this.errorMessage =
          "Could not send request. Check your internet connection.";
      }
    }
  },
};
</script>

<style scoped>
* {
  flex: 1;
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
}
.component {
  border: 1px solid gray;
  padding: 1em;
  margin: 1em;
  background: lightcoral;
}
p {
  color: rgb(255, 255, 255);
  font-size: 1.5em;
  margin-top: 0.2em;
}
.card {
  flex: 1;
  float: left;
  width: 250px;
  height: 150px;
  background-color: #3c3650;
  border-radius: 10px;
  box-shadow: -1rem 0 3rem #000;
  /*   margin-left: -50px; */
  transition: 0.4s ease-out;
  position: relative;
  left: 0px;
}
.card:not(:first-child) {
  margin-left: -50px;
}
.card:hover {
  transform: translateY(-20px);
  transition: 0.4s ease-out;
  background-color: rgb(103, 85, 148);
}
.card:hover ~ .card {
  position: relative;
  left: 50px;
  transition: 0.4s ease-out;
}
.container ul li {
  list-style: none;
}
.container {
  display: flex;
  margin-left: 100px;
  margin-right: 60px;
}

.readMore:hover {
  background: lightblue;
  cursor: pointer;
}
</style>