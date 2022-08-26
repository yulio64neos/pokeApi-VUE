<template>
    <div v-if="datos">
        <h1>Poke name: {{$route.params.name}}</h1>
        <img :src="datos.sprites?.front_default" alt="">
    </div>
    <h1 v-else>
        No existe ese Pokemon
    </h1>
        <button @click="back" class="btn btn-outline-primary">Volver</button>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios'
import { useRoute, useRouter } from 'vue-router';

const route = useRoute()
const router = useRouter()
const datos = ref({})

const back = () =>{
    router.push('/pokemons')
}

const getData = async() =>{
    try {
        const {data} = await axios.get(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`)
        console.log(data)
        datos.value = data;
    } catch (error) {
        console.log(error)
        datos.value = null
    }
}

getData();
</script>

<style>

</style>