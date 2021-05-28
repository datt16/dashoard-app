<template>
  <v-app>
    <v-container>
      <!-- <v-row class="px-4">
        <span class="ml-3 my-4 display-1 font-weight-bold">ダッシュボード</span>
      </v-row> -->

      <v-row class="px-3">
        <v-col lg="2" sm="4" md="3" cols="6" v-for="d in current" :key="d.name">
          <dataCard :dataSets="d" @clicked="showHelp" />
        </v-col>
      </v-row>

      <v-row class="px-3">
        <v-col cols="12" lg="4" md="6">
          <v-card class="px-2 py-2 rounded-lg">
            <v-row dense>
              <v-col cols="10" align-self="end" class="mt-2 mx-3">
                <span class="headline">気温の推移</span>
              </v-col>
            </v-row>
            <LineChart class="py-2" color="#2196F3" />
          </v-card>
        </v-col>

        <v-col cols="12" lg="4" md="6">
          <v-card tile class="px-2 py-2 rounded-lg">
            <v-row dense>
              <v-col cols="10" align-self="end" class="mt-2 mx-3">
                <span class="headline">水温の推移</span>
              </v-col>
            </v-row>
            <LineChart class="py-2" color="#311B92" />
          </v-card>
        </v-col>

        <v-col cols="12" lg="4" md="6">
          <v-card tile class="px-2 py-2 rounded-lg">
            <v-row dense>
              <v-col cols="10" align-self="end" class="mt-2 mx-3">
                <span class="headline">栄養塩量の推移</span>
              </v-col>
            </v-row>
            <LineChart class="py-2" color="#009688" />
          </v-card>
        </v-col>
      </v-row>

      <v-row class="px-3">
        <v-col cols="12" lg="5">
          <delta :dataSet="this.delta_dataSet" />
        </v-col>
        <v-col cols="12" lg="4">
          <acc current="200" days="10" />
        </v-col>
        <v-col cols="12" lg="1" class="mb-4"></v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
import dataCard from "./components/dashboard/dataCard";
import LineChart from "./components/dashboard/chart";
import dataSet from "./components/dashboard/dataSet";
import acc from "./components/dashboard/accTemp";
import delta from "./components/dashboard/delta";

import setting from "./components/dashboard/setting";

export default {
  name: "App",

  data: () => ({
    lastUpdate: "",
    headers: [],
    dataset: [],
    current: [],
    selected: [],
    delta_dataSet: [],
    snackbar: true,
    snack_text: "ダッシュボードでは海の情報が確認できます。",
  }),
  components: {
    LineChart,
    dataCard,
    acc,
    delta,
  },
  computed: {
    records() {
      return this.$store.getters["sakuraFunc/records"];
    },
  },
  mounted() {
    this.dataset = dataSet.records;
    this.headers = dataSet.headers;
    this.current = dataSet.current;
    this.delta_dataSet = dataSet.delta_sample;
    this.setCurrentData();
  },
  methods: {
    /** 画面右下にヘルプを表示する
     * @param {string} type 表示するテキストを選択するための識別子
     * type : components/dashboard/setting.jsonを参照
     */
    showHelp: function (type) {
      this.snack_text = setting.help[type].text;
      this.snackbar = true;
      setTimeout(() => {
        this.snackbar = false;
      }, 10000);
    },

    /** Storeから最新の観測データをcurrentに代入 */
    setCurrentData: function () {
      this.current[0].record = this.records[0].temperature;
      this.current[0].timeRatio =
        (this.records[0].temperature * 10 - this.records[1].temperature * 10) /
        10;

      this.current[1].record = this.records[0].wTemperature;
      this.current[1].timeRatio =
        (this.records[0].wTemperature * 10 -
          this.records[1].wTemperature * 10) /
        10;

      this.current[2].record = this.records[0].windSpeed;
      this.current[2].timeRatio =
        (this.records[0].windSpeed * 10 - this.records[1].windSpeed * 10) / 10;

      this.current[3].record = this.records[0].waveHeight;
      this.current[3].timeRatio =
        (this.records[0].waveHeight * 10 - this.records[1].waveHeight * 10) /
        10;

      this.current[4].record = this.records[0].nutrition;
      this.current[4].timeRatio =
        (this.records[0].nutrition * 10 - this.records[1].nutrition * 10) / 10;

      this.lastUpdate = this.records[0].date;
    },
  },
};
</script>
