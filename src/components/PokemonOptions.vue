<template>
  <div class="options-container">
    <ul>
      <li
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        @click="$emit('selection', pokemon.id )"
      >
      {{  pokemon.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "PokemonOptions",
  props:{
    pokemons: {
      type: Array,
      required: true
    }
  },
  data() {
    return {};
  },

  mounted() {
    
  },

  methods: {

  },
}
</script>

<style scoped>
/* Pokemon Options */
ul {
  list-style-type: none;
  padding: 0;
}

li {
  background-color: #f5f5f5;
  border: 1px solid #dcdcdc;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  margin-bottom: 10px;
  padding: 10px;
  width: 250px;
  transition: background-color 0.3s ease;
}

li:hover {
  background-color: #f0f0f0;
}

.options-container {
  display: flex;
  justify-content: center;
}

</style>
