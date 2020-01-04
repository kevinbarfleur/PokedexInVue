<template>
  <div class="pokemon-card">
    <h3 class="pokemon-name">{{ this.pokemonName }}</h3>
    <img :src="this.pokemonSprite" :alt="'sprite ' + this.pokemonName" />
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    sprite: String
  },
  data() {
    return {
      pokemonName: '',
      pokemonSprite: ''
    }
  },
  mounted() {
    this.getProps()
  },
  methods: {
    getProps() {
      this.pokemonName = this.name
      this.pokemonSprite = this.sprite
    }
  }
}
</script>

<style lang="scss">
.pokemon-card {
  max-width: 400px;
  min-width: 200px;

  padding: 5%;
  margin: 10% auto;

  border: 1px solid #fafafa;
  border-radius: 10px;
  box-shadow: 2px 2px 25px lightgrey;

  .pokemon-name {
  }
}
</style>