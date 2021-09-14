<template>
  <div>
    <h1>StarWars films</h1>
    <div class="container">
      <ul>
        <li v-for="results in dataFromApi.results" v-bind:key="results.name">
          <div class="card">
            <p>{{ results.title}}</p>
            <br />
            <h4>
              Director:<span class="normal-text">{{
                " " + results.director
              }}</span>
            </h4>
            <h4>
              Episode:
              <span class="normal-text">{{ " " + results.episode_id }}</span>
            </h4>
            <h4>
              Realease date:
              <span class="normal-text">{{ " " + results.release_date }}</span>
            </h4>
            <h4>
              Producer(s):
              <span class="normal-text">{{ "" + results.producer }}</span>
            </h4>
            <h4>Charachters</h4>
            {{results.films.Charachters}}
            <div class="expand">
              <h4>Opening crawl:</h4>
              <div class="opening-crawl">
                <h5>{{ results.opening_crawl }}</h5>
                <br />
              </div>
            </div>
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
    films: [],
  }),
  methods: {
    async getAPIData() {
      if (!this.dataFromApi) {
        return "";
      } else {
        for (let index = 0; index < this.dataFromApi.results.length; index++) {
          const element = this.dataFromApi.results[index];
          this.films[index] = element;
          console.log("loop ", this.films[index]);
        }
        console.log("loop done", this.films);
        return this.films;
      }
    },
  },
  async mounted() {
    console.log("mounted");
    const url = `https://swapi.dev/api/films`;
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
  margin-top: 1em;
  margin-left: 1em;
  margin-right: 1em;
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
.opening-crawl {
  font-size: 0.7em;
  display: none;
}
.expand:hover .opening-crawl {
  display: block;
}
.normal-text {
  font-weight: normal;
  font-size: 1em;
}
h4 {
  text-align: left;
  margin-left: 1em;
}
h5 {
  text-align: left;
  margin-top: 1em;
  margin-left: 1em;
  margin-right: 1em;
}
</style>