<script setup>
import { ref, onMounted } from 'vue';

const posts = ref([]);
const isLoading = ref(true);
const error = ref(null);

async function fetchPosts() {
  try {
    const response = await fetch('https://data.cityofnewyork.us/resource/hc8x-tcnd.json');
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    const data = await response.json();
    posts.value = data;
  } catch (err) {
    error.value = err.message;
  } finally {
    isLoading.value = false;
  }
}

const result = filter


const filterData()



</script>

<template>
  <div v-if="isLoading">Loading posts...</div>
  <div v-else-if="error">Error: {{ error }}</div>
  <ul v-else>
    <li v-for="post in posts" :key="post.id">
      {{ post.title }}
    </li>
  </ul>
</template>

<template>
  <h1>You did it!</h1>
  <p>
    Visit <a href="https://vuejs.org/" target="_blank" rel="noopener">vuejs.org</a> to read the
    documentation
  </p>
</template>




<style scoped></style>
