<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const posts = ref([]);

const fetchPosts = async () => {
  try {
    const response = await axios.get('http://localhost:8080/posts');
    posts.value = response.data;
  } catch (error) {
    console.error('Error al traer los posts:', error);
  }
};

onMounted(() => {
  fetchPosts();
});
</script>

<template>
  <h1>Todos los Posts</h1>
 <table id="posts">
    <thead>
      <tr>
        <th>N.º</th>
        <th>Título</th>
        <th>Acción</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(post, index) in posts" :key="post.id">
        <td>{{ index + 1 }}</td>
        <td>{{ post.title }}</td>
        <td>
          <button class="btn btn-green">Ver</button>
          <button class="btn btn-blue">Editar</button>
          <button class="btn btn-red">Borrar</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>