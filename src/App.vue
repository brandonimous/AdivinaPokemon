<script setup>
import Posta from "./components/Posta.vue";

import { ref } from "vue";

const posts = ref([]);

fetch('https://pokeapi.co/api/v2/pokemon')
  .then(res => res.json())
  .then(data => posts.value = data.results);
</script>

<template>
  <div class="container">
    <h2>Pokémon</h2>
    <Posta v-for="posta in posts" :key="posta.url" :name="posta.name" :url="posta.url"></Posta>
  </div>
</template>

<style>
.oscurecer {
  filter: brightness(0%);
}
</style>
