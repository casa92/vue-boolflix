<template>
  <div id="app">
    <Header @inputRefresh="search"/>
    <h2>Film</h2>
    <Main :movieItemList="moviesArray"/>
    <h2>Serie Tv</h2>
    <Main :seriesItemList="seriesArray"/>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";
import axios from 'axios';
export default {
  name: "App",
  components: {
    Header,
    Main,

  },
  data: function() {
    return {
      queryInputValue: '',
      apiKeyValue: '9383eb0e39275dd36956e0deb30c8e02',
      moviesArray: [],
      seriesArray: [],
    };
  },
  methods: {
    search: function(userInputString) {
      this.queryInputValue = userInputString;
      this.getMovies();
      this.getSeries();
    },
    getMovies: function() {
      axios.get(
        'https://api.themoviedb.org/3/search/movie',
        {
          params: {
            api_key: this.apiKeyValue,
            query: this.queryInputValue,
          }
        }
      ).then((response) => {
        this.moviesArray = response.data.results;
      });
    },
    getSeries: function() {
      axios.get(
        'https://api.themoviedb.org/3/search/tv',
        {
          params: {
            api_key: this.apiKeyValue,
            query: this.queryInputValue,
          }
        }
      ).then((response) => {
        this.seriesArray = response.data.results;
      });
    },
  }
};
</script>

<style lang="scss">

</style>
