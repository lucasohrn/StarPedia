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
    <p>showing results {{this.count}}</p>
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
    urls: [],
    nextUrl: "",
    previousUrl: "",
    count: 0
  }),
  props: ["searchQuery"],

  watch: {
    searchQuery: function () {
      this.onSearchBarChange();
    },
  },

  methods: {
    async returnFilms(movieUrl) {
      let moviesForPerson = [null];
      for (let i = 0; i < movieUrl.length; i++) {
        moviesForPerson[i] = await this.getMoviesByCharacter(await movieUrl[i]);
        this.test[i] = await moviesForPerson[i]
      }
      return this.test
    },
    async getMoviesByCharacter(url) {
      let response;
      this.errorMessage = "";
      try {
        response = await fetch(url);
        const data = await response.json();

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
      const url = this.url;
      let response;
      this.errorMessage = "";
      try {
        response = await fetch(url);
        const data = await response.json();
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

      if (this.searchQuery == "") {
        this.people = this.filterItems(this.dataFromApi.results, query)
        this.count = this.people.length
      }
      else{  
        this.people = this.filterItems(this.peopleFromApi, query);
        this.count = this.people.length
      }
      return this.people;
    },

    async getAPIData() {
    let peopleResponse;
    let count = 1
      while (count != this.dataFromApi.count - 1) {
        if (count == 17)
        {
          count += 1; // seventeen doesn't work
        }

        peopleResponse = await fetch(
          `https://swapi.dev/api/people/` + count + `/`
        );
        this.urls[count] = `https://swapi.dev/api/people/` + count + `/`;
        const peopleData = await peopleResponse.json();
        this.peopleFromApi[count] = peopleData;
        count += 1;
      }
    },

    filterItems(arr, query) {
      return arr.filter((person) => {
        return person.name.toLowerCase().indexOf(query.toLowerCase()) !== -1;
      });
    },
  },
  //methods

  async mounted() {
    await this.drawMap();
    await this.getAPIData();
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