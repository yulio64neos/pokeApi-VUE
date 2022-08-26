<template>
  <h1>Pokemons</h1>
  <ul>
    <li v-for="(pok, index) in pokemons" :key="index">
        <router-link :to="`/pokemons/${pok.name}`">
            {{pok.name}}
        </router-link>        
    </li>
  </ul>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'
import {RouterLink} from 'vue-router'

const pokemons = ref([])
const getData = async () => {
    try
    {
        const {data} = await axios.get('https://pokeapi.co/api/v2/pokemon/')
        pokemons.value = data.results
    }
    catch(error)
    {
        console.log(error)
    }
}

getData();
</script>

<style>

</style>