<template>
  <!-- Tests filtres :  v-show="this.visible" -->
  <div class="pokemon-card">
    <h3 class="pokemon-name">{{ this.pokemonName }}</h3>
    <p>
      Type :
      <span :style="{ color: this.pokemonColorType }">{{ this.formatUpper(this.pokemonType) }}</span>
    </p>
    <img :src="this.pokemonSprite" :alt="'sprite ' + this.pokemonName" />
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quis sit nam maxime. Accusamus, veritatis tempora harum voluptatem ut perspiciatis provident.</p>
    <div id="button" :style="{ borderColor: this.pokemonColorType }">
      <div id="slide" :style="{ backgroundColor: this.pokemonColorType }"></div>
      <a href="#" :style="{ color: this.pokemonColorType }">Show More &#8594;</a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    type: String,
    sprite: String
    // Test filtres => visible: Boolean
  },
  data() {
    return {
      pokemonName: '',
      pokemonType: '',
      pokemonColorType: '',
      pokemonSprite: ''
    }
  },
  mounted() {
    this.getProps()
    this.typeToColor()
  },
  methods: {
    getProps() {
      this.pokemonName = this.formatUpper(this.name)
      this.pokemonType = this.type
      this.pokemonSprite = this.sprite
      // Tests Filtres : this.showCard = this.visible
    },
    formatUpper(name) {
      return name.charAt(0).toUpperCase() + name.substr(1)
    },
    typeToColor() {
      switch (this.pokemonType) {
        case 'poison':
          this.pokemonColorType = '#9C27B0'
          break
        case 'fire':
          this.pokemonColorType = '#FF3D00'
          break
        case 'flying':
          this.pokemonColorType = '#BBDEFB'
          break
        case 'water':
          this.pokemonColorType = '#2196F3'
          break
        case 'bug':
          this.pokemonColorType = '#9E9D24'
          break
        case 'steel':
          this.pokemonColorType = '#546E7A'
          break
        case 'normal':
          this.pokemonColorType = '#9E9E9E'
          break
        case 'electric':
          this.pokemonColorType = '#FDD835'
          break
        case 'ground':
          this.pokemonColorType = '#8D6E63'
          break
        case 'ice':
          this.pokemonColorType = '#80DEEA'
          break
        case 'fairy':
          this.pokemonColorType = '#F48FB1'
          break
        case 'grass':
          this.pokemonColorType = '#43A047'
          break
        case 'fighting':
          this.pokemonColorType = '#212121'
          break
        case 'psychic':
          this.pokemonColorType = '#311B92'
          break
        case 'rock':
          this.pokemonColorType = '#4E342E'
          break

        default:
          this.pokemonColorType = '#f4511e'
          break
      }
    }
  }
}
</script>

<style lang="scss">
.pokemon-card {
  max-width: 300px;
  min-width: 200px;

  padding: 5%;
  margin: 20% auto;

  background-color: white;
  border: 1px solid #fafafa;
  border-radius: 10px;
  box-shadow: 2px 2px 25px lightgrey;
  transition: 0.3s;

  &:hover {
    transform: translateY(2px) translateX(2px);
    box-shadow: 1px 1px 10px lightgrey;
    transition: 0.3s;
  }

  #button {
    position: relative;
    overflow: hidden;
    cursor: pointer;

    display: inline-flex;
    border: 1px solid #f4511e;
    margin: 10px auto;
    text-decoration: none;
    align-items: center;
    justify-content: center;
    overflow: hidden;

    border-radius: 2px;
  }

  #button a {
    text-decoration: none;
    color: #f4511e;
    position: relative;
    transition: all 0.35s ease-Out;
    padding: 1px 10px;
  }

  #slide {
    width: 100%;
    height: 100%;
    left: -200px;
    background: #f4511e;
    position: absolute;
    transition: all 0.35s ease-Out;
    bottom: 0;
  }

  #button:hover #slide {
    left: 0;
  }

  #button:hover a {
    color: white !important;
  }
}
</style>