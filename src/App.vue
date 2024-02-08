<template>
  <div class="relative h-full overflow-hidden">

    <div class="w-full bg-light-100">
      <TopBar/>
    </div>

    <div class="relative w-full overflow-hidden h-[100vh] ">
      <div class="absolute inset-0 z-10">
        <Globo/>
      </div>
      <div class="absolute top-0 bottom-0 left-0 z-20 hidden w-1/4 sm:flex">
        <SideCasos/>
      </div>
      <div class="absolute w-full sm:w-1/3 right-0 bottom-[12%]  z-20  h-[45%] ">
        <SidePaisesCasosNovos/>
      </div>
    </div>

  </div>
</template>

<script>
import Globo from './components/Globo.vue';
import SideCasos from './components/SideCasos.vue';
import SidePaisesCasosNovos from './components/SidePaisesCasosNovos.vue';
import TopBar from './components/TopBar.vue';

export default {
  components: {
    Globo,
    TopBar,
    SidePaisesCasosNovos,
    SideCasos
},
};
</script>
