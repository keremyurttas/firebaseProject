<template>
  <div id="app">
    <div class="wrapper p-20">
      <input
        v-model="search"
        type="text"
        placeholder="search film"
        class="border border-danger p-2 rounded-lg mb-12"
      />
      <!-- <span class="ml-12">{{ search }}</span> -->
      <button @click="nextPage" class="ml-10 bg-gray-800 text-white p-3 rounded-lg">NEXT</button>
      <div class="cards px-5 flex flex-wrap justify-center gap-x-8 gap-y-8">
        <movieCard
          v-for="movie in movies"
          :key="movie.id"
          :title="movie.title"
          :description="movie.overview"
          :img="`https://image.tmdb.org/t/p/w1280/${movie.backdrop_path}`"
        />
      </div>
    </div>
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <!-- <button @click="getFilms">Filmleri cek</button> -->
  </div>
</template>

<script>
import movieCard from "./components/movieCard.vue";
import axios from "axios";
// import HelloWorld from './components/HelloWorld.vue'
// const APIURL ="
// https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=04c35731a5ee918f014970082a0088b1&page=1
// ";
// const IMGPATH = "
// https://image.tmdb.org/t/p/w1280/
// ";
// const SEARCHAPI ="

// ";

export default {
  name: "App",
  components: {
    movieCard,
  },
  data() {
    return {
      search: "",
      movies: [],
      pageNumber: 1,
      pageURL:
        "https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=04c35731a5ee918f014970082a0088b1&page=",
      apiURL:
        "https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=04c35731a5ee918f014970082a0088b1&page=1",
      searchURL:
        "https://api.themoviedb.org/3/search/movie?&api_key=04c35731a5ee918f014970082a0088b1&query=",
    };
  },
  watch: {
    search: "searchMovie",
  },
  methods: {
    async nextPage() {
      this.pageNumber++;
      const data = await axios.get(this.pageURL + this.pageNumber.toString());
      const results = await data.data.results;
      this.movies = results;
    },
    async searchMovie(query) {
      console.log({ query });
      const data = await axios.get(this.searchURL + query);
      const results = await data.data.results;
      this.movies = results;
      console.log("searc film", results);
    },
    async getFilms() {
      const data = await axios.get(this.apiURL);
      // const response = await data.json()
      const results = await data.data.results;
      this.movies = results;
      // return data.data.results
    },
  },
  async created() {
    const data = await axios.get(this.apiURL);
    // const response = await data.json()
    const results = await data.data.results;
    console.log(results);
    this.movies = results;

    // console.log("data", data);
  },
  // components: {
  //   HelloWorld
  // }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center;
  color: #2c3e50;
  margin-top: 60px; */
}
</style>
