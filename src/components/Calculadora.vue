<template>
  <div class="container">
    <div class="calculadora">
      <div id="resultado" class="display">{{ resultado }}</div>
      <button class="btn_span2" @click="inicializar()">C</button>
      <button @click="borrarNum()">&#8592;</button>
      <button @click="agregarOpe('/')">/</button>
      <button @click="agregarNum('7')">7</button>
      <button @click="agregarNum('8')">8</button>
      <button @click="agregarNum('9')">9</button>
      <button @click="agregarOpe('*')">&#215;</button>
      <button @click="agregarNum('4')">4</button>
      <button @click="agregarNum('5')">5</button>
      <button @click="agregarNum('6')">6</button>
      <button @click="agregarOpe('-')">&#8722;</button>
      <button @click="agregarNum('1')">1</button>
      <button @click="agregarNum('2')">2</button>
      <button @click="agregarNum('3')">3</button>
      <button @click="agregarOpe('+')">&#43;</button>
      <button class="btn_span2" @click="agregarNum('0')">0</button>
      <button @click="agregarNum('.')">&#46;</button>
      <button @click="calcular()">&#61;</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      num1: "",
      num2: "",
      ope: "",
      comp: 0,
      resultado: "",
      flotante: false,
    };
  },
  methods: {
    limpiarL() {
      this.num1 = "";
      this.num2 = "";
      this.ope = "";
      this.comp = 0;
      this.flotante = false;
    },
    inicializar() {
      this.limpiarL();
      this.resultado = "";
    },
    agregarNum(nume) {
      if (nume === ".") {
        if (this.flotante) {
          nume = "";
        }
        this.flotante = true;
      }
      switch (this.comp) {
        case 0:
          this.num1 = this.num1 + nume;
          break;
        case 1:
          this.num2 = this.num2 + nume;
      }
      this.actualizarRes();
    },
    borrarNum() {
      if (this.comp == 0) {
        this.num1 = this.num1.substring(0, this.num1.length - 1);
      } else if (this.comp == 1) {
        this.num2 = this.num2.substring(0, this.num2.length - 1);
      }
      this.actualizarRes();
    },
    agregarOpe(operador) {
      if ((this.num1 === "") & (this.resultado !== "")) {
        this.num1 = this.resultado;
      }
      if ((this.num1 !== "") & (this.num1 != ".") & (this.comp !== 1)) {
        this.ope = operador;
        this.comp++;
        this.flotante = false;
      }
      this.actualizarRes();
    },
    actualizarRes() {
      this.resultado = this.num1 + this.ope + this.num2;
    },
    trf(num) {
      return parseFloat(num);
    },
    calcular() {
      switch (this.ope) {
        case "+":
          this.resultado = this.trf(this.num1) + this.trf(this.num2);
          break;
        case "-":
          this.resultado = this.trf(this.num1) - this.trf(this.num2);
          break;
        case "*":
          this.resultado = this.trf(this.num1) * this.trf(this.num2);
          break;
        case "/":
          this.resultado = this.trf(this.num1) / this.trf(this.num2);
          break;
        default:
          this.limpiarL();
      }
      this.limpiarL();
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.calculadora {
  display: grid;
  /*grid-template-columns: 75px 75px 75px 75px;*/
  grid-template-columns: repeat(4, 75px);
  grid-template-rows: 100px repeat(5, 75px);
  background-color: #00916e;
  padding: 15px;
  border-radius: 32px;
  box-shadow: 15px 10px 5px 5px #00000033;
}

.display {
  grid-column: span 4;
  padding: 30px 15px;
  margin: 10px 20px 10px 20px;
  background-color: #363636;
  border-radius: 32px;
  text-align: right;
  box-shadow: 0px 0px 0px 10px #00000033;
}

button {
  margin: 5px;
  padding: 0;
  border-radius: 32px;
  border: none;
  background-color: #02c799;
  box-shadow: 5px 5px 10px 2px #00000040;
  font-size: 25px;
}

button:active {
  background-color: #006f54;
}

.btn_span2 {
  grid-column: span 2;
}

body {
  background-color: #224870;
}

* {
  color: white;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}
</style>