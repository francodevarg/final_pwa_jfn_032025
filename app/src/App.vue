<template>
  <div id="app">
    <p>Nombre: {{ nombre }}</p>
    <p>Edad: {{ edad }}</p>
    <p>Ciudad: {{ ciudad }}</p>
    <p>"Hola, mi nombre es {{ nombre }}, tengo {{ edad }} años y vivo en {{ ciudad }}."</p>
    <hr>
    <h2>Contador</h2>
    <p>{{ contador }}</p>
    <button @click="incrementar">Incrementar</button>
    <button @click="decrementar">Decrementar</button>
    <hr>
    <h2>Lista de Tareas</h2>
    <p>Total de Tareas: {{ totalTareas }} - Tareas pendientes: {{ tareasPendientes.length }}</p>
    <!-- Input para agregar una nueva tarea -->
    <input type="text" v-model="nuevaTarea" placeholder="Agregar nueva tarea">
    <button @click="agregarTarea">Agregar</button>
    <!-- Lista de tareas -->
    <ul>
      <li v-for="tarea in tareas" :key="tarea.id">
        <input type="checkbox" v-model="tarea.completada">
        <span :style="{ textDecoration: tarea.completada ? 'line-through' : 'none' }">{{ tarea.texto }}</span>
      </li>
    </ul>

    <hr>
    <h2>Posts y Comments con Axios</h2>
    <div>
      <div class="post-content" v-for="post in posts" :key="post.id" style="border: 1px solid #ccc; margin-bottom: 10px; padding: 10px;">
        <h3>{{post.id}} - {{ post.title }}</h3>
        <p>{{ post.body }}</p>
        <button @click="mostrarComments(post.id)">Mostrar Comments</button>
      </div>
      <div v-if="comments.length > 0" style="border: 1px solid #ccc; padding: 10px; margin-top: 20px;">
        <h3>Comments del Post: {{ comments[0].postId }}</h3>
        <ul>
          <li v-for="comment in comments" :key="comment.id">
            <p><strong>{{ comment.name }}</strong> ({{ comment.email }}): {{ comment.body }}</p>
          </li>
        </ul>
      </div>
      </div>


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
            ],
            posts:[],
            comments:[],
            showcomments: false  
        }
    },
    async created() {
      const TOTAL_POSTS = 10;
      for (let i = 0; i < TOTAL_POSTS; i++) {
        const post = await this.obtenerPosts(i + 1);
        this.posts.push(post);
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
          return response.data;
        } catch (error) {
          console.error("Error al obtener posts:", error);
        }
      },
      async obtenerCommentsFromPost(postId) {
        try {
          const response = await axios.get(`https://jsonplaceholder.typicode.com/posts/${postId}/comments`);
          return response.data;
        } catch (error) {
          console.error("Error al obtener comments:", error);
        }
      },
      async mostrarComments(postId) {
        this.comments = await this.obtenerCommentsFromPost(postId);
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