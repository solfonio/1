<script setup>
import { watch, ref } from 'vue';

const props = defineProps({
    episodios: null
});

const listaEpisodios = ref([])

watch(
  () => props.episodios,
  (newValue) => {
    listaEpisodios.value = []
    for (let indice in newValue) {
      let urlEpisodio = (newValue[indice])

      fetch(urlEpisodio)
        .then(response => {
          if (response.status === 200) {
            return response.json(); // Convierte la respuesta a JSON
          } else {
            throw new Error('No se pudo obtener la información');
          }
        })
        .then(data => {
          listaEpisodios.value.push(data) //Obtengo el results que es donde esta mi vector que quiero trabajar
        })
        .catch(error => {
          console.error(error);
        });
    }
  }
);

</script>
<template>
    <div class="card" style="width: 18rem;">
        <div class="card-body">
            <table class="table">
                <th>
                    <h5 class="card-title"> "Apariciones:" </h5>
                </th>
                <tr v-for="(episodio) in listaEpisodios"><td>{{ episodio.name }}</td></tr>
            </table>
        </div>
    </div>
</template>