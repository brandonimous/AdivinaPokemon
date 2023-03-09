<script setup>
import Posta from "../components/Posta.vue";
import { ref, onMounted } from "vue";

const posts = ref([]);
var pokemon = ref(null);
const nombre = ref("");

onMounted(() => {
  fetch('https://pokeapi.co/api/v2/pokemon')
    .then(res => res.json())
    .then(data => {
      const randomIndex = Math.floor(Math.random() * data.results.length);
      pokemon.value = data.results[randomIndex];
    });
});

const actualizarPokemon = () => {
  fetch('https://pokeapi.co/api/v2/pokemon')
    .then(res => res.json())
    .then(data => {
      const randomIndex = Math.floor(Math.random() * data.results.length);
      pokemon.value = data.results[randomIndex];
      nombre.value = "";
    });
};

</script>

<template>
  <h3>Quién es este Pokémon?</h3>

  <div class="row" :key="refreshKey">

    <div class="col s6 offset-s3">
      <input placeholder="Quién es este Pokémon?" type="text" v-model="nombre">
    </div>

    <div class="col s12" v-if="pokemon && nombre.toLowerCase() === pokemon.name.toLowerCase()">

      <Posta v-if="pokemon" :key="pokemon.url" :name="pokemon.name" :url="pokemon.url"></Posta>
      <h5>Correcto!!</h5>
      <div class="col s12">
        <button class="green lighten-4" @click="actualizarPokemon">Siguiente Pokémon</button>
      </div>

    </div>
    <div v-else>
      <div class="col s12">

        <Posta class="" v-if="pokemon" :key="pokemon.url" :name="' '" :url="pokemon.url"></Posta>
        <div v-else class="progress">
          <div class="indeterminate"></div>
        </div>

      </div>
    </div>
    <div class="col s12">
      <button class="red lighten-4" @click="actualizarPokemon">Me rindo</button>  
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