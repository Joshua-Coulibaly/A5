<script setup>
import { ref } from "vue";
import axios from "axios"
import SiteModal from '../components/SiteModal.vue';

const movies = ref("");
const response = ref(null);
const showModal = ref(false);
const selectedId = ref(0);
 
const openModal = (id) => {
  showModal.value = true;
  selectedId.value = id;
};
 
const closeModal = () => {
  showModal.value = false;
};
 
const getMovies = async () => {
  response.value = (await getData(`https://api.themoviedb.org/3/trending/movie/week`, {
    params: {
      api_key: "464558c39f92ed4e861ee35019feed2f",
      append_to_response: "videos",
    }
  })).data['results']
}
 
const getData = async (url, params) => {
  try {
    return await axios.get(url, params);
  } catch (error) {
    console.log(error)
  }
};
 
await getMovies();
</script>
 
<template>
  <h1 id="movies"> Movies </h1>
  <template v-if="response">
    <div v-for="result in response" class="Movies-contanier">

      <img @click="openModal(result.id)" v-bind:src="'https://image.tmdb.org/t/p/w500' + result.poster_path" />
    </div>
  </template>
  <SiteModal v-if="showModal" @toggleModal="closeModal()" :id="selectedId" />
</template>
 
<style>
.Movies-contanier {
  display: flex;
  display: inline-grid;
  align-content: space-evenly;
  padding: 10px;
  gap: 10px;
  margin-bottom: -300px;
  padding-bottom: -50px;
  margin-right: -10px;
  margin-left: 15px;
  background-color: lightblue;
}
 
img {
  height: 50%;
  border-radius: 1rem;
  padding: 10px;
  cursor: pointer;
}
 
h1 {
  text-align: center;
  font-size: 100px;
}
 
.footer {
  text-align: center;
  padding-top: 60px;
}
</style>
