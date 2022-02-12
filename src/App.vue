<template>
  <div id="app">
    <div class="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <div class="nav" v-if="pokemons">
      <a
        href="#"
        v-if="pokemons.previous"
        @click.prevent="getPokemonsList(pokemons.previous)"
      >
        Previous Page
      </a>
      <router-link
        v-for="pokemon in pokemons.results"
        :key="pokemon.name"
        :to="'/pokemon/' + pokemon.name"
      >
        {{ pokemon.name }}
      </router-link>
      <a
        href="#"
        v-if="pokemons.next"
        @click.prevent="getPokemonsList(pokemons.next)"
      >
        Next Page
      </a>
    </div>
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      pokemons: null,
    };
  },
  methods: {
    getPokemonsList(url) {
      //  fetch pokemons list from api
      fetch(url)
        .then((response) => response.json())
        .then((data) => (this.pokemons = data));
    },
  },
  beforeMount() {
    this.getPokemonsList("https://pokeapi.co/api/v2/pokemon/");
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.nav {
  padding: 30px;
}

.nav a {
  font-weight: bold;
  color: #2c3e50;
  margin: 5px;
}

.nav a.router-link-exact-active {
  color: #42b983;
}
</style>
