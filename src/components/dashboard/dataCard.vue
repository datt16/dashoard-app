<template>
  <v-card elevation="2" @click="click()" class="px-4 py-1 pb-4 rounded-lg">
    <div>
      <v-row no-gutters class="d-flex">
        <v-col>
          <v-row no-gutters class="d-flex">
            <span
              class="font-weight-light grey--text"
              style="font-size: 0.79rem"
            >
              {{ dataSets.name }}
            </span>
          </v-row>
          <v-row no-gutters class="d-flex">
            <span class="font-weight-bold" style="font-size: 2.3rem">
              {{ dataSets.record }}
            </span>
            <span class="display-1 font-weight-bold">{{ dataSets.type }}</span>
          </v-row>
        </v-col>
        <v-icon size="36pt" class="ml-auto mt-2" color="blue accent-2">
          {{ dataSets.icon }}
        </v-icon>
      </v-row>
      <v-divider class="mt-4" />
      <v-row no-gutters class="mt-1">
        <span class="caption grey--text text--accent-2">時間比 &nbsp;</span>
        <span class="caption orange--text text--accent-3"></span>
        <span class="caption orange--text text--accent-3"
          >&nbsp;{{ dataSets.timeRatio }}</span
        >
        <span class="caption orange--text text--accent-3"></span>
      </v-row>
    </div>
  </v-card>
</template>

<script>
export default {
  props: {
    dataSets: {
      default: () => [],
    },
  },
  data: function () {
    return {
      id: this.dataSets.id,
    };
  },
  methods: {
    click() {
      this.$emit("clicked", this.id);
    },
  },
};
</script>

<style scoped>
.subText {
  color: rgba(0, 0, 0, 0.3);
}
</style>
