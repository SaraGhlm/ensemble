<template>
  <v-card width="300" min-height="600" class="mx-auto">
    <v-img height="400" :src="src">
      <template v-slot:placeholder>
        <v-row class="fill-height ma-0" align="center" justify="center">
          <v-progress-circular
            indeterminate
            color="grey lighten-4"
          ></v-progress-circular>
        </v-row>
      </template>
    </v-img>

    <v-card-text class="pb-2">
      <p class="text-h6">{{ title }}</p>

      <p class="text-subtitle-1">
        {{ year }}
      </p>
    </v-card-text>

    <v-card-actions class="py-0">
      <v-spacer></v-spacer>

      <v-btn @click="alert"> Button </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "Movie",

  props: {
    src: String,
    title: String,
    year: String,
  },

  methods: {
    alert() {
      alert(this.title);
    },
  },
};
</script>

<style>
</style>