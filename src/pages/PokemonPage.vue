<template>
  <h1>Adivina el pokemon</h1>
  <PokemonImagen :pokemonId="2" :showPokemon="true" />
  <PokemonOpciones />
</template>

<script>
import PokemonImagen from "../components/PokemonImagen.vue";
import PokemonOpciones from "../components/PokemonOpciones.vue";
import obtenerPokemonsFachada from "../helpers/pokemonHelper";

export default {
  components: {
    PokemonImagen,
    PokemonOpciones,
  },
  mounted() {
    this.cargaInicial()
  },
  methods: {
    async cargaInicial() {
      console.log("se monto el componente pokemonpage");
      const arregloPokemons = await obtenerPokemonsFachada();
      console.log("desde componente");
      console.log(arregloPokemons);
    },
  },
};
</script>

<style>
</style>