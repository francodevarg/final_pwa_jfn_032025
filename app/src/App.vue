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
    <br>
    <h2>Lista de Tareas</h2>
    <p>Total de Tareas: {{ totalTareas }} - Tareas pendientes: {{ tareasPendientes.length }}</p>
    <!-- Input para agregar una nueva tarea -->
    <input type="text" v-model="nuevaTarea" placeholder="Agregar nueva tarea">
    <button @click="agregarTarea">Agregar</button>
    <br>
    <br>
    <!-- Lista de tareas -->
    <ul>
      <li v-for="tarea in tareas" :key="tarea.id">
        <input type="checkbox" v-model="tarea.completada">
        <span :style="{ textDecoration: tarea.completada ? 'line-through' : 'none' }">{{ tarea.texto }}</span>
      </li>
    </ul>

  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'App',
      data() {
        return {
            nombre: "Ana García",
            edad: 30,
            ciudad: "Tupungato",
            contador: 0,
            nuevaTarea: "",
            tareas: [
              { id: 1, texto: "Aprender Vue", completada: false },
            ]  
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
      },
      //Tareas
      agregarTarea() {
        if (this.nuevaTarea.trim() !== "") {
          const nuevaTareaObj = {
            id: Date.now(),
            texto: this.nuevaTarea,
            completada: false
          };
          this.tareas.push(nuevaTareaObj);
          this.nuevaTarea = ""; // Limpiar el input después de agregar la tarea
        }
      },
      //Axios Posts
      async obtenerPosts(postId) {
        try {
          const response = await axios.get(`https://jsonplaceholder.typicode.com/posts/${postId}`);
          console.log("Posts obtenidos:", response.data);
        } catch (error) {
          console.error("Error al obtener posts:", error);
        }
      },
      async obtenerCommentsFromPost(postId) {
        try {
          const response = await axios.get(`https://jsonplaceholder.typicode.com/posts/${postId}/comments`);
          console.log("Comments obtenidos:", response.data);
        } catch (error) {
          console.error("Error al obtener comments:", error);
        }
      }
    },
    computed: {
      tareasPendientes() {
        return this.tareas.filter(tarea => tarea.completada === false);
      },
      totalTareas() {
        return this.tareas.length;
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