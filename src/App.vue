<template>
  <div class="bg-dark-400">
    <TopBar/>
    <Grafico />
  </div>
</template>

<script>
import Grafico from './components/Grafico.vue';
import TopBar from './components/TopBar.vue';

export default {
  components: {
    Grafico,
    TopBar
},
};
</script>
