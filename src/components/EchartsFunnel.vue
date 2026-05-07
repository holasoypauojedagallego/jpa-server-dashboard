<template>
    <v-chart class="chart" :option="option" autoresize />
  </template>
  
  <script setup lang="ts">
  import { use } from 'echarts/core';
  import { CanvasRenderer } from 'echarts/renderers';
  import { FunnelChart } from 'echarts/charts';
  import { TitleComponent, TooltipComponent, LegendComponent } from 'echarts/components';
  import VChart from 'vue-echarts';
  import { ref } from 'vue';
  
  use([CanvasRenderer, FunnelChart, TitleComponent, TooltipComponent, LegendComponent]);
  
  const option = ref({
    backgroundColor: 'transparent',
    tooltip: {
      trigger: 'item',
      formatter: '{b} : {c}%'
    },
    series: [
      {
        name: 'Conversión de Usuarios',
        type: 'funnel',
        left: '10%',
        top: 10,
        bottom: 10,
        width: '80%',
        min: 0,
        max: 100,
        minSize: '0%',
        maxSize: '100%',
        sort: 'descending',
        gap: 2,
        label: {
          show: true,
          position: 'inside',
          color: '#fff',
          fontSize: 12
        },
        itemStyle: {
          borderColor: '#1e1e1e',
          borderWidth: 1
        },
        emphasis: {
          label: { fontSize: 16 }
        },
        data: [
          { value: 100, name: 'Visitas Web' },
          { value: 75, name: 'Configura Server' },
          { value: 40, name: 'Registro' },
          { value: 20, name: 'Server Lanzado' }
        ]
      }
    ]
  });
  </script>
  
  <style scoped>
  .chart {
    height: 250px;
    width: 100%;
  }
  </style>