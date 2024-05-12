<script>
// export default {
//   async asyncData() {
//     const response = await fetch('https://pokeapi.co/api/v2/pokemon?limit=151');
//     const data = await response.json();
//     return { pokemons: data.results };
//   }
// };
export default {
  data() {
    return {
      loading: true,
      pokemons: [],
    };
  },
  async mounted() {
    try {
      const response = await $fetch('https://pokeapi.co/api/v2/pokemon?limit=151');
      this.pokemons = response.results;
      this.loading = false;
    } catch (error) {
      console.error('Error while loading pokemons :', error);
    }
  },
};
</script>

<template>
  <div>
    <h1>Liste des Pokémon</h1>
    <ul>
      <li v-for="pokemon in pokemons.slice(0, 15)" :key="pokemon.name">
        <nuxt-link :to="'/pokemon/' + pokemon.name">{{ pokemon.name }}</nuxt-link>
      </li>
    </ul>
  </div>
</template>

