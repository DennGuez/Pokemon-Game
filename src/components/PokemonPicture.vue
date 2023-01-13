<template>
    <div class="pokemon-container">
        <img :src="imgSrc"
            class="hidden-pokemon">
        <img v-if="showPokemon" :src="imgSrc">
    </div>
</template>

<script setup lang="ts">
import { computed, toRef } from 'vue'

interface Props {
    pokemonId: number
    showPokemon: boolean
}

const props = withDefaults(defineProps<Props>(), {
    pokemonId: 1,
    showPokemon: false,
})

const pokemonId = toRef( props, 'pokemonId')

const imgSrc = computed(() =>{
    return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${ pokemonId.value }.svg`
})
</script>

<style scoped>
/* Pokemon Picture */
.pokemon-container {
    height: 200px;
}
img {
    height: 200px;
    position: absolute;
    right: 32%;
    user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    -webkit-user-drag: none;
    -webkit-user-select: none;
}
.hidden-pokemon {
    filter: brightness(0);
}
</style>