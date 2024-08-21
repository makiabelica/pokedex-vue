<template>
  <div class="pokedex">
    <h1>Pokedex</h1>
    <div v-if="loading" class="loading">Loading...</div>
    <div v-if="error" class="error">Error: {{ error }}</div>
    <h1 class="title">Pokedex</h1>
    <div class="cards-container" v-if="pokemons">
      <div v-for="pokemon in pokemons" :key="pokemon.name" class="card">
        <img :src="getPokemonImage(pokemon.name)" alt="Pokemon image" class="card-image" />
        <h2 class="card-title">{{ pokemon.name }}</h2>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Pokedex',
  data() {
    return {
      pokemons: null,
      loading: true,
      error: null,
    };
  },
  async created() {
    try {
      const response = await axios.get('https://pokeapi.co/api/v2/pokemon?limit=32'); 
      this.pokemons = response.data.results;
    } catch (err) {
      this.error = err.message;
    } finally {
      this.loading = false;
    }
  },
  methods: {
    getPokemonImage(name) {
      const pokemonNumber = name.toLowerCase().replace(' ', '-');
      return `https://img.pokemondb.net/artwork/large/${pokemonNumber}.jpg`;
    },
  },
};
</script>

<style scoped>
.title{
    text-align: center;
    color: black;
}
.pokedex {
  text-align: center;
  padding: 20px;
}

.loading {
  font-size: 1.2em;
}

.error {
  color: red;
  font-size: 1.2em;
}

.cards-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
  justify-content: center;
  align-items: start;
}

.card {
  background-color: #f8f8f8;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 200px; /* Tamaño fijo para las cartas */
  text-align: center;
  padding: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.card-image {
  max-width: 100%;
  height: 150px;
  object-fit: cover;
  border-radius: 8px;
}

.card-title {
  font-size: 1em;
  margin: 10px 0 0;
  color: black
}
</style>
