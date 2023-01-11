<script setup>
import axios from 'axios';
const props = defineProps(["id"]);
const emits = defineEmits(["toggleModal"]);
const info = await axios.get(`https://api.themoviedb.org/3/movie/${props.id}`, {
      params: {
        api_key: "f944b70daa59b60504fca0c383e63483",
        append_to_response: "videos"
      },
    })
console.log(info)
</script>

<template>

  <Teleport to="body">
    <div class="modal-outer-container" @click.self="emits('toggleModal')">
      <div class="modal-inner-container">
        <button class="close-button" @click="emits('toggleModal')">X</button>
        <img :src="`https://image.tmdb.org/t/p/w500${info.data.poster_path}`" alt="">
        <p> {{info.data.original_title}}</p>
        <p> Release Date: {{info.data.release_date}}</p>
        <iframe :src="`https://www.youtube.com/embed/${info.data.videos.results.filter((video) => video.type === 'Trailer').at(0).key}`"></iframe>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
.modal-outer-container {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background: #00000099;
  z-index: 3;
  font-size: 20px;
  font-family: 'Bangers', cursive;
}
.modal-outer-container .modal-inner-container {
  background-color: rgb(29, 28, 28);
  color: white;
  width: clamp(280px, 100%, 800px);
  height: 400px;
  position: relative;
  
}
.modal-outer-container .modal-inner-container .close-button {
  position: absolute;
  right: 0px;
  padding: 1rem;
  border: none;
  background: #1F2123;
  font-weight: bold;
  font-size: 1.25rem;
  color: white;
}
img {
  width: 250px;
  height: 400px;
  float: right;

}
iframe {
  width: 320px;
  height: 170px;

}
</style>