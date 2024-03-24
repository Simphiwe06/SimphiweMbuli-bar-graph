<template>
  <div class="bar-graph-wrapper">
    <h2 class="graph-title">Installation Trends Over Months</h2>
    <p class="graph-description"><strong>Visual representation of software installations over different months.</strong></p>

    <div class="bar-graph-container">
      <div class="axes">
        <!-- Bars -->
        <div class="bar-graph">
          <div
            v-for="(item, index) in data"
            :key="index"
            class="bar"
            @mouseover="showCount(item)"
            @mouseleave="hideCount"
          >
            <div
              class="bar-fill"
              :style="{ height: item.numInstalls * 3 + 'px', backgroundColor: barColors[index] }"
            ></div>
            <span class="bar-label"><strong>{{ item.month }}</strong></span>
            <span class="bar-count" v-if="showBarCount && activeBarIndex === index"><strong>{{ item.numInstalls }}</strong></span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['data'],
  data() {
    return {
      showBarCount: false,
      activeBarIndex: null,
      barColors: ['#FF6384', '#36A2EB', '#FFCE56', '#4BC0C0', '#9966FF', '#F670A0', '#68B3C8', '#FDD835'], // Update with more colors if needed
    };
  },
  methods: {
    showCount(item) {
      this.showBarCount = true;
      this.activeBarIndex = this.data.findIndex(bar => bar.month === item.month);
    },
    hideCount() {
      this.showBarCount = false;
      this.activeBarIndex = null;
    },
  },
};
</script>

<style scoped src="./BarGraph.css"></style>
