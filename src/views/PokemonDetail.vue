<template>
  <div>
    <h1>Pokemon Detail: {{ pokemonName }}</h1>
    <div v-if="pokemon">
      {{ pokemon.name }}
      <br />
      <img :src="pokemon.sprites.front_default" :alt="pokemon.name" />
    </div>
  </div>
</template>

<script>
export default {
  name: "PokemonDetail",
  data() {
    return {
      pokemon: null,
    };
  },
  computed: {
    pokemonName() {
      return this.$route.params.name;
    },
  },
  methods: {
    getPokemonDetail() {
      fetch("https://pokeapi.co/api/v2/pokemon/" + this.pokemonName)
        .then((response) => response.json())
        .then((data) => (this.pokemon = data));
    },
  },
  beforeMount() {
    this.getPokemonDetail();
  },
  watch: {
    pokemonName() {
      this.pokemon = null;
      this.getPokemonDetail();
    },
  },
};
</script>