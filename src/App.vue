<script setup>
import { ref, computed } from 'vue'
import Personaje from './components/personajes.vue'

const url = 'https://rickandmortyapi.com/api/character/'
const id = ref('1')
const personajeObtenido = ref(null)

const ObtenerPersonaje = () => {
    fetch(url + id.value).then(response => {
        //verifica si solicitud exitosa (codigo de estado 200)
        if (response.status === 200) {
            return response.json();
        } else {
            throw new Error('No se pudo obtener la información');
        }
    })
        .then(data => {
            //manipula los datos obtenidos
            console.log(data);
            personajeObtenido.value = data
        })
        .catch(error => {
            console.error(error);
        });
}

</script>

<template>
        <div class="container">
        <h1>Componentes</h1>
        <hr>
        <input type="text" v-model=id >
        <hr>
        <button @click="ObtenerPersonaje()">Obtener</button>
        <hr>
        <Personaje v-if="personajeObtenido!=null" :personaje=personajeObtenido></Personaje>
    </div>
</template>

<style scoped></style>
