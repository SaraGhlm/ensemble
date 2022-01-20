<template>
  <v-container>
    <v-app-bar app color="indigo darken-4" dark prominent>
      <v-app-bar-title class="text-no-wrap hidden-xs-only align-self-center">
        OMDB Movie Search
      </v-app-bar-title>

      <v-container class="align-self-center">
        <v-layout row wrap justify-end>
          <v-flex xs12 sm8 md4>
            <v-text-field
              class="mx-2"
              label="Movie Title"
              v-model="title"
              :rules="[rules.required]"
              @keydown.enter="searchMovie"
            ></v-text-field>
          </v-flex>

          <v-flex xs6 sm6 md2>
            <v-text-field
              class="mx-2"
              label="Year"
              v-model="year"
              type="number"
            ></v-text-field>
          </v-flex>

          <v-flex xs6 sm2 md2>
            <v-btn @click="searchMovie" icon class="mx-2">
              <v-icon>mdi-magnify</v-icon>
            </v-btn>
          </v-flex>
        </v-layout>
      </v-container>
    </v-app-bar>

    <v-main>
      <v-container>
        <v-row class="text-center">
          <v-flex>
            <v-container fluid grid-list-lg class="">
              <v-card flat>
                <v-layout row wrap>
                  <v-flex v-for="movie in movies" :key="movie.imdbID">
                    <v-card flat hover class="white">
                      <v-layout>
                        <v-flex>
                          <Movie
                            :title="movie.Title"
                            :src="movie.Poster"
                            :year="movie.Year"
                          />
                        </v-flex>
                      </v-layout>
                    </v-card>
                  </v-flex>
                </v-layout>
                <!-- Add here the vuetify directive -->
                <v-card v-intersect="loadMore"></v-card>
              </v-card>
            </v-container>
          </v-flex>
        </v-row>
      </v-container>
    </v-main>
  </v-container>
</template>

<script>
import Movie from "./Movie";

export default {
  name: "MovieSearch",

  components: {
    Movie,
  },

  data: () => ({
    title: "",
    url: "http://www.omdbapi.com/?",
    titleParam: "s=",
    apiKeyParam: "&apikey=5e55a98a",
    pageParam: "&page=",
    yearParam: "&y=",
    year: "",
    page: 1,
    movies: [],
    rules: {
      required: (value) => !!value || "Required.",
    },
  }),

  methods: {
    searchMovie(event) {
      event.preventDefault();
      this.page = 1;
      const endpoint = `${this.url}${this.titleParam}${this.title}${this.yearParam}${this.year}${this.pageParam}${this.page}${this.apiKeyParam}`;

      const xhr = new XMLHttpRequest();
      xhr.responseType = "json";

      xhr.onreadystatechange = () => {
        if (xhr.readyState === XMLHttpRequest.DONE) {
          this.movies = xhr.response.Search;
        }
      };

      xhr.open("GET", endpoint);
      xhr.send();
    },

    loadMore() {
      if (this.title !== "") {
        this.page++;
        console.log(this.page);
        const endpoint = `${this.url}${this.titleParam}${this.title}${this.yearParam}${this.year}${this.pageParam}${this.page}${this.apiKeyParam}`;

        const xhr = new XMLHttpRequest();
        xhr.responseType = "json";

        xhr.onreadystatechange = () => {
          if (xhr.readyState === XMLHttpRequest.DONE) {
            this.movies.push(...xhr.response.Search);
          }
        };

        xhr.open("GET", endpoint);
        xhr.send();
      }
    },
  },
};
</script>

<style>
.v-app-bar-title__content {
  width: 250px !important;
}
</style>