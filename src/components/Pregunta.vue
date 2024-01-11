<template>
  <img v-if="img !== null" :src="img" alt="No se puede visualizar" />
  <div class="dark"></div>

  <div class="container">
    <input v-model="pregunta" type="text" />
    <p>Recuerda que debes terminar con el signo de interrogación (?)</p>
    <div v-if="preguntaValida===true">
      <h2>{{ pregunta }}</h2>
      <h1>{{ respuesta }}</h1>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pregunta: null,
      respuesta: null,
      img: null,
      preguntaValida: false,
    };
  },
  watch: {
    pregunta(value, oldvalue) {
      this.preguntaValida=false;
      console.log(value);
      console.log(oldvalue);
      if (!value.includes("?")) return;
      //Consumo del API
      this.consumirAPI();
      this.preguntaValida=true;
    },
  },
  methods: {
    async consumirAPI() {
      this.respuesta="Pensando."
      this.respuesta="Pensando.."
      
      const { answer, image } = await fetch("https://yesno.wtf/api").then(
        (respuesta) => respuesta.json()
      );
      console.log(answer);
      console.log(image);
      this.respuesta="Pensando..."
      this.respuesta="Pensando...."
      this.respuesta = answer==='yes'?'SI!':'NO';
      this.img = image;
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