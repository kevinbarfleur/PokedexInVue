<template>
  <div class="pokedex-container">
    <header class="header">
      <h1 class="main-title">Pokedex</h1>
      <p class="main-subtitle">Basic pokedex in Vue.js</p>
    </header>
    <div class="cards-container">
      <div class="card" v-for="pokemon in pokemons" :key="pokemon.id">
        <PokemonCard :name="pokemon.name" :sprite="pokemon.sprites.front_default"></PokemonCard>
      </div>
    </div>
  </div>
</template>

<script>
import PokemonCard from './PokemonCard'

export default {
  components: {
    PokemonCard
  },
  props: {
    name: String,
    sprite: String
  },
  data() {
    return {
      pokemons: []
    }
  },
  mounted() {
    this.getDatas()
  },
  methods: {
    getDatas() {
      for (let i = 1; i <= 151; i++) {
        const url = `https://pokeapi.co/api/v2/pokemon/${i}`
        fetch(url)
          .then(res => res.json())
          .then(pokemon => {
            this.pokemons.push(pokemon)
          })
      }
    }
  }
}
</script>

<style lang="scss">
.pokedex-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.cards-container {
  display: flex;
  justify-content: space-evenly;
  flex-direction: row;
  flex-wrap: wrap;
}
</style>