<template>
  <v-card id="card" ref="card" class="rounded-lg pb-3" min-width="100px">
    <v-container>
      <v-row dense class="d-flex justify-space-between align-center">
        <div class="d-flex align-center">
          <v-card-title>積算温度</v-card-title>
        </div>
        <span class="body mr-3">積算開始から{{ days }}日</span>
      </v-row>

      <transition name="fade">
        <v-row dense class="pl-3 d-flex align-center" v-if="this.toggle">
          <div class="gage_base">
            <div class="gage1" />
          </div>

          <div class="flex-colmn ml-10">
            <span class="body">
              <slot name="detail">現 在の積算温度</slot>
            </span>
            <div
              class="align-baseline mr-3"
              style="color: var(--current_color)"
            >
              <span class="display-3 font-weight-bold">
                <slot name="temp">{{ current }}</slot>
              </span>
              <span class="display-1 font-weight-bold">℃</span>
            </div>
          </div>
        </v-row>
      </transition>
    </v-container>
  </v-card>
</template>

<style scoped>
#card {
  --current_color: #2196f3;
}
.gage_base {
  width: 35%;
  display: flex;
  max-width: 250px;
  height: 200px;
  overflow: hidden;
  flex-wrap: wrap;
  align-items: flex-end;
  border-radius: 5px;
  border: var(--current_color) 1px solid;
}
.gage1 {
  z-index: 0;
  overflow: hidden;
  width: 100%;
  height: 45%;
  background-color: var(--current_color);
}
.fade-enter-active {
  transition: opacity 0.9s;
}
.fade-leave-active {
  transition: opacity 0.1s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>

<script>
export default {
  props: {
    current: {
      default: 1000,
    },
    days: {
      default: 1,
    },
  },
  data: () => ({ toggle: true }),
  updated() {
    let color = "#2196f3";
    if (this.current < 100) {
      color = "#01579B";
    } else if (this.current < 500) {
      color = "#2196F3";
    } else if (this.current < 800) {
      color = "#00BCD4";
    } else if (this.current < 1000) {
      color = "#8BC34A";
    } else if (this.current >= 1000) {
      color = "#FFC107";
    }
    document.querySelector("#card").style.setProperty("--current_color", color);
  },
  mounted() {
    let color = "#2196f3";
    if (this.current < 100) {
      color = "#01579B";
    } else if (this.current < 500) {
      color = "#2196F3";
    } else if (this.current < 800) {
      color = "#00BCD4";
    } else if (this.current < 1000) {
      color = "#8BC34A";
    } else if (this.current >= 1000) {
      color = "#FFC107";
    }
    document.querySelector("#card").style.setProperty("--current_color", color);
  },
  methods: {
    toggleHelp: function () {
      this.toggle = !this.toggle;
    },
  },
};
</script>
