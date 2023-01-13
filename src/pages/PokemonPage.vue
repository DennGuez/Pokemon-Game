<template>
    <div class="container">
        <h1>¿Quien es este Pokemon?</h1>

        <h3 v-if="!pokemon" >Espere por favor...</h3>
        <div v-else>
            <PokemonPicture :pokemon-id="pokemon.id" :show-pokemon="showPokemon" />
           <PokemonOptions
              :disable="disableLink"
              :pokemons="pokemonArr"
              @selection="checkAnswer(/*1,*/ $event)" />

            <template v-if="showAnswer" class="fade-in">
                <h2>{{ message }}</h2>
                <button @click="newGame" >Nuevo juego</button>
            </template>

        </div>
    </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
import PokemonPicture from '../components/PokemonPicture.vue'
import PokemonOptions from '../components/PokemonOptions.vue'
import getPokemonsOptions from '../helpers/getPokemonOptions'
import { Pokemon } from '../interfaces/Pokemon';

const pokemonArr = ref<Pokemon[]>([])
const pokemon = ref<Pokemon>()
const showPokemon = ref<boolean>(false)
const showAnswer = ref<boolean>(false)
const message = ref<string>('')
const disableLink = ref(true)

const mixPokemonArray = async() => {
    pokemonArr.value = await getPokemonsOptions()
    // console.table(JSON.parse(JSON.stringify(pokemonArr.value)))

    const rndInt = Math.floor( Math.random() * 4 )
    pokemon.value = pokemonArr.value[ rndInt ]
}

onMounted(() => {
    mixPokemonArray()
})

const checkAnswer = ( /*numero,*/ pokemonId: number) => {
    disableLink.value = false
    showPokemon.value = true
    showAnswer.value = true
    if ( pokemonId === pokemon.value?.id ) {
        message.value = `Correcto is ${ pokemon.value.name }!!`
    } else {
        message.value = `Oops was ${ pokemon.value!.name }!!`
    }

}

const newGame = () => {
    pokemonArr.value = []
    pokemon.value = undefined
    showPokemon.value = false
    showAnswer.value = false
    message.value = ''
    disableLink.value = true
    mixPokemonArray()
}
</script>

<style scoped>
.container {
    display: grid;
}
</style>