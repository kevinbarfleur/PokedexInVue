<template>
  <div class="pokedex-container">
    <header class="header">
      <div class="main-title">
        <h1>Pokedex</h1>
        <img class="icon" src="../assets/pokeball.png" alt />
      </div>
      <p class="main-subtitle">Basic pokedex in Vue.js</p>
    </header>
    <transition name="fade" mode="out-in">
      <div class="loading" v-if="pokemonsLength !== 151" key="loading">{{ pokemonsLength }}</div>
      <div class="cards-container" v-else key="cards">
        <div class="card" v-for="pokemon in pokemons" :key="pokemon.id">
          <PokemonCard :name="pokemon.name" :sprite="pokemon.sprites.front_default" />
        </div>
      </div>
    </transition>
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
  },
  computed: {
    pokemonsLength() {
      // 151 * 100 % 151 = 100%
      return this.pokemons.length
    }
  }
}
</script>

<style lang="scss">
.main-title {
  display: flex;
  flex-direction: row;

  font-family: 'Press Start 2P', cursive;

  .icon {
    margin: auto;
    margin-left: 10px;
    width: 50px;
    height: 50px;
  }
}
.pokedex-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.loading {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translateX(-50%) translateY(-50%);
  border: 1px solid grey;
  width: 200px;
  padding: 5px 0px;
  border-radius: 10px;
}
.cards-container {
  margin: 100px auto;
  width: 80%;
  display: flex;
  justify-content: center;
  flex-direction: row;
  flex-wrap: wrap;
}
.card {
  min-width: 200px;
  margin: auto 5%;
}
.fade-enter-active,
.fade-leave-active {
  transition-property: opacity;
  transition-duration: 0.5s;
}

.fade-enter-active {
  transition-delay: 0.25s;
}

.fade-enter,
.fade-leave-active {
  opacity: 0;
}
</style>