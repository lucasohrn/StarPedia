<template>
  <div>
    <h1>StarWars films</h1>
    <div class="container">
      <ul>
        <li v-for="results in dataFromApi.results" v-bind:key="results.name">
          <div class="card">
            <p>{{ results.title }}</p>
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

            <div class="expand">
              <h4>Producer(s):</h4>
              <div class="info">
                <h5>{{ "" + results.producer }} <br /></h5>
                <br />
              </div>
            </div>
            <h4>
              <span class="normal-text"></span>
            </h4>

            <div class="expand">
              <h4>Charachters:</h4>
              <div class="info">
                <h5>{{ getCharacters(results) }} <br /></h5>
                <br />
              </div>
            </div>

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
    movies: {},
    characters: {} 
  }),
  methods: {
    async getAPIData() {
      if (!this.dataFromApi) {
        return "";
      } else {
        for (let index = 0; index < this.dataFromApi.results.length; index++) {
          const element = this.dataFromApi.results[index];
          this.films[index] = element;
          console.log("loop1 ", this.films[index]);
        }
        console.log("loop done1", this.films);
        return this.films;
      }
    },
    async getCharacters(results) {
      this.characters = 0
      console.log("urler: ", results.characters);

      for (let i = 0; i < results.characters.length; i++) {
        const url = results.characters[i];
        console.log("Karaktär3: ", url)
        const response = await fetch(url);
        const characterData = await response.json();
        console.log("Karaktär1: ", characterData)
        this.characters[i] = characterData.name;
        console.log("Karaktär: ", characterData.name)
      }

      console.log("finished", this.characters)

      return await this.characters.toString();
    },

    async getCharactersNow() {
      if (!this.dataFromApi) {
        return "ERROR";
      } 
      else 
      {
        for ( let i = 0; i < this.dataFromApi.results.length; i++) 
        {
        //   //console.log("Count", this.dataFromApi.results.length);
        //   //console.log("CountMovies", this.dataFromApi.results[i].characters);
        //   // console.log("CountCharacters", this.dataFromApi.results[i].characters.length);
        //   this.movies[i] = this.dataFromApi.results[i].title;

          for (let j = 0; j < this.dataFromApi.results[i].characters.length; j++) {
            // console.log("KaraktärURL", this.dataFromApi.results[i].characters[j]);
            const url = this.dataFromApi.results[i].characters[j];
            const response = await fetch(url);
            const characterData = await response.json();
            // console.log("Data about characters: ", characterData);
            this.characters[j] = characterData.name;
          }

          // for (let j = 0; j < this.movies[i].characters.length; j++) {
          //   const characters = this.movies[i].characters[j];
          //   console.log("url:", this.characters[j]);
          //   const urlResponse = characters;

          //   const response = await fetch(urlResponse);
          //   const characterData = await response.json();
          //   console.log("Data about characters: ", characterData);
          //   this.movies.characters[j] = characterData;
          // }
        }
        
        // return this.characters;
      }
        console.log("Url", this.dataFromApi.results[1].characters[1]);
        console.log("film", this.characters);
        console.log("loop finished");
      // // Get all characters
      // for (let i = 0; i < data.results.characters.length; i++) {
      //   const urlResponse = data.results.characters[i];
      //   response = await fetch(urlResponse);
      //   const characterData = await characterData.json();
      //   console.log("Data about characters: ", characterData)
      //   this.characters = characterData
      // }
    },
  },
  async mounted() {
    console.log("mountedFilms");
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
.card {
  margin-left: 1.5em;
  background-color: rgb(236, 232, 240);
  width: 25vh;
  float: left;
  margin: 1em;
  width: 250px;
  height: 14rem;
  background-color: #3c3650;
  border-radius: 10px;
  box-shadow: -1rem 0 3rem #000;
  /*   margin-left: -50px; */
  transition: 0.5s ease-out;
}
.card:hover {
  transform: translateY(-20px);
  background-color: rgb(103, 85, 148);
}
/* .card:hover ~ .card {
  position: relative;
  left: 50px;
  transition: 0.4s ease-out;
} */
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
.container ul li {
  list-style: none;
}
.container {
  display: flex;
  margin-left: 100px;
  margin-right: 60px;
}
.card .opening-crawl {
  font-size: 0.7em;
  display: none;
  position: relative;
  z-index: 101;
}
.card .info {
  font-size: 0.7em;
  display: none;
  position: relative;
}
.expand:hover .info {
  transition: 0.5s all;
  display: block;
  background: rgb(103, 85, 148);
  color: rgb(255, 255, 255);
  position: absolute;
  opacity: 1;
  margin-left: 140px;
}
.expand:hover .opening-crawl {
  transition: 0.5s all;
  display: block;
  background: rgb(103, 85, 148);
  color: rgb(255, 255, 255);
  position: absolute;
  opacity: 1;
}
.expand {
  cursor: pointer;
}
</style>