<script setup>
const pokemonProp = defineProps(['name', 'url', 'id']);

const id = pokemonProp.url.split('/')[6] + '.png';

//console.log(id);
</script>

<template>
    <div class="">
        <div class="card">
            <div class="card-content">
                <h3>{{ name }}</h3>

                <div class="icon">
                    <div class="icon-content">
                        <img class="oscurecer"
                            :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/' + id" />
                    </div>
                </div>
            </div>
        </div>


    </div>
</template>


