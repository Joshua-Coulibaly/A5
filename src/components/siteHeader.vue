<script setup>
import { useRouter } from "vue-router";

const router = useRouter();
const button = () => {
    router.push("/Login")
}
</script>

<template>
<h1>Movie Paradise</h1>

<button @click="button()" class="button">Login</button>
</template>

<style scoped>
h1{
    text-align: center;
    background-color:lightblue
}




</style>