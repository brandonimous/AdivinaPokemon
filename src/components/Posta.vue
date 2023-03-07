<script setup>
const pokemonProp = defineProps(['name', 'url', 'id']);

const id = pokemonProp.url.split('/')[6] + '.png';
//console.log(id);
</script>

<template>
    <div class="container">
        <h3>{{ name }}</h3>
        <img class="oscurecer" :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/' + id" />
    </div>
</template>
