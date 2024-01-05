<template>
  <div>
    <h2>{{ titulo }}</h2>
    <p>{{ counter }} <sup>2</sup> = {{ obtenerCuadradoComputado }}</p>
    <button @click="sumar">+1</button>
    <button @click="restar">-1</button>
  </div>
</template>

<script>
export default {
  /*props: ["titulo", "valor"],*/
  props: {
    titulo: String,
    valor: {
      type: Number,
      require: false,
      default: 100,
      validator(value) {
        return value > 0;
      },
    },
  },
  data() {
    return {
      counter: this.valor,
    };
  },
  methods: {
    obtenerCuadrado() {
      console.log("Se calcula el cuadrado");
      return this.counter * this.counter;
    },
    sumar() {
      this.counter++;
    },
    restar() {
      this.counter--;
    },
  },
  computed: {
    obtenerCuadradoComputado() {
      console.log("Se calcula el cuadrado computado");
      return this.counter * this.counter;
    },
  },
};
</script>

<style scoped>
button {
  background-color: #64b687;
  border-radius: 5px;
  border: 1px solid #304c4b;
  color: white;
  cursor: pointer;
  margin: 0px 5px;
  padding: 5px 15px;
}
button:hover {
  background-color: #304c4b;
}

h2 {
  font-style: italic;
  font-family: 'Times New Roman', Times, serif;
}

p, sup{
font-style: italic;
font-family: 'Courier New', Courier, monospace;
}
</style>