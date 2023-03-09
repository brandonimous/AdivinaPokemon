<script setup>
const pokemonProp = defineProps(['name', 'url', 'id']);

const id = pokemonProp.url.split('/')[6] + '.png';

//console.log(id);
</script>

<template>
    <div class="icon">
        <div class="icon-content">
            <img class="oscurecer"
                :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/' + id" />
        </div>
    </div>
    <h4>{{ name }}</h4>
</template>


