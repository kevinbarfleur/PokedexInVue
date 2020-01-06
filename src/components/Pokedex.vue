<template>
  <div class="pokedex-container">
    <header class="header">
      <div class="main-title">
        <h1>Pokedex</h1>
        <img class="icon" src="../assets/pokeball.png" alt />
      </div>
      <p class="main-subtitle">Basic pokedex in Vue.js</p>
    </header>
    <div class="filters">
      <div class="checkbox-container" v-for="type in types" :key="type">
        <input type="checkbox" :name="type" :id="type" v-model="type.filters" />
        <label :for="type">{{ type }}</label>
      </div>
    </div>
    <transition name="fade" mode="out-in">
      <div class="loading" v-if="pokemonsLength !== 151" key="loading">
        <div class="loading-bar"></div>
        {{ percentage + "%" }}
      </div>
      <div class="cards-container" v-else key="cards">
        <div class="card" v-for="pokemon in pokemons" :key="pokemon.id">
          <PokemonCard
            :name="pokemon.name"
            :sprite="pokemon.sprites.front_default"
            :type="pokemon.types[0].type.name"
          />
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
      pokemons: [],
      types: [],
      filters: []
    }
  },
  mounted() {
    this.getDatas()
    this.$set(this, this.filters, this.types)
  },
  methods: {
    getDatas() {
      for (let i = 1; i <= 151; i++) {
        const url = `https://pokeapi.co/api/v2/pokemon/${i}`
        fetch(url)
          .then(res => res.json())
          .then(pokemon => {
            setTimeout(() => {
              this.pokemons.push(pokemon)

              const formatedType = this.formatUpper(pokemon.types[0].type.name)

              if (!this.types.includes(formatedType)) {
                this.types.push(formatedType)
              }
            }, 1000)
          })
      }
    },
    formatUpper(name) {
      return name.charAt(0).toUpperCase() + name.substr(1)
    },
    updateFilters(filter) {
      console.log(filter)
    }
  },
  computed: {
    pokemonsLength() {
      return this.pokemons.length
    },
    typesLenght() {
      return this.types.length
    },
    percentage() {
      return Math.round((100 * this.pokemonsLength) / 150)
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
.filters {
  position: fixed;
  top: 50%;
  left: -10px;
  display: flex;
  flex-direction: column;
  transform: translateY(-50%);
  /*  CHECKBOX ANIMATION  */

  .checkbox-container {
    background-color: #fff;
    display: block;
    position: relative;

    label {
      padding: 12px 30px;
      width: 100%;
      display: block;
      text-align: left;
      color: #3c454c;
      cursor: pointer;
      position: relative;
      z-index: 2;
      transition: color 200ms ease-in;
      overflow: hidden;

      &:before {
        width: 10px;
        height: 10px;
        border-radius: 50%;
        content: '';
        background-color: #5562eb;
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%) scale3d(1, 1, 1);
        transition: all 300ms cubic-bezier(0.4, 0, 0.2, 1);
        opacity: 0;
        z-index: -1;
      }

      &:after {
        width: 32px;
        height: 32px;
        content: '';
        border: 2px solid #d1d7dc;
        background-color: #fff;
        background-image: url("data:image/svg+xml,%3Csvg width='32' height='32' viewBox='0 0 32 32' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M5.414 11L4 12.414l5.414 5.414L20.828 6.414 19.414 5l-10 10z' fill='%23fff' fill-rule='nonzero'/%3E%3C/svg%3E ");
        background-repeat: no-repeat;
        background-position: 2px 3px;
        border-radius: 50%;
        z-index: 2;
        position: absolute;
        right: 30px;
        top: 50%;
        transform: translateY(-50%);
        cursor: pointer;
        transition: all 200ms ease-in;
      }
    }

    input:checked ~ label {
      color: #fff;

      &:before {
        transform: translate(-50%, -50%) scale3d(56, 56, 1);
        opacity: 1;
      }

      &:after {
        background-color: #54e0c7;
        border-color: #54e0c7;
      }
    }

    input {
      width: 32px;
      height: 32px;
      order: 1;
      z-index: 2;
      position: absolute;
      right: 30px;
      top: 50%;
      transform: translateY(-50%);
      cursor: pointer;
      visibility: hidden;
    }
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
  width: 200px;
  padding: 5px 0px;
  border-radius: 10px;

  color: #212121;
  font-size: 1.1em;
  font-family: 'Press Start 2P', cursive;

  .loading-bar {
    z-index: -1;
    position: absolute;
    top: 0px;
    left: 0px;
    width: 100%;
    height: 100%;
    background-color: #f4511e;
    border-radius: 9px;
  }
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