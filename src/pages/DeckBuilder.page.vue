<template>
  <!-- Search input field -->
  <n-input v-model="search" placeholder="Rechercher un Pokémon" />

  <!-- Loading state -->
  <div v-if="loading">Loading Pokémon...</div>

  <!-- Pokémon list -->
  <div v-else>
    <div v-for="pokemon in filteredPokemons" :key="pokemon.id">
      <PokemonCard :pokemon="pokemon" />
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import axios from 'axios';

const search = ref('');
const pokemons = ref([]);
const loading = ref(true);

// Fetch Pokémon data from the API
onMounted(async () => {
  try {
    const response = await axios.get('https://pokemon-api-seyrinian-production.up.railway.app/pokemon-cards');
    pokemons.value = response.data.results;
  } catch (error) {
    console.error('Error fetching Pokémon data:', error);
  } finally {
    loading.value = false;
  }
});

// Filter Pokémon based on the search term
const filteredPokemons = computed(() => {
  return pokemons.value.filter(pokemon =>
    pokemon.name.toLowerCase().includes(search.value.toLowerCase())
  );
});
</script>

<style scoped>
/* Basic styling for the input field */
.n-input {
  margin-bottom: 20px;
  width: 100%;
  max-width: 400px;
}

/* Style for the Pokémon card list */
div {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

div > div {
  width: 150px;
}
</style>
