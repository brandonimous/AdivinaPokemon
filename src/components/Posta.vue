<script setup>
const pokemonProp = defineProps(['name', 'url', 'id', 'bandera']);

const id = pokemonProp.url.split('/')[6] + '.png';

</script>

<template>
    <div :class="{ 'icon': bandera, 'iconDesactivado': !bandera }">
        <div :class="{ 'icon-content': bandera, 'icon-contentDesactivado': !bandera }">
            <img :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/' + id" />
        </div>
    </div>

    <div v-if="!bandera">
        <h4 class="borde">{{ name }}</h4>
        <!--<button class="red lighten-3 bordeBoton" @click="$emit('eventoActualizarPokemon')">Me rindo</button>-->
        <button class="green lighten-3 bordeBoton" @click="$emit('eventoActualizarPokemon')">Siguiente Pokémon</button>
    </div>
    <div v-else="bandera">
        <h4 class="borde">????????????</h4>
        <!--<button class="red lighten-3 bordeBoton" @click="$emit('eventoActualizarPokemon')">Me rindo</button>-->
        <button class="green lighten-3 bordeBoton" disabled>Siguiente Pokémon</button>
    </div>
</template>


