<template>
  <div>
    <h1>People in StarWars</h1>

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
  }),
  methods: {
    async getNext(){

    },
    async getPrevious(){

    },

    async getApiData() {
      if (!this.dataFromApi) {
        return "";
      } else {
        for (let index = 0; index < this.dataFromApi.results.length; index++) {
          const element = this.dataFromApi.results[index];
          this.people[index] = element;
          console.log("loop ", this.people[index]);
        }
        console.log("loop done", this.people);
        return this.people;
      }
    },
  },
  async mounted() {
    console.log("mounted");
    const url = `https://swapi.dev/api/people`;
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
  margin: 2em;
  background-color: rgb(236, 232, 240);
  width: 250px;
}
.container ul li{
    list-style: none;
}
.container {
    padding-bottom: 50px;
}
</style>