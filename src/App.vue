<template>
  <h1 class="title">Projeto Calculadora</h1>

  <div class="container">
    <div class="calculadora">
      <div class="valores">
        <input type="number" disabled :value="numeros.x">
        <strong>{{ operacao }}</strong>
        <input type="number" disabled :value="numeros.y"> 

      </div>

      <div class="botoes">
        <button limpar @click="limpar()">C</button>
        <button>()</button>
        <button>%</button>
        <button operacao @click="adicionarOperacao($event.target.innerText)">/</button>
        <button @click="adicionarNumero($event.target.innerText)">7</button>
        <button @click="adicionarNumero($event.target.innerText)">8</button>
        <button @click="adicionarNumero($event.target.innerText)">9</button>
        <button operacao @click="adicionarOperacao($event.target.innerText)">*</button>
        <button @click="adicionarNumero($event.target.innerText)">4</button>
        <button @click="adicionarNumero($event.target.innerText)">5</button>
        <button @click="adicionarNumero($event.target.innerText)">6</button>
        <button operacao @click="adicionarOperacao($event.target.innerText)">-</button>
        <button @click="adicionarNumero($event.target.innerText)">1</button>
        <button @click="adicionarNumero($event.target.innerText)">2</button>
        <button @click="adicionarNumero($event.target.innerText)">3</button>
        <button operacao @click="adicionarOperacao($event.target.innerText)">+</button>
        <button>+/-</button>
        <button @click="adicionarNumero($event.target.innerText)">0</button>
        <button>,</button>
        <button calcular @click="calcular()">=</button>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      resultado: "",
      numeros: {
        x: 0,
        y: 0,
      },
      operacao: ""
    }
  },

  methods: {
    adicionarOperacao(operacao) {
      this.operacao = operacao
    },
    adicionarNumero(caracter) {
      if (!this.operacao) {
        this.numeros.x = Number(caracter)
      }else {
        this.numeros.y = Number(caracter)
      }
    },
    limpar() {
      this.operacao = ""
      this.numeros.x = 0
      this.numeros.y = 0
    },
    calcular() {
      const { x, y } = this.numeros
      if(this.operacao === "+") {
        this.numeros.x = this.soma(x, y)
        this.numeros.y = 0
        this.operacao = ""
      } else if(this.operacao === "-") {
        this.numeros.x = this.menos(x, y)
        this.numeros.y = 0
        this.operacao = ""
      } else if(this.operacao === "/") {
        this.numeros.x = this.divisao(x, y)
        this.numeros.y = 0
        this.operacao = ""
      }else if(this.operacao === "*") {
        this.numeros.x = this.multiplicacao(x, y)
        this.numeros.y = 0
        this.operacao = ""
      }
    },
    soma: (x, y) => x + y,
    menos: (x, y) => x - y,
    divisao: (x, y) => x / y,
    multiplicacao: (x, y) => x * y,

  }
}
</script>

<style>
body, html{
  margin: 0;
  padding: 0;
  background-color: #33344a;
}

.title {
  text-align: center;
}

.container {
  display: flex;
  height: 100%;
  padding: 2rem;
  justify-content: center;
}

.calculadora {
  box-sizing: border-box;
  border: 2px solid #000;
  width: 24rem;
  height: 32rem;
  background-color: #FFF;
}

.botoes {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(5, 1fr);
  gap: 0.5rem;
  height: calc(100% - 7rem);
}

.botoes button {
  background-color: #3d3e52;
  border: 0;
  color: #FFF;
}

.botoes button:hover {
  background-color: #3a3c4e;
  color: #000;
}

.botoes button[operacao] {
  color: lightcoral;
}

.botoes button[limpar] {
  color: rgb(202, 66, 17);
}

.botoes button[calcular] {
  background-color: rgb(204, 107, 107);
}

.valores {
  display: grid;
  height: 7rem;
  grid-template-rows: repeat(3, 1fr);
  align-items: center;
  justify-content: end;
}

.valores strong, input {
  text-align: end;
  background: none;
  border: none;
  outline: none;
  font-size: 2rem;
}

.valores strong {
  font-size: 1rem;
  padding-right: 1rem;
}
</style>