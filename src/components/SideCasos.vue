<template>
  <div class="w-full h-full bg-gradient-to-b from-blue-900">
    <div class="flex flex-col items-center h-full ">
      <!-- Card de Informações de Casos -->
      <div class="p-6 m-4 bg-transparent rounded-lg shadow-2xl shadow-violet-500">
        <h2 class="mb-4 text-2xl font-bold">ESTADO DE CASOS BRAZIL</h2>
        <p class="text-xl">País: {{ country }}</p>
        <p class="text-xl">Casos Confirmados: {{ confirmed }}</p>
        <p class="text-xl">Casos Totais: {{ cases }}</p>
        <p class="text-xl">Mortes: {{ deaths }}</p>
        <p class="text-xl">Recuperados: {{ recovered }}</p>
        <p class="text-xl">Última atualização: {{ updatedAt }}</p>
      </div>
      
      <!-- Card de Logo da Empresa -->
      <div class="p-6 m-4 rounded-lg shadow-lg">
        <img src="./logo.png" alt="Logo da Empresa" class="mx-auto h-28">
        <!-- Informações adicionais da empresa podem ser adicionadas aqui -->
      </div>
    </div>
  </div>
</template>

<script setup>
import {
  onMounted,
  ref,
} from 'vue';

import axios from 'axios';

const country = ref('');
const cases = ref('');
const confirmed = ref('');
const deaths = ref('');
const recovered = ref('');
const updatedAt = ref('');

onMounted(async () => {
  try {
    const response = await axios.get('https://covid19-brazil-api.now.sh/api/report/v1/brazil');
    const data = response.data.data;
    country.value = data.country;
    cases.value = data.cases;
    confirmed.value = data.confirmed;
    deaths.value = data.deaths;
    recovered.value = data.recovered;
    updatedAt.value = new Date(data.updated_at).toLocaleString();
  } catch (error) {
    console.error('Erro ao obter dados da API:', error);
  }
});
</script>
