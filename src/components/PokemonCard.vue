<template>
  <div class="pokemon-card">
    <h3 class="pokemon-name">{{ this.pokemonName }}</h3>
    <img :src="this.pokemonSprite" :alt="'sprite ' + this.pokemonName" />
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quis sit nam maxime. Accusamus, veritatis tempora harum voluptatem ut perspiciatis provident.</p>
    <!-- <button class="card-button">Show More</button> -->
    <div id="button">
      <div id="slide"></div>
      <a href="#">Show More &#8594;</a>
    </div>
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
      this.pokemonName = this.formatName(this.name)
      this.pokemonSprite = this.sprite
    },
    formatName(name) {
      return name.charAt(0).toUpperCase() + name.substr(1)
    }
  }
}
</script>

<style lang="scss">
.pokemon-card {
  //   cursor: pointer;
  max-width: 300px;
  min-width: 200px;

  padding: 5%;
  margin: 20% auto;

  border: 1px solid #fafafa;
  border-radius: 10px;
  box-shadow: 2px 2px 25px lightgrey;
  transition: 0.3s;

  &:hover {
    transform: translateY(2px) translateX(2px);
    box-shadow: 1px 1px 10px lightgrey;
    transition: 0.3s;
  }

  .card-button {
  }

  /* Second Button */

  #button {
    position: relative;
    overflow: hidden;
    cursor: pointer;

    display: inline-flex;
    // height: 40px;
    // width: 150px;
    border: 1px solid #4fc3f7;
    margin: 10px auto;
    text-decoration: none;
    align-items: center;
    justify-content: center;
    overflow: hidden;

    border-radius: 2px;
  }

  #button a {
    text-decoration: none;
    color: #4fc3f7;
    position: relative;
    transition: all 0.35s ease-Out;
    padding: 1px 10px;
  }

  #slide {
    width: 100%;
    height: 100%;
    left: -200px;
    background: #4fc3f7;
    position: absolute;
    transition: all 0.35s ease-Out;
    bottom: 0;
  }

  #button:hover #slide {
    left: 0;
  }

  #button:hover a {
    color: white;
  }
}
</style>