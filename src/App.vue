<script setup>
import { ref } from 'vue'
import usePokemon from '@/composables/usePokemon'
import useBattle from '@/composables/useBattle'
import PokemonCard from '@/components/PokemonCard.vue'

const { pokemons, isLoading, loadPokemons } = usePokemon()
const { fightPokemons } = useBattle()

const winner = ref()

const startFight = () => {
  const [pokemon1, pokemon2] = pokemons.value
  winner.value = fightPokemons(pokemon1, pokemon2)
}

const reset = () => {
  winner.value = null
  loadPokemons()
}


</script>

<template>
  <div class="container">
  <h1>
    <img class="logo" src="/pokemonlogo.png" alt="Pokemon Logo">
  </h1>
  
    <div>
      <button
        @click="reset"
      >
        Get Pokemons
      </button>
    </div>
    
    <div
      v-if="isLoading"
    >
      Loading pokemons...
    </div>

    <div v-else>
      <div class="innerContainer">
        <PokemonCard
          v-bind="pokemons[0]"
          :is-winner="pokemons[0].name === winner"
        />

        <p>V/S</p>

        <PokemonCard
          v-bind="pokemons[1]"
          :is-winner="pokemons[1].name === winner"
        />
      </div>

      <button
        class="fightButton"
        :disabled="winner"
        @click="startFight"
      >
        Fight!
      </button>
    </div>
  </div>
</template>