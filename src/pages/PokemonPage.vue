<template>
  <h1 v-if="pokemonGanador === nul">
    Espere por favo estamos cargando el juego
  </h1>
  <div v-if="pokemonGanador!==null">
    <h1>Adivina el pokemon</h1>
    <PokemonImagen :pokemonId="pokemonGanador.id" :showPokemon="mostrarPokemon" />
    <PokemonOpciones :pokemons="pokemonArr" @selecciono="revisarClick($event)"/>
  </div>
</template>

<script>
import PokemonImagen from "../components/PokemonImagen.vue";
import PokemonOpciones from "../components/PokemonOpciones.vue";
import obtenerPokemonsFachada from "../helpers/pokemonHelper.js";

export default {
  components: {
    PokemonImagen,
    PokemonOpciones,
  },
  beforeCreate() {
    console.log("antes de crear el componenete");
  },
  created() {
    console.log("se creo el componente");
  },
  beforeMount() {
    console.log("antes de que se monte el componente en la página");
  },
  mounted() {
    this.cargaInicial();
    console.log("se monto el componente pokemonpage");
  },
  beforeUpdate() {
    console.log("antes de que se actualice el componente");
  },
  updated() {
    console.log("Se actualiza el componente");
  },
  beforeDestroy() {
    console.log("antes de destruir");
  },
  destroyed() {
    console.log("Destruido");
  },
  methods: {
    async cargaInicial() {
      const arregloPokemons = await obtenerPokemonsFachada();
      console.log("desde componente");
      console.log(arregloPokemons);
      this.pokemonArr = arregloPokemons;
      const indiceGanador = Math.floor(Math.random() * 4);
      this.pokemonGanador = this.pokemonArr[indiceGanador];
    },
    revisarClick(datoRecibido){
      console.log("Dio click, reporto desde el padre");
      console.log(datoRecibido.id);
      console.log(datoRecibido.hobby);
      console.log(datoRecibido.nom);
      this.mostrarPokemon=true;

      if(this.pokemonGanador.id===datoRecibido.id){
        console.log("GANOOOO!!!!!");
      }
    }
  },
  data() {
    return {
      pokemonArr: [],
      pokemonGanador: null,
      mostrarPokemon:false,
    };
  },
};
</script>

<style>
</style>