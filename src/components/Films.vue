<template>
  <div>
    <h1>StarWars films</h1>
    <div class="container">
      <ul>
        <li v-for="results in movies.results" v-bind:key="results.name">
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
                <h5>{{ "" + returnCharacter(results.characters) + "\n" }} <br /></h5>
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
    movies: {},
    characters: {},
    urls: {},
    peopleInMovie: {}
  }),
  functions: {

  },
  computed: {

  },
  methods: {
    returnCharacter(movieUrl) {
      let peopleInMovie = [null];
      for (let i = 0; i < movieUrl.length; i++) {
        for (let j = 1; j < 82; j++) {
          if (movieUrl[i] == this.urls[j]) {
            peopleInMovie[i] = ("\n" + this.characters[j]);
            break;
          } else {
            continue;
          }
        }
      }
      return peopleInMovie;
    },
  },
  async mounted() {
    const urlFilms = `https://swapi.dev/api/films`;
    let count = 1;

    let filmsResponse;
    let peopleResponse;

    this.errorMessage = "";
    try {
      filmsResponse = await fetch(urlFilms);
      const filmsData = await filmsResponse.json();
      this.movies = filmsData;

      while (count != 83) {
        if (count == 17)
        {
          count += 1;
        }

        peopleResponse = await fetch(
          `https://swapi.dev/api/people/` + count + `/`
        );
        this.urls[count] = `https://swapi.dev/api/people/` + count + `/`;
        const peopleData = await peopleResponse.json();
        this.characters[count] = peopleData.name;
        count += 1;
      }
    } catch (error) {
      if (filmsResponse || peopleResponse) {
        this.errorMessage = "Data is in the wrong format. Try again later.";
        console.log("ERROR 1");
      } else {
        this.errorMessage =
          "Could not send request. Check your internet connection.";
        console.log("ERROR 2");
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
  background-color: #202016;
  border-radius: 10px;
  box-shadow: -1rem 0 3rem rgba(189, 197, 69, 0.678);
  /*   margin-left: -50px; */
  transition: 0.5s ease-out;
}
.card:hover {
  transform: translateY(-20px);
  background-color: rgb(0, 0, 0);
  transition: 0.5s all;
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
h1 {
  margin: 1em;
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
  color: black;
}
p {
  color: rgb(241, 233, 111);
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
  display:list-item;
  background: rgb(143, 148, 67);
  color: rgb(255, 255, 255);
  position: absolute;
  opacity: 1;
  margin-left: 150px;
}
.expand:hover .opening-crawl {
  transition: 0.5s all;
  display: block;
  background: rgb(143, 148, 67);
  color: rgb(255, 255, 255);
  position: absolute;
  opacity: 1;
}
.expand {
  cursor: pointer;
}
</style>