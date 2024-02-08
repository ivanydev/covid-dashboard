<template>
  <div class="flex flex-col items-center w-full h-full bg-gradient-to-b from-dark-50">
    <div class="w-full h-full">
      <canvas ref="chart"></canvas>
    </div>
    
    <button class="px-4 text-sm bg-blue-800 rounded btn border-t-neutral-500" @click="loadMore">Ver mais</button>
  </div>
</template>

<script setup>
import {
  onMounted,
  ref,
} from 'vue';

import axios from 'axios';
import Chart from 'chart.js/auto';

const chart = ref(null);
let countriesData = []; // Armazenar todos os dados dos países
let currentPage = 0;
const pageSize = 10;
let myChart = null;

onMounted(async () => {
  await loadCountriesData();
  renderChart();
});

async function loadCountriesData() {
  const response = await axios.get('https://covid19-brazil-api.now.sh/api/report/v1/countries');
  countriesData = response.data.data; // Extrair a matriz de países da resposta da API
}

function renderChart() {
  const countries = getCountriesForCurrentPage();
  const labels = countries.map(country => country.country);
  const confirmedCases = countries.map(country => country.confirmed);

  if (myChart) {
    myChart.destroy(); // Destruir o gráfico existente
  }

  const ctx = chart.value.getContext('2d');
  myChart = new Chart(ctx, {
    type: 'bar',
    data: {
      labels: labels,
      datasets: [{
        label: 'Confirmed Cases',
        data: confirmedCases,
        backgroundColor: 'rgba(54, 162, 235, 0.2)',
        borderColor: 'rgba(54, 162, 235, 1)',
        borderWidth: 1,
      }]
    },
    options: {
      indexAxis: 'y',
      scales: {
        x: {
          beginAtZero: true
        }
      },
      layout: {
        padding: {
          left: 20, // Ajuste o espaçamento esquerdo conforme necessário
          right: 20, // Ajuste o espaçamento direito conforme necessário
          top: 20, // Ajuste o espaçamento superior conforme necessário
          bottom: 20 // Ajuste o espaçamento inferior conforme necessário
        }
      }
    }
  });
}

function getCountriesForCurrentPage() {
  const startIndex = currentPage * pageSize;
  const endIndex = startIndex + pageSize;
  return countriesData.slice(startIndex, endIndex);
}

function loadMore() {
  currentPage++;
  renderChart();
}
</script>

<style scoped>
canvas {
  width: 100% !important;
  height:100%!important;
  display: block;
}
</style>
