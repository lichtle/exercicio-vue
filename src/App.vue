<script setup>
import { reactive } from "vue";

const estado = reactive({
  resultado: 0,
  numero1: 0,
  numero2: 0,
  filtro: "soma",
});

function capturarPrimeiroNumero(event) {
  estado.numero1 = parseInt(event.target.value); // Transformando o número capturado no input, que está em formato de string, em um dado do tipo number
}

function capturarSegundoNumero(event) {
  estado.numero2 = parseInt(event.target.value);
}

function realizarOperacao() {
  const filtro = estado.filtro;

  switch (filtro) {
    case "soma":
      estado.resultado = estado.numero1 + estado.numero2;
      return estado.resultado;
    case "subtracao":
      estado.resultado = estado.numero1 - estado.numero2;
      return estado.resultado;
    case "divisao":
      estado.resultado = estado.numero1 / estado.numero2;
      return estado.resultado;
    case "multiplicacao":
      estado.resultado = estado.numero1 * estado.numero2;
      return estado.resultado;
  }
}
</script>

<template>
  <div class="container container-flex">
    <header><h1>Calculadora Aritmética com Vue</h1></header>
    <main>
      <label for="operacao">Selecione o tipo da operação desejada: </label>
      <select
        id="operacao"
        required
        @change="(evento) => (estado.filtro = evento.target.value)"
      >
        <option value="soma">Soma</option>
        <option value="subtracao">Subtração</option>
        <option value="divisao">Divisão</option>
        <option value="multiplicacao">Multiplicação</option>
      </select>
      <div class="numero">
        <label for="first-number">Primeiro número: </label>
        <input
          type="number"
          id="first-number"
          required
          @keyup="capturarPrimeiroNumero"
          placeholder="0"
        />
      </div>
      <div class="numero">
        <label for="second-number">Segundo número: </label>
        <input
          type="number"
          id="second-number"
          required
          @keyup="capturarSegundoNumero"
          placeholder="0"
        />
      </div>
      <div class="resultado">
        <p>Resultado: {{ realizarOperacao() }}</p>
      </div>
    </main>
  </div>
</template>

<style scoped>
* {
  font-family: Arial, Helvetica, sans-serif;
}
.container {
  max-width: 1024px;
  margin: 0 auto;
}

.container-flex {
  /* Adicionar aos containers com display flex */
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

header {
  margin-top: 100px;
}

h1 {
  margin-bottom: 50px;
}

select {
  margin-bottom: 40px;
}

input {
  padding: 5px;
}

.numero {
  display: flex;
  flex-direction: column;
  margin-bottom: 30px;
  text-align: center;
}

.numero label {
  margin-bottom: 8px;
}

.resultado {
  margin-top: 50px;
  text-align: center;
}
</style>
