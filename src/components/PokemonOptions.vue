<template>
    <div class="options-container">
        <ul>
            <li
              v-for="pokemon in pokemons"
              :key="pokemon.id"
              @click="$emit('selection', pokemon.id)"
              :class="!disable ? 'disabled' : ''"
              >
              {{ pokemon.name }}
            </li>
        </ul>
    </div>
</template>

<script setup lang="ts">
import { toRef } from 'vue';
import { Pokemon } from '../interfaces/Pokemon';

const props = defineProps<{ 
    pokemons: Pokemon[] 
    disable: boolean
}>()
const pokemons = toRef(props, 'pokemons')

</script>

<style scoped>
/* Pokemon Options */
ul {
    list-style-type: none;
}
li {
    background-color: white;
    border-radius: 5px;
    border: 1px solid rgba(0, 0, 0, 0.2);
    cursor: pointer;
    margin-bottom: 10px;
    width: 250px;
}

li:hover {
    background-color: rgba(0, 0, 0, 0.05);
}

.options-container {
    display: flex;
    justify-content: center;
}

.disabled {
  pointer-events: none;
  cursor: default;
  opacity: 0.6;
}

</style>