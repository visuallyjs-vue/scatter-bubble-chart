<script setup>
import { charts } from "./examples.js";
</script>

<template>
  <div class="vjs-scatter-bubble-chart">
    <div v-for="(chart, index) in charts" :key="index" class="vjs-chart-example">
      <div class="vjs-chart-example-title">{{ chart.desc }}</div>
      <div v-if="chart.comments" class="vjs-chart-example-comments">{{ chart.comments }}</div>
      <component :is="chart.component" class="vjs-chart-example-container" :options="chart.options" />
    </div>
  </div>
</template>

