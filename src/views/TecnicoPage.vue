<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="tertiary"></ion-menu-button>
        </ion-buttons>
        <ion-title>JPA Servers - Técnico</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" class="ion-padding">
      <ion-grid class="dashboard-grid">
        
        <ion-row class="ion-row-1">
          <ion-col size="12" size-lg="4">
            <div class="box flex-column">
              <ion-note>ESTADO DE MICROSERVICIOS</ion-note>
              <div class="status-list">
                <div v-for="service in services" :key="service.name" class="status-item">
                  <span class="dot" :class="service.status"></span>
                  <span class="service-name">{{ service.name }}</span>
                  <span class="service-ms">{{ service.latency }}ms</span>
                </div>
              </div>
            </div>
          </ion-col>

          <ion-col size="12" size-lg="4">
            <div class="box flex-column">
              <ion-note>HTTP STATUS CODES (API)</ion-note>
              <div class="chart-wrapper-js">
                <BarChart :chartData="apiData" :options="apiOptions" />
              </div>
            </div>
          </ion-col>

          <ion-col size="12" size-lg="4">
            <div class="box">
              <div class="realtime-container">
                <ion-note>USO DE CPU GLOBAL (TIEMPO REAL)</ion-note>
                <h1 class="live-number technical">{{ cpuUsage }}%</h1>
                <div class="progress-bar-container">
                  <div class="progress-fill" :style="{ width: cpuUsage + '%' }"></div>
                </div>
              </div>
            </div>
          </ion-col>
        </ion-row>

        <ion-row class="ion-row-2">
          <ion-col size="12">
            <div class="box">
              <div class="chart-wrapper-apex">
                <ion-note>LATENCIA DE RED (MS)</ion-note>
                <apexchart 
                  type="line" 
                  height="300" 
                  width="100%"
                  :options="latencyOptions" 
                  :series="latencySeries" 
                />
              </div>
            </div>
          </ion-col>
        </ion-row>

        <ion-row class="ion-row-3">
          <ion-col size="12" size-lg="5">
            <div class="box flex-column">
              <ion-note>DISTRIBUCIÓN DE RAM</ion-note>
              <div class="chart-wrapper-echarts">
                <v-chart class="chart" :option="ramOption" autoresize />
              </div>
            </div>
          </ion-col>

          <ion-col size="12" size-lg="7">
            <div class="box flex-column">
              <ion-note>LOGS DE USO DE SERVIDORES (ÚLTIMAS 6H)</ion-note>
              <div class="chart-wrapper-apex">
                <apexchart 
                  type="heatmap" 
                  height="250" 
                  width="100%"
                  :options="heatmapOptions" 
                  :series="heatmapSeries" 
                />
              </div>
            </div>
          </ion-col>
        </ion-row>

      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';
import { 
  IonButtons, IonContent, IonHeader, IonMenuButton, IonPage, 
  IonTitle, IonToolbar, IonGrid, IonRow, IonCol, IonNote 
} from '@ionic/vue';

import apexchart from 'vue3-apexcharts';

import { BarChart } from 'vue-chart-3';
import { Chart, registerables } from 'chart.js';
Chart.register(...registerables);

import VChart from "vue-echarts";
import { use } from "echarts/core";
import { CanvasRenderer } from "echarts/renderers";
import { PieChart } from "echarts/charts";
import { TooltipComponent, LegendComponent } from "echarts/components";
import { ApexOptions } from 'apexcharts';
use([CanvasRenderer, PieChart, TooltipComponent, LegendComponent]);


const services = ref([
  { name: 'Auth Server', status: 'online', latency: 12 },
  { name: 'Race Engine', status: 'online', latency: 5 },
  { name: 'Assetto API', status: 'warning', latency: 145 },
  { name: 'DB Cluster', status: 'online', latency: 8 }
]);

const cpuUsage = ref(42);
let cpuInterval: any;
onMounted(() => {
  cpuInterval = setInterval(() => {
    cpuUsage.value = Math.floor(Math.random() * (65 - 35) + 35);
  }, 2000);
});
onUnmounted(() => clearInterval(cpuInterval));

const apiData = {
  labels: ['200 OK', '404 NF', '500 ERR', '403 FRB'],
  datasets: [{
    label: 'Peticiones',
    data: [12000, 450, 120, 80],
    backgroundColor: ['#2dd36f', '#ffc409', '#eb445a', '#3dc2ff']
  }]
};
const apiOptions = { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false } } };

