<template>
  <div class="relative w-full h-full globe-container" style="background-image: url('//unpkg.com/three-globe/example/img/night-sky.png');">
    <div id="globeViz"></div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';

import Globe from 'globe.gl';

onMounted(() => {
  fetch('/dados.json', { mode: 'no-cors' })
    .then(res => res.json())
    .then(places => {
      const globe = Globe()
        .globeImageUrl('//unpkg.com/three-globe/example/img/earth-night.jpg')
        .backgroundImageUrl('//unpkg.com/three-globe/example/img/night-sky.png')
        .labelsData(places.features)
        .labelLat(d => d.properties.latitude)
        .labelLng(d => d.properties.longitude)
        .labelText(d => d.properties.name)
        .labelSize(d => Math.sqrt(d.properties.pop_max) * 4e-4)
        .labelDotRadius(d => Math.sqrt(d.properties.pop_max) * 4e-4)
        .labelColor(() => 'rgba(255, 165, 0, 0.75)')
        .labelResolution(2);

      globe(document.getElementById('globeViz'));
    }).catch((error) => {
      console.error("Falhou: ", error);
    });
});
</script>

<style scoped>
/* Ajuste o tamanho do globo */
#globeViz {
  width: 100%;
  height: 100%;
  z-index: -1;
}
</style>
