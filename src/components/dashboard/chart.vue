<template>
  <div class="small">
    <line-chart
      id="chart"
      :height="200"
      :chart-data="datacollection"
      :options="options"
    ></line-chart>
    <!-- <button @click="fillData()">Randomize</button> -->
  </div>
</template>

<script>
import LineChart from "../../plugins/LineChart";
import Chart from "chart.js";

Chart.defaults.global.defaultFontColor = "#AAA";

export default {
  props: {
    color: {
      type: String,
      default: "",
    },
  },
  components: {
    LineChart,
  },
  data() {
    return {
      datacollection: null,
      options: null,
    };
  },
  created() {
    this.fillData();
  },
  // mode1 [0:00, 1:00, 2:00, 3:00, ...]
  // mode2 []
  methods: {
    // genChartColor : Genarete Chart Color [HEX] -> [RGBA]
    genChartColor(Code, Type) {
      if (Code == "") {
        return "#0288D1";
      }
      if (Type == "back") {
        const red = parseInt(Code.substring(1, 3), 16);
        const green = parseInt(Code.substring(3, 5), 16);
        const blue = parseInt(Code.substring(5, 7), 16);
        return `RGBA(${red},${green},${blue},0.2)`;
      } else if (Type == "border") {
        const red = parseInt(Code.substring(1, 3), 16);
        const green = parseInt(Code.substring(3, 5), 16);
        const blue = parseInt(Code.substring(5, 7), 16);
        return `RGBA(${red},${green},${blue},1)`;
      }
      return "";
    },
    fillData() {
      (this.datacollection = {
        labels: this.createLabel(12),
        datasets: [
          {
            label: "水温",
            data: this.createArray(12),
            backgroundColor: this.genChartColor(this.color, "back"),
            borderColor: this.genChartColor(this.color, "border"),
            lineTension: 0,
            fill: true,
          },
        ],
      }),
        (this.options = {
          responsive: true,
          scales: {
            xAxes: [
              {
                // gridLines: {
                //   color: baseColor,
                // },
              },
            ],
            yAxes: [
              {
                // gridLines: {
                //   color: baseColor,
                // },
                ticks: {
                  suggestedMin: 0,
                  suggestedMax: 50,
                  stepSize: 10,
                },
              },
            ],
          },
          legend: {
            display: false,
          },
        });
    },
    getRandomInt() {
      return Math.floor(Math.random() * (40 - 5 + 1)) + 5;
    },
    createArray(n) {
      const list = [];
      for (let i = 0; i < n; i++) {
        const num = Math.floor(Math.random() * (40 - 5 + 1)) + 5;
        list.push(num);
      }
      return list;
    },
    createLabel(n) {
      const list = [];
      for (let i = 0; i < 24; i += 24 / n) {
        const label = i.toString() + ":00";
        list.push(label);
      }
      return list;
    },
  },
};
</script>

<style>
.small {
  margin: 5px auto;
}
</style>