const latencySeries = ref([{ 
  name: 'Ping (ms)', 
  data: [30, 40, 35, 50, 49, 33, 50, 61, 43, 48, 57] 
}]);

const latencyOptions = {
  chart: { 
    id: 'latency-chart',
    toolbar: { show: false }, 
    background: 'transparent',
    foreColor: '#ccc' 
  },
  stroke: { curve: 'smooth', colors: ['#3dc2ff'], width: 3 },
  theme: { mode: 'dark' },
  grid: { borderColor: '#333' },
  xaxis: { 
    categories: ['10:00', '11:00', '12:00', '13:00', '14:00', '15:00', '16:00', '17:00', '18:00', '19:00' , '20:00'],
    axisBorder: { show: false } 
  },
  tooltip: { theme: 'dark' }
} as ApexOptions;

const ramOption = ref({
  backgroundColor: 'transparent',
  tooltip: { trigger: 'item', backgroundColor: '#1e1e1e' },
  label: {
      show: true,
      position: 'outside',
      color: '#fff',
      formatter: '{b}: {d}%'
    },
  series: [{
    type: 'pie',
    radius: ['40%', '70%'],
    data: [
      { value: 45, name: 'AC Physics' },
      { value: 20, name: 'Node.js' },
      { value: 20, name: 'SQL' },
      { value: 15, name: 'Ubuntu Server' }
    ]
  }]
});

const heatmapSeries = [
  { name: 'Servidor 1', data: [{x: '1h', y: 10}, {x: '2h', y: 20}, {x: '3h', y: 30}, {x: '4h', y: 80}, {x: '5h', y: 50}] },
  { name: 'Servidor 2', data: [{x: '1h', y: 50}, {x: '2h', y: 10}, {x: '3h', y: 60}, {x: '4h', y: 60}, {x: '5h', y: 10}] },
  { name: 'Servidor 3', data: [{x: '1h', y: 30}, {x: '2h', y: 30}, {x: '3h', y: 50}, {x: '4h', y: 90}, {x: '5h', y: 40}] }
];
const heatmapOptions = {
  chart: { 
    id: 'heatmapOptions',
    type: 'heatmap' as const,
    toolbar: { show: false },
    background: 'transparent'
  },
  dataLabels: { enabled: false },
  theme: { mode: 'dark' },
  plotOptions: {
    heatmap: {
      colorScale: {
        ranges: [
          { from: 0, to: 30, color: '#D1F2FF', name: 'Bajo' },
          { from: 31, to: 60, color: '#3dc2ff', name: 'Medio' },
          { from: 61, to: 100, color: '#004A6B', name: 'Crítico' }
        ]
      }
    }
  },
} as ApexOptions;
</script>

<style scoped>
.box {
  background: #121212;
  border: 1px solid #333;
  border-radius: 12px;
  padding: 15px;
  height: 100%;
  display: flex;
  flex-direction: column;
}

.chart-wrapper-apex {
  width: 100%;
  flex-grow: 1;
}

.status-list { width: 100%; margin-top: 10px; }
.status-item {
  display: flex;
  align-items: center;
  margin-bottom: 8px;
  background: #1e1e1e;
  padding: 8px;
  border-radius: 6px;
}
.dot { width: 8px; height: 8px; border-radius: 50%; margin-right: 12px; }
.online { background: #2dd36f; box-shadow: 0 0 5px #2dd36f; }
.warning { background: #ffc409; box-shadow: 0 0 5px #ffc409; }
.service-name { flex-grow: 1; font-size: 0.85rem; color: #fff; }
.service-ms { font-family: monospace; color: #888; font-size: 0.8rem; }

.technical { color: #3dc2ff !important; margin: 10px 0; }
.chart-wrapper-echarts, .chart-wrapper-js { width: 100%; height: 230px; }

.progress-bar-container {
  width: 100%;
  height: 8px;
  background: #333;
  border-radius: 4px;
  margin-top: 15px;
  overflow: hidden;
}
.progress-fill { height: 100%; background: #3dc2ff; transition: width 0.5s ease; }

@media (min-width: 992px) {
  .ion-row-1 { height: 28%; }
  .ion-row-2 { height: 35%; }
  .ion-row-3 { height: 37%; }
}
</style>