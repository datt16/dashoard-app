<template>
  <div class="deltaCard">
    <v-card color="white" max-height="300px">
      <v-card-title style="padding-bottom: 0px"
        >最高・最低・平均値
      </v-card-title>
      <span class="d-flex body"></span>
      <v-row class="mx-1">
        <v-col>
          <v-slide-group multiple show-arrows>
            <v-slide-item
              style="text-align: center"
              v-for="dt in dataSet"
              :key="dt.name"
            >
              <div class="ma-4" color="white">
                <p class="display-1 red--text text--accent-5">
                  {{ dt.max }}
                  <span style="font-size: 0.5em">{{ dt.type }}</span>
                </p>
                <p class="display-1">
                  {{ dt.avg }}
                  <span style="font-size: 0.5em">{{ dt.type }}</span>
                </p>
                <p class="display-1 blue--text">
                  {{ dt.min }}
                  <span style="font-size: 0.5em">{{ dt.type }}</span>
                </p>
                <p class="body" style="text-align: center; margin-bottom: 0px">
                  {{ dt.displayName }}
                </p>
              </div>
            </v-slide-item>
          </v-slide-group>
        </v-col>
      </v-row>
    </v-card>
  </div>
</template>

<style>
.side {
  margin-top: 2.4em;
}
</style>

<script>
export default {
  props: {
    dataSet: {
      type: Array,
      default: () => [
        {
          name: "sample",
          displayName: "サンプル",
          type: "℃",
          max: 0,
          min: 30.5,
          avg: 0,
        },
      ],
    },
  },
};
</script>
