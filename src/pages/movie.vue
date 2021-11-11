<script setup>
import { useRoute } from "vue-router";

import { useAPI } from "../composables/useAPI";

const route = useRoute();

const { id } = route.params;

const { movie, getMovie, quotes, getQuotes } = useAPI();

getMovie(id);
getQuotes(id);

const who = async (id) => {
  const character = await getCharacter(id);
  console.log(character.name);
};
</script>

<template>
  <div
    v-if="movie"
    class="max-w-md py-8 mx-auto mt-16 text-center bg-white rounded-lg"
  >
    <h3 class="text-xl font-semibold tracking-tight">{{ movie.name }}</h3>
    <p>Runtime: {{ movie.runtimeInMinutes }} minutes</p>
    <p>Budget in Millions: ${{ movie.budgetInMillions }}</p>
    <p>Academic Awards: {{ movie.academyAwardWins }}</p>
    <p>Rotten Tomatoes: {{ movie.rottenTomatoesScore }}</p>
  </div>
  <div v-else>Loading...</div>
  <div class="mt-8">
    <p
      class="px-4 py-6 my-4 text-xl italic text-center bg-white rounded-lg"
      v-for="quote in quotes"
      :key="quote._id"
    >
      {{ quote.dialog }}
    </p>
  </div>
</template>
