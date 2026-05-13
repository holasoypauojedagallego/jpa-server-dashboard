<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>JPA Servers - Negocio</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" class="ion-padding">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">🚀 Negocio</ion-title>
        </ion-toolbar>
      </ion-header>

      <!-- Grid principal del Dashboard -->
      <ion-grid class="dashboard-grid">
        

        <!-- 🟢 Fila 1: KPIs Rápidos (Propio y Tiempo Real) -->
        <ion-row class="ion-row-1">
          <ion-col size="12" size-lg="6">
            <div class="box">
              <ion-note>RANKING DE COCHES MÁS USADOS</ion-note>
              <TopModsRanking />
            </div>
          </ion-col>

          <ion-col size="12" size-lg="6">
            <div class="box">
              <!-- KPI Tiempo Real: Pilotos -->
              <div class="realtime-container">
                <ion-note>PILOTOS CONECTADOS (LIVE)</ion-note>
                <h1 class="live-number">{{ livePilots }}</h1>
                <div class="pulse-wrapper">
                  <div class="pulse-dot"></div>
                  <span>Actualizando ahora</span>
                </div>
              </div>
            </div>
          </ion-col>
        </ion-row>

        <!-- 🔵 Fila 2: Análisis (Chart.js y ApexCharts) -->
        <ion-row class="ion-row-2">
          <!-- Columna Pequeña: Chart.js (Circuitos) -->
          <ion-col size="12" size-lg="4">
            <div class="box flex-column">
              <ion-note style="margin-bottom: 10px;">CIRCUITOS POPULARES</ion-note>
              <div class="chart-wrapper-js">
                <DoughnutChart :chartData="circuitsData" :options="circuitsOptions" />
              </div>
            </div>
          </ion-col>

          <!-- COLUMNA GRANDE: ApexCharts (Uso de infraestructura) -->
          <ion-col size="12" size-lg="8">
            <div class="box">
              <div class="chart-wrapper-apex">
                <ion-note>SERVIDORES EN USO VS CAPACIDAD</ion-note>
                <ApexMixedChart :series="serverUsageSeries" />
              </div>
            </div>
          </ion-col>
        </ion-row>

        <!-- 🟠 Fila 3: Estrategia (ECharts y Sparkline) -->
        <ion-row class="ion-row-3">
          <ion-col size="12" size-lg="4">
            <div class="box">
              <spark-line v-bind="sparkData1"/>
            </div>
          </ion-col>

          <ion-col size="12" size-lg="8">
            <div class="box flex-column">
              <ion-note>EMBUDO DE CONVERSIÓN (VENTAS)</ion-note>
              <EchartsFunnel />
            </div>
          </ion-col>
        </ion-row>

      </ion-grid>
    </ion-content>
  </ion-page>
</template>


<script setup lang="ts">
import {
  IonButtons, IonContent, IonHeader, IonMenuButton, IonPage,
  IonTitle, IonToolbar, IonGrid, IonRow, IonCol, IonNote
} from '@ionic/vue'
import { ref, onMounted, onUnmounted } from 'vue'

// Importación de Librerías de Gráficos
import { DoughnutChart } from 'vue-chart-3'
import { Chart, registerables } from 'chart.js'
import ApexMixedChart from '@/components/ApexMixedChart.vue'
import SparkLine from '@/components/SparkLine.vue'
import EchartsFunnel from '@/components/EchartsFunnel.vue'
import TopModsRanking from '@/components/TopModsRanking.vue'

Chart.register(...registerables)

// --- 1. Lógica de Tiempo Real ---
const livePilots = ref(55)
let interval: any
onMounted(() => {
  interval = setInterval(() => {
    livePilots.value += Math.floor(Math.random() * 5) - 2
  }, 3000)
})
onUnmounted(() => clearInterval(interval))

// --- 2. Datos ApexCharts (Servidores JPA) ---
const serverUsageSeries = ref([
  {
    name: 'Servidores Activos',
    type: 'area',
    data: [10, 15, 12, 22, 25, 28, 24]
  },
  {
    name: 'Capacidad Máxima',
    type: 'line',
    data: [30, 30, 30, 30, 30, 30, 30]
  }
])

// --- 3. Datos Chart.js (Circuitos) ---
const circuitsData = {
  labels: ['Monza', 'Spa', 'Nordschleife', 'Otros'],
  datasets: [{
    data: [45, 25, 20, 10],
    backgroundColor: [
      '#eb445a', 
      '#9c1c2c',  
      '#333333', 
      '#666666'  
    ],
    borderWidth: 0
  }]
}
const circuitsOptions = {
  responsive: true,
  maintainAspectRatio: false,
  plugins: { legend: { position: 'bottom' as const, labels: { color: '#fff' } } }
}

// --- 4. Datos Sparkline ---
const sparkData1 = ref({
  /* Propiedades del componente */
  title: "Usuarios registrados",
  value: "333",
  bgColor: "gradient-purple",
  textColor: "white",
  iconName: "navigate-outline",
  /* Propiedades del componentes interno de ApexChart */
  chartOptions: {
    chart: {
      id: 'clicks',
      type: 'area',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'smooth', width: 3 },
    colors: ['#af86ff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [25, 66, 41, 59, 25, 44, 12, 36, 9, 21] }],
});
</script>


<style scoped>
/* Grid y Layout */
ion-row { overflow: hidden; }
ion-col { --ion-grid-column-padding: 10px; }

.dashboard-grid { height: 100%; }

.box {
  background: #1E1E1E;
  height: 100%;
  width: 100%;
  border-radius: 8px;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  box-sizing: border-box;
}

.flex-column { flex-direction: column; align-items: flex-start; }

/* Contenedores específicos para que los gráficos no se desborden */
.chart-wrapper-js, .chart-wrapper-apex {
  width: 100%;
  height: 100%;
}

/* Estilos Tiempo Real */
.realtime-container { text-align: center; color: black; }
.live-number { font-size: 3.5rem; margin: 10px 0; color: #2dd36f; font-weight: 800; }
.pulse-wrapper { display: flex; align-items: center; justify-content: center; gap: 8px; font-size: 0.8rem; color: #888; }
.pulse-dot { width: 8px; height: 8px; background: #2dd36f; border-radius: 50%; animation: pulse 1.5s infinite; }

@keyframes pulse {
  0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(45, 211, 111, 0.7); }
  70% { transform: scale(1); box-shadow: 0 0 0 10px rgba(45, 211, 111, 0); }
  100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(45, 211, 111, 0); }
}

/* Layout responsive desktop */
@media (min-width: 992px) {
  .ion-row-1 { height: 25%; }
  .ion-row-2 { height: 40%; }
  .ion-row-3 { height: 35%; }
}
</style>