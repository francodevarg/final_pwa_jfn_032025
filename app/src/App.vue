<template>
  <div id="app">
  <p>Nombre: {{ nombre }}</p>
  <p>Edad: {{ edad }}</p>
  <p>Ciudad: {{ ciudad }}</p>
  <p>"Hola, mi nombre es {{ nombre }}, tengo {{ edad }} años y vivo en {{ ciudad }}."</p>
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
        }
    },
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