<template>
  <v-card width="300" min-height="600" class="mx-auto d-flex flex-column">
    <v-img height="400" lazy-src="@/assets/ImageNotAvailable.png" :src="src">
    </v-img>

    <v-card-text class="pb-2">
      <p class="text-h6">{{ title }}</p>

      <p class="text-subtitle-1">
        {{ year }}
      </p>
    </v-card-text>

    <v-card-actions>
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