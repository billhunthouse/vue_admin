<template>
  <div ref="chartContainer" style="width: 600px; height: 400px;"></div>
</template>
 
<script setup>
import { onMounted, ref } from 'vue';
import * as echarts from 'echarts';
import axios from 'axios';

 
const chartContainer = ref(null);
 
onMounted(async () => {
  try {
    const response = await axios.get('http://127.0.0.1:8000/api/report', { withCredentials: true });
    const data = response.data;
    console.log(data);

    const chart = echarts.init(chartContainer.value);
    const option = {
      title: {
        text: '最近运行报告',
      },
      tooltip: {},
      xAxis: {
        data: ['passed', 'failed', 'broken', 'skipped', 'unknown', 'total'],
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
  } catch (error) {
    console.error(error);
  }
});

</script>
 
<style>
/* 你的样式 */
</style>