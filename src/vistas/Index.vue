<template>
  <h3>Quién es este Pokémon?</h3>

  <div class="row" :key="refreshKey">
    <div class="col s6 offset-s3">
      <input placeholder="p. ej.: charmander" type="text" v-model="nombre" >
    </div>

    <div class="col s12" v-if="pokemon">
      <Posta :key="pokemon.url" :name="pokemon.name" :url="pokemon.url"
        :bandera="nombre.toLowerCase() !== pokemon.name.toLowerCase()" @eventoActualizarPokemon="actualizarPokemon">
      </Posta>
    </div>
    <div v-else class="progress">
      <div class="preloader-wrapper big active">
        <div class="spinner-layer spinner-blue">
          <div class="circle-clipper">
            <div class="circle"></div>
          </div>
        </div>
      </div>
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