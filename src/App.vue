<template>
  <v-app>
    <div class="pa-4">
      <v-row class="px-4">
        <span class="ml-3 my-4 display-1 font-weight-bold">ダッシュボード</span>
      </v-row>

      <v-row class="px-3">
        <v-col lg="2" sm="4" md="3" cols="6" v-for="d in current" :key="d.name">
          <dataCard :dataSets="d" />
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
        <v-col cols="12" lg="1" class="mb-4"></v-col>
      </v-row>
    </div>
  </v-app>
</template>

<script>
import dataCard from "./components/dashboard/dataCard";
import LineChart from "./components/dashboard/chart";
import dataSet from "./components/dashboard/dataSet";
import delta from "./components/dashboard/delta";

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
  },
};
</script>
