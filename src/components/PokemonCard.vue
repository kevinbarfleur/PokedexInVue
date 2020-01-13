<template>
  <transition name="fade" mode="out-in">
    <div class="pokemon-card">
      <h3 class="pokemon-name">{{ this.pokemonName }}</h3>
      <p>
        Type :
        <span
          :style="{ color: this.pokemonColorType }"
        >{{ this.formatUpper(this.pokemonType) }}</span>
      </p>
      <img :src="this.pokemonSprite" :alt="'sprite ' + this.pokemonName" />
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quis sit nam maxime. Accusamus, veritatis tempora harum voluptatem ut perspiciatis provident.</p>
      <div id="button" :style="{ borderColor: this.pokemonColorType }">
        <div id="slide" :style="{ backgroundColor: this.pokemonColorType }"></div>
        <a href="#" :style="{ color: this.pokemonColorType }">Show More &#8594;</a>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  /***************
       PROPS 
  ***************/
  props: {
    name: String,
    type: String,
    sprite: String,
    color: String
  },
  /***************
       STATE 
  ***************/
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
  },
  /***************
      METODS 
  ***************/
  methods: {
    getProps() {
      this.pokemonName = this.formatUpper(this.name)
      this.pokemonType = this.type
      this.pokemonColorType = this.color
      this.pokemonSprite = this.sprite
    },
    formatUpper(name) {
      return name.charAt(0).toUpperCase() + name.substr(1)
    }
  }
}
</script>

<style lang="scss">
.pokemon-card {
  max-width: 300px;
  min-width: 200px;

  padding: 5%;
  margin: 20% 50px 20% 50px;

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