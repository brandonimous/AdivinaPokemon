<script setup>
import Posta from "./components/Posta.vue";

import { ref, onMounted } from "vue";

const posts = ref([]);

var pokemon = ref(null);


const nombre = ref("");


/*fetch('https://pokeapi.co/api/v2/pokemon')
  .then(res => res.json())
  .then(data => posts.value = data.results);*/

onMounted(() => {
  fetch('https://pokeapi.co/api/v2/pokemon')
    .then(res => res.json())
    .then(data => {
      const randomIndex = Math.floor(Math.random() * data.results.length);
      pokemon.value = data.results[randomIndex];
    });
});

</script>

<template>
  <h2>Pokémon</h2>
  <div class="row">
    <!--<Posta v-for="posta in posts" :key="posta.url" :name="posta.name" :url="posta.url"></Posta>-->

    <Posta v-if="pokemon" :key="pokemon.url" :name="pokemon.name" :url="pokemon.url"></Posta>

    <div v-else class="progress">
      <div class="indeterminate"></div>
    </div>
  </div>

  <div class="row">
    <input placeholder="Quién es este Pokémon?" type="text" v-model="nombre">

    <div v-if="pokemon && nombre.toLowerCase() === pokemon.name.toLowerCase()">
      El nombre ingresado coincide con el atributo name.
    </div>
  </div>
</template>

<style>
.icon {
  font-size: 100px;
  overflow: hidden;
  display: inline-flex;
}

.icon-content {
  display: flex;
  position: relative;
  left: -1em;
  filter: drop-shadow(1em 0 0px #2596be);
}
</style>

