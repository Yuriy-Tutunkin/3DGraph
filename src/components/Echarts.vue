<script>
import * as echarts from 'echarts';
import 'echarts-gl';

export default {
  name: "Echarts",
  data: () => ({
    chartInstance: null,


    option: {
      tooltip: {},
      backgroundColor: '#fff',
      xAxis3D: {
        type: 'value',
        name: 'X (m)'
      },
      yAxis3D: {
        type: 'value',
        name: 'Y (m)'
      },
      zAxis3D: {
        type: 'value',
        name: 'Глубина (m)'
      },
      grid3D: {
        viewControl: {
          projection: 'perspective',
        },
        boxWidth: 150,
        boxDepth: 150,
        boxHeight: 150,
      },
      series: [
        {
          type: 'line3D',
          data: [
            [0, 0, 0],
            [2, 1, -100],
            [5, 3, -300],
            [9, 7, -600],
            [12, 10, -1000],
          ],
          lineStyle: {
            width: 4,
            color: '#0077ff',
          },
        },
      ],
    }
  }),

  mounted() {
    this.chartInstance = echarts.init(this.$refs.chart);
    this.chartInstance.setOption(this.option);
  },
  beforeUnmount() {
    if (this.chartInstance) {
      this.chartInstance.dispose();
    }
  },
}
</script>

<template>
  <div ref="chart" style="width: 800px; height: 800px">

  </div>
</template>

<style scoped>

</style>
