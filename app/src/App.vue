<template>
  <div id="app">
    <p>Nombre: {{ nombre }}</p>
    <p>Edad: {{ edad }}</p>
    <p>Ciudad: {{ ciudad }}</p>
    <p>"Hola, mi nombre es {{ nombre }}, tengo {{ edad }} años y vivo en {{ ciudad }}."</p>
    <br>
    <h2>Contador</h2>
    <p>{{ contador }}</p>
    <button @click="incrementar">Incrementar</button>
    <button @click="decrementar">Decrementar</button>
  </div>
</template>

<script>
export default {
  name: 'App',
      data() {
        return {
            nombre: "Ana García",
            edad: 30,
            ciudad: "Tupungato",
            contador: 0  
        }
    },
    methods: {
      incrementar() {
        this.contador++;
        console.log("Contador incrementado a:", this.contador);
      },
      decrementar() {
        this.contador--; 
        console.log("Contador decrementado a:", this.contador);
      } 
    }
}
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