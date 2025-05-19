<script>
  import PlotlyCharts from "./components/PlotlyCharts.vue";
  import Echarts from "./components/Echarts.vue";
  import { getCoordinates } from "./Store/index.js";

  export default {
    name: 'Chart',
    components: {Echarts, PlotlyCharts},
    created() {
      getCoordinates();
    }
  }
</script>

<template>
  <PlotlyCharts/>
<!--  <Echarts/>-->
</template>

<style scoped>

</style>
