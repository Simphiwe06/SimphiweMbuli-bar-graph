<template>
  <div id="app">
    <BarGraph :data="chartData" />
  </div>
</template>

<script>
import BarGraph from './components/BarGraph.vue';
import barGraphData from '../public/barGraph.json';

export default {
  name: 'App',
  components: {
    BarGraph
  },
  data() {
    return {
      chartData: barGraphData
    };
  }
};
</script>

<style>
/* Add global styles here if needed */
</style>
