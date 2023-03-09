<template>
  <h3>Quién es este Pokémon?</h3>

  <div class="row" :key="refreshKey">
    <div class="col s6 offset-s3">
      <input placeholder="p. ej.: charmander" type="text" v-model="nombre">
    </div>

    <div class="col s12" v-if="pokemon && nombre.toLowerCase() === pokemon.name.toLowerCase()">
      <Posta :key="pokemon.url" :name="pokemon.name" :url="pokemon.url"></Posta>
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

<script setup>
import Posta from "../components/Posta.vue";
import { ref, onMounted } from "vue";

const pokemon = ref(null);
const nombre = ref("");

onMounted(() => {
  obtenerPokemonAleatorio();
});

const obtenerPokemonAleatorio = () => {
  fetch('https://pokeapi.co/api/v2/pokemon')
    .then(res => res.json())
    .then(data => {
      const randomIndex = Math.floor(Math.random() * data.results.length);
      pokemon.value = data.results[randomIndex];
      nombre.value = "";
    });
};

const actualizarPokemon = () => {
  obtenerPokemonAleatorio();
};

</script>

<style>
.icon {
  height: 300px;
  width: 300px;
  font-size: 100px;
  overflow: hidden;
  display: inline-flex;
}

.icon-content {
  height: auto;
  display: flex;
  position: relative;
  left: -5em;
  filter: drop-shadow(5em 0 0px #2596be);
}
</style>