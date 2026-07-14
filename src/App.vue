<script setup>
import { ref } from 'vue';
import { charts } from "./examples.js";
import CodeViewer from './CodeViewer.vue';

const viewingOptions = ref(null);

const setViewingOptions = (options) => {
  viewingOptions.value = options;
};
</script>

<template>
  <div class="vjs-scatter-bubble-chart">
    <div v-for="(chart, index) in charts" :key="index" class="vjs-chart-example">
      <div class="vjs-chart-header">
        <div class="vjs-chart-example-title">{{ chart.desc }}</div>
        <button class="show-code-btn" @click="setViewingOptions(chart.options)">
          Show me the code
        </button>
      </div>
      <div v-if="chart.comments" class="vjs-chart-example-comments">{{ chart.comments }}</div>
      <component :is="chart.component" class="vjs-chart-example-container" :options="chart.options" />
    </div>
    <CodeViewer
        v-if="viewingOptions"
        :options="viewingOptions"
        @close="setViewingOptions(null)"
    />
  </div>
</template>

