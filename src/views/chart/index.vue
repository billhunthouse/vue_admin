<template>
  <div ref="chartContainer" style="width: 600px; height: 400px;"></div>
</template>
 
<script setup>
import { onMounted, ref } from 'vue';
import * as echarts from 'echarts';
 
const chartContainer = ref(null);
 
onMounted(() => {
  const chart = echarts.init(chartContainer.value);
  const option = {
    title: {
      text: 'ECharts Demo',
    },
    tooltip: {},
    xAxis: {
      data: ['A', 'B', 'C', 'D', 'E', 'F'],
    },
    yAxis: {},
    series: [
      {
        name: '数量',
        type: 'bar',
        data: [5, 20, 36, 10, 10, 20],
      },
    ],
  };
 
  chart.setOption(option);
});
</script>
 
<style>
/* 你的样式 */
</style>