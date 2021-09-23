<template>
  <div>
    <h1>People in StarWars</h1>
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
          </div>
        </li>
      </ul>
    </div>
    <button class="showButton" v-on:click="getPrevious">
      <img src="../assets/arrow_left.png" alt="left_arrow" />
    </button>
    <button class="showButton" v-on:click="getNext">
      <img src="../assets/arrow_right.png" alt="right_arrow" />
    </button>
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
    nextUrl: "",
    previousUrl: "",
    test: []
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
    async returnFilms(movieUrl) {
      let moviesForPerson = [null];
      console.log("längd", movieUrl.length);
      for (let i = 0; i < movieUrl.length; i++) {
        moviesForPerson[i] = await this.getMoviesByCharacter(await movieUrl[i]);
        console.log("movies", moviesForPerson[i])
        this.test[i] = await moviesForPerson[i]
      }
      console.log("TEST", this.test)
      return this.test
    },
    async getMoviesByCharacter(url) {
      let response;
      this.errorMessage = "";
      try {
        response = await fetch(url);
        const data = await response.json();

        console.log("data.name", data.title)
        return await data.title;

      } catch (error) {
        if (response) {
          this.errorMessage = "Data is in the wrong format. Try again later.";
        } else {
          this.errorMessage =
            "Could not send request. Check your internet connection.";
        }
      }
    },
    async drawMap() {
      console.log("mountedPeople");
      const url = this.url;
      let response;
      this.errorMessage = "";
      try {
        response = await fetch(url);
        const data = await response.json();
        console.log("People.MountPeople, data from API: ", data);

        this.dataFromApi = data;
        this.onSearchBarChange();
      } catch (error) {
        if (response) {
          this.errorMessage = "Data is in the wrong format. Try again later.";
        } else {
          this.errorMessage =
            "Could not send request. Check your internet connection.";
        }
      }
    },
    async getNext() {
      this.url = this.dataFromApi.next;
      this.drawMap();
    },

    async getPrevious() {
      this.url = this.dataFromApi.previous;
      this.drawMap();
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
    await this.drawMap();
  },
};
</script>

<style scoped>
* {
  flex: 1;
  font-family: Georgia, "Times New Roman", Times, serif;
}
.component {
  border: 1px solid gray;
  padding: 1em;
  margin: 1em;
  background: lightcoral;
}
p {
  color: rgb(241, 233, 111);
  font-size: 1.5em;
  margin-top: 1em;
  margin-left: 0.1em;
  margin-right: 0.1em;
}
h1 {
  margin: 1em;
}
.card {
  margin-left: 1.5em;
  background-color: rgb(236, 232, 240);
  width: 25vh;
  float: left;
  margin: 1em;
  width: 250px;
  height: 11rem;
  background-color: #202016;
  border-radius: 10px;
  box-shadow: -1rem 0 3rem rgba(189, 197, 69, 0.658);
  /*   margin-left: -50px; */
  transition: 0.5s ease-out;
}
.card:not(:first-child) {
  margin-left: -50px;
}
.card:hover {
  transform: translateY(-20px);
  transition: 0.4s ease-out;
  background-color: rgb(0, 0, 0);
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
.readMore {
  margin-top: 0.6em;
}
.readMore:hover {
  background: lightblue;
  cursor: pointer;
}
.showButton {
  margin-top: 3em;
  margin-left: 2em;
  margin-right: 2em;
}
.showButton img {
  max-width: 50px;
}
button {
  border: black;
}
.showButton:hover {
  box-shadow: -1rem 0 3rem rgba(219, 221, 195, 0.678);
}
.showButton:enabled {
  background-color: rgb(183, 212, 52);
  color: rgb(0, 0, 0);
}
.showButton:active {
  background-color: rgb(238, 255, 0);
}
</style>