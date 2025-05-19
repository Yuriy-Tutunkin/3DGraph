<script>
import Plotly from "plotly.js-dist";
import { state } from "../Store/index.js";

/*export default {
  name: "PlotlyCharts",
  data: () => ({
    dataset: [
      {
        type: 'scatter3d',
        mode: 'lines+markers',
        x: [0, 10, 20], // восток-запад
        y: [0, -5, -10], // север-юг
        z: [0, 100, 200], // глубина
        line: { color: 'cyan', width: 4 },
        marker: { color: 'white', size: 4 }
      }
    ],

    layout: {
      // paper_bgcolor: 'gray',
      scene: {
        // aspectmode: 'data',
        bgcolor: 'gray',
        xaxis: {
          title: 'X (Запад-Восток)',
          showgrid: true,
          zeroline: true,
          color: 'blue',
        },
        yaxis: {
          title: 'Y (Север-Юг)',
          showgrid: true,
          zeroline: true,
          color: 'red',
        },
        zaxis: {
          title: 'Z (Глубина)',
          showgrid: true,
          zeroline: true,
          autorange: false,
          range: [300, 0], // Глубина от 0 вниз
          color: 'green',
        },
        camera: {
          eye: { x: 1.5, y: 1.5, z: 1.5 },
          up: { x: 0, y: 0, z: 1 }
        },
      },
    },
  }),

  mounted() {
    Plotly.newPlot(this.$refs.chart, this.dataset, this.layout);
  },
}*/

export default {
  name: "PlotlyCharts",
  data: () => {
    return ({


      layout: {
        paper_bgcolor: 'gray',
        scene: {
          bgcolor: 'gray',

          xaxis: {
            title: 'X',
            showgrid: true,
            // color: 'white',
            zeroline: false
          },
          yaxis: {
            title: 'Y',
            showgrid: true,
            // color: 'white',
            zeroline: false
          },
          zaxis: {
            title: 'Глубина (м)',
            autorange: false,
            // gridcolor: 'lime',
            // linecolor: 'lime',
            range: [10000, 0], // ось Z сверху вниз
            // color: 'white',
            showgrid: true,
            zeroline: false
          },

          // aspectmode: 'data',
          camera: {
            eye: {x: 1.5, y: 1.5, z: 1.5},
            up: {x: 0, y: 0, z: 1}
          }
        },
        margin: {l: 0, r: 0, b: 0, t: 30},
        title: {
          text: 'Профиль инклинометрии',
          font: {color: 'white'}
        }
      },

      annotations: [
        {
          type: 'scatter3d',
          mode: 'text',
          x: [50],
          y: [0],
          z: [0],
          text: ['В'],
          textfont: {
            color: 'yellow',
            size: 14
          },
          showlegend: false,
          hoverinfo: 'skip'
        },
        {
          type: 'scatter3d',
          mode: 'text',
          x: [-50],
          y: [0],
          z: [0],
          text: ['З'],
          textfont: {
            color: 'yellow',
            size: 14
          },
          showlegend: false,
          hoverinfo: 'skip'
        },
        {
          type: 'scatter3d',
          mode: 'text',
          x: [0],
          y: [50],
          z: [0],
          text: ['С'],
          textfont: {
            color: 'yellow',
            size: 14
          },
          showlegend: false,
          hoverinfo: 'skip'
        },
        {
          type: 'scatter3d',
          mode: 'text',
          x: [0],
          y: [-50],
          z: [0],
          text: ['Ю'],
          textfont: {
            color: 'yellow',
            size: 14
          },
          showlegend: false,
          hoverinfo: 'skip'
        }
      ],
    });
  },

  methods: {
    generateGrid(gridSize = 50, gridStep = 10) {
      const lines = [];

      for (let i = -gridSize; i <= gridSize; i += gridStep) {
        // Линии по X
        lines.push({
          type: 'scatter3d',
          mode: 'lines',
          opacity: 0.8,
          x: [-gridSize, gridSize],
          y: [i, i],
          z: [0, 0],
          line: { color: 'lime', width: 1 },
          showlegend: false,
          hoverinfo: 'skip'
        });

        // Линии по Y
        lines.push({
          type: 'scatter3d',
          mode: 'lines',
          x: [i, i],
          y: [-gridSize, gridSize],
          z: [0, 0],
          line: { color: 'lime', width: 1 },
          showlegend: false,
          hoverinfo: 'skip'
        });
      }

      return lines;
    },

    plotIncline() {
      const dataset = {
        type: 'scatter3d',
            mode: 'lines+markers',
            x: state.x,
            y: state.y,
            z: state.z,
            line: {
          color: 'cyan',
              width: 4
        },
        marker: {
          size: 4,
              color: 'white'
        },
        name: 'Скважина',
      }

      const gridLines = this.generateGrid(50, 10);
      Plotly.newPlot(this.$refs.chart, [dataset, ...gridLines,  ...this.annotations], this.layout);
    }
  },

  beforeCreate() {
    console.log(state)

  },
  mounted() {
    this.plotIncline();
  },
};
</script>

<template>
  <div ref="chart" style="width: 800px; height: 800px">

  </div>
</template>

<style scoped>

</style>
