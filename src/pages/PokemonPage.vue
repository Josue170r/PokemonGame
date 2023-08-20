<template>
  <div v-if="pokemon">
    <h1>¿Quién es este Pokemon?</h1>

    <PokemonPicture
      :pokemonId="pokemon.id"
      :showPokemon="showPokemon" />
    <PokemonOptions
      :pokemons
      ="pokemonArr" 
      @selection="checkAnswer"
    />

    <div v-if="showAnswer" class="fade-in">
      <h2>{{  message  }}</h2>
      <button @click="newGame">
        Nuevo juego
      </button>
    </div>

  </div>
  <div v-else>
    <h1>Espere por favor ....</h1>
  </div>
</template>

<script>
import PokemonOptions from "@/components/PokemonOptions"
import PokemonPicture from "@/components/PokemonPicture"
import getPokemonOptions from '@/helpers/getPokemonOptions'


export default {
  name: "PokemonPage",
  components: {
    PokemonOptions,
    PokemonPicture,
  },
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: null
    }
  },

  mounted() {
    this.mixpoemonArray()
  },

  methods: {
    async mixpoemonArray() {
      this.pokemonArr = await getPokemonOptions()
      const rndInt = Math.floor(Math.random() * 4)
      this.pokemon = this.pokemonArr[rndInt]
    },
    checkAnswer(pokemonId) {
      this.showAnswer = true
      if (pokemonId === this.pokemon.id) {
        this.showPokemon = true
        this.message = `Correcto, ${this.pokemon.name}`
      }else {
        this.message = `Opps, era ${this.pokemon.name} `
      }
    },
    newGame() {
      this.showPokemon = false
      this.showAnswer = false
      this.pokemon = null
      this.pokemonArr = []
      this.mixpoemonArray()
    }
  },
}
</script>

<style scoped></style>
