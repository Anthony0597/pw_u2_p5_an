<template>
  <PokemonPages/>
  
</template>

<script>
import PokemonPages from "./pages/PokemonPage.vue";

export default {
  name: "App",
  components: {
    PokemonPages,
  },
  data() {
    return {
      puntaje: 0,
      intento: 0,
      url1: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg",
      url2: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/2.svg",
      url3: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/3.svg",
      texto1: "xxxxxxxxx",
      texto2: "xxxxxxxxx",
      texto3: "xxxxxxxxx",
      mostrarGanador: false,
      mostrarPerdedor: false,
      mostrarJuego: true,
    };
  },
  methods: {
    async jugar() {
      this.texto1 = "charmander";
      //instancia 1
      const data1 = await this.consumirAPI();
      this.texto1 = data1.answer;
      this.url1 = data1.image;
      const data2 = await this.consumirAPI();
      this.texto2 = data2.answer;
      this.url2 = data2.image;
      const data3 = await this.consumirAPI();
      this.texto3 = data3.answer;
      this.url3 = data3.image;

      this.evaluarResultado();
    },
    async consumirAPI() {
      return await fetch("https://yesno.wtf/api").then((r) => r.json());
    },
    evaluarResultado() {
      this.intento++;
      if (
        this.texto1 === "yes" &&
        this.texto2 === "yes" &&
        this.texto3 === "yes"
      ) {
        this.puntaje += 5;
      } else if (
        (this.texto1 === "yes" && this.texto2 === "yes") ||
        (this.texto1 === "yes" && this.texto3 === "yes") ||
        (this.texto3 === "yes" && this.texto2 === "yes")
      ) {
        this.puntaje += 2;
      } else if (
        this.texto1 === "yes" ||
        this.texto2 === "yes" ||
        this.texto3 === "yes"
      ) {
        this.puntaje += 1;
      } else {
        this.puntaje += 0;
      }

      if (this.puntaje >= 10) {
        this.mostrarGanador = true;
        this.mostrarJuego = false;
        this.mostrarPerdedor = false;
      }

      if (this.intento === 5) {
        this.mostrarPerdedor = true;
        this.mostrarJuego = false;
        this.mostrarGanador = false;
      }
    },
    reiniciar() {
      this.puntaje = 0;
      this.intento = 0;
      this.url1 =
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg";
      this.url2 =
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/2.svg";
      this.url3 =
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/3.svg";
      this.texto1 = "xxxxxxxxx";
      this.texto2 = "xxxxxxxxx";
      this.texto3 = "xxxxxxxxx";
      this.mostrarGanador = false;
      this.mostrarPerdedor = false;
      this.mostrarJuego = true;
    },
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
  margin-top: 60px;
}
.container {
  display: grid;
  justify-content: center;
  align-content: center;
  grid-template-columns: repeat(4, 200px);
}
h1 {
  grid-column: span 4;
}
h2 {
  grid-column: span 2;
}
button {
  grid-column: 2;
}
.imagen {
  display: grid;
  grid-template-columns: repeat(3, 200px);
  justify-content: center;
  align-content: center;
  grid-column: span 4;
}
button {
  margin: 30px;
  border: 3px solid black;
}
</style>
