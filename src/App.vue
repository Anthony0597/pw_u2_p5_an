<template>
  <Pregunta/>
</template>

<script>
import Contador from "./components/Contador.vue";
import Calculadora from "./components/Calculadora.vue";
import Pregunta from "./components/Pregunta.vue"

export default {
  name: "App",
  components: {
    Contador,
    Calculadora,
    Pregunta
  },
 methods:{
   calcularValor() {
    return 5 + 5 * 100;
  }
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
</style>
