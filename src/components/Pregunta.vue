<template>
  <img
    src="https://media.es.wired.com/photos/6501e7429fa9000811a95fe8/16:9/w_2560%2Cc_limit/Adobe%2520Firefly.jpeg"
    alt="No se puede visualizar"
  />
  <div class="dark"></div>

  <div class="container">
    <input v-model="pregunta" type="text" />
    <p>Recuerda que debes terminar con el signo de interrogación (?)</p>

    <h2>{{ pregunta }}</h2>
    <h1>SI, NO.......</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pregunta: "Voy a ser millonario",
    };
  },
  watch: {
    pregunta(value, oldvalue) {
      console.log(value);
      console.log(oldvalue);
      if (!value.includes("?")) return;
      //Consumo del API
      this.consumirAPI()
    },
  },
  methods: {
    async consumirAPI() {
      const {answer,image} = await fetch("https://yesno.wtf/api").then((respuesta) =>
        respuesta.json()
      );
      console.log(answer)
      console.log(image)
    },
  },
};
</script>

<style scoped>
.dark,
img {
  height: 100vh;
  width: 100vw;
  max-height: 100%;
  max-width: 100%;
  position: fixed;
  top: 0px;
  left: 0px;
}

.dark {
  background-color: rgba(0, 0, 0, 0.5);
}

input {
  width: 250px;
  height: 25px;
  padding: 10px, 15px;
  border-radius: 5px;
  border: none;
}

input:focus {
  outline: none;
}

.container {
  position: relative;
}
p {
  color: white;
  font-size: 20px;
  margin-top: 0px;
}

h1,
h2 {
  color: white;
}

h2 {
  margin-top: 150px;
}
</style>