<template>
  <v-app>
    <MovieSearch />
  </v-app>
</template>

<script>
import MovieSearch from "./components/MovieSearch";

export default {
  name: "App",

  components: {
    MovieSearch,
  },
};
</script>
