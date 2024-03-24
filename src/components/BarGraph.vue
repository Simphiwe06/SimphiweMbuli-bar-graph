<template>
    <div class="bar-graph-container">
      <h2 class="graph-title">Installation Trends Over Months</h2>
      <p class="graph-description"><strong>Visual representation of software installations over different months.</strong></p>
  
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
  
  <style scoped>
  .bar-graph-container {
    text-align: center;
    padding: 40px 20px;
    margin-bottom: 40px; /* Added margin at the bottom */
  }
  
  .graph-title {
    font-size: 30px;
    font-weight: bold;
    margin-bottom: 20px;
  }
  
  .graph-description {
    font-size: 20px;
    color: #666;
    margin-bottom: 20px;
  }
  
  .axes {
    display: flex;
    align-items: flex-end;
    position: relative;
  }
  
  .bar-graph {
    display: flex;
    justify-content: space-around;
    align-items: flex-end;
    width: calc(100% - 90px); /* Adjust for padding */
    margin: 0 auto;
  }
  
  .bar {
    position: relative;
    flex-grow: 1;
  }
  
  .bar-fill {
    width: 70%;
    margin: 0 auto;
    margin-bottom: 5px;
    transition: height 0.5s ease-in-out;
  }
  
  .bar-label {
    font-size: 14px;
  }
  
  .bar-count {
    position: absolute;
    top: -20px; /* Adjust for better visibility */
    left: 50%;
    transform: translateX(-50%);
    font-size: 14px;
    font-weight: bold;
    color: #333;
    display: none;
  }
  
  .bar:hover .bar-count {
    display: block;
  }
  </style>
  