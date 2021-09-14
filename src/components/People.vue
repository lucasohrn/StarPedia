<template>
  <div>
    <h1>People in StarWars</h1>

    <button @click="changePage">click me</button>

    <div class="container">
      <ul>
        <li v-for="results in dataFromApi.results" v-bind:key="results.name">
          <div class="card">
            <p>{{ results.name }}</p>
            <br />
            <h4>BirthYear:</h4>
            {{ results.birth_year }} <br />
            <h4>Eyecolor:</h4>
            {{ results.eye_color }} <br />
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    errorMessage: "No results yet",
    dataFromApi: {},
    people: [],
    index: 0,
    url: `https://swapi.dev/api/people`,
  }),
  methods: {
    async sunrise() {
      if (!this.dataFromApi) {
        return "";
      } else {
        for (
          this.index = 0;
          this.index < this.dataFromApi.results.length;
          this.index++
        ) {
          const element = this.dataFromApi.results[this.index];
          this.people[this.index] = element;
          console.log("loop ", this.people[this.index]);
        }
        console.log("loop done", this.people);
        return this.people;
      }
    },
    changePage() {
      this.url = `https://swapi.dev/api/people/?page=2`;
    },
  },
  async mounted() {
    console.log("mounted");
    const url = this.url;
    let response;
    this.errorMessage = "";
    try {
      response = await fetch(url);
      const data = await response.json();
      console.log("Data from API: ", data);
      this.dataFromApi = data;
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
  font-family: Georgia, "Times New Roman", Times, serif;
}
.component {
  border: 1px solid gray;
  padding: 1em;
  margin: 1em;
  background: lightcoral;
}
p {
  color: rgb(30, 28, 31);
  font-size: 1.5em;
}
.card {
  margin-left: 1.5em;
  background-color: rgb(236, 232, 240);
  width: 25vh;
  flex: 1;
  float: left;
  margin: 1em;
}
.container ul li {
  list-style: none;
}
.container {
  display: flex;
  margin-left: 100px;
  margin-right: 20px;
}
</style>