  
  <script setup>
import {
  onMounted,
  ref,
} from 'vue';

import Chart from 'chart.js/auto';

const chart = ref(null);
    
    onMounted(() => {
      const ctx = chart.value.getContext('2d');
      new Chart(ctx, {
        type: 'bar',
        data: {
          labels: ['Country 1', 'Country 2', 'Country 3'], // Labels dos países
          datasets: [{
            label: 'Confirmed Cases', // Rótulo para o eixo y
            data: [1000, 2000, 3000], // Dados de casos confirmados
            backgroundColor: 'rgba(54, 162, 235, 0.2)', // Cor de fundo das barras
            borderColor: 'rgba(54, 162, 235, 1)', // Cor da borda das barras
            borderWidth: 1
          }]
        },
        options: {
          scales: {
            y: {
              beginAtZero: true
            }
          }
        }
      });
    });
    
  
</script>
    
<style scoped>
.bar-chart {
    width: 80%;
    margin: auto;
}
</style>

<template>
    <div class="bar-chart h-full w-full">
      <canvas ref="chart"></canvas>
    </div>
</template>


  