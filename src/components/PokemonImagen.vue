<template>
  <div class="pokemonContainer">    
    <img
      class="ocultar"
      :src="imagenFuente"
      alt="No se puede mostrar"
    />
    <img :src="imagenFuente" alt="No se puede mostrar" v-if="showPokemon" />
  </div>
</template>

<script>
export default {
  props: {
    pokemonId: {
      type: Number,
      required: true,
    },
    showPokemon: {
      type: Boolean,
      required: true,
      default: false,
    },
  },
  computed: {
    imagenFuente() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`;
    },
  },
};
</script>

<style scoped>
.ocultar {
  filter: brightness(0);
}
img {
  height: 200px;
  position: absolute;
  right: 42%;
}
.pokemonContainer {
  height: 200px;
}
</style>