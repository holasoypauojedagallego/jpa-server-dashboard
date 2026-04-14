<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>🚀 Negocio</ion-title>
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

        <!-- 🟢 Fila 1 -->
        <ion-row class="ion-row-1">
          <ion-col size="6" size-lg="6">
            <div class="box">
              <div class="box">Columna 1</div>
            </div>
          </ion-col>

          <ion-col size="6" size-lg="6">
            <div class="box">Columna 2</div>
          </ion-col>
        </ion-row>

        <!-- 🔵 Fila 2 -->
        <ion-row class="ion-row-2">

          <ion-col size="12" size-lg="3">
            <div class="box">Columna Pequeña</div>
          </ion-col>

          <!-- COLUMNA GRANDE -->
          <ion-col size="12" size-lg="9">
            <div class="box">
              <ApexMixedChart :series="dataMixedChartSeries" />
            </div>
          </ion-col>

        </ion-row>

        <!-- 🟠 Fila 3 -->
        <ion-row class="ion-row-3">

          <ion-col size="12" size-lg="4">
            <div class="box">Columna 1</div>
          </ion-col>

          <ion-col size="12" size-lg="4">
            <div class="box">Columna 2</div>
          </ion-col>

          <ion-col size="12" size-lg="4">
            <div class="box">Columna 3</div>
          </ion-col>

        </ion-row>

      </ion-grid>
    </ion-content>
  </ion-page>
</template>


<script setup lang="ts">

import {
IonButtons,
IonContent,
IonHeader,
IonMenuButton,
IonPage,
IonTitle,
IonToolbar,
IonGrid,
IonRow,
IonCol
} from '@ionic/vue'

import { ref } from 'vue'

/* Importamos el gráfico */
import ApexMixedChart from '@/components/ApexMixedChart.vue'


/* Datos del gráfico */
const dataMixedChartSeries = ref([
{
  name: 'Column',
  type: 'column',
  data: [23, 11, 22, 27, 13, 22, 37, 21, 44, 22, 30]
},
{
  name: 'Area',
  type: 'area',
  data: [44, 55, 41, 67, 22, 43, 21, 41, 56, 27, 43]
},
{
  name: 'Line',
  type: 'line',
  data: [30, 25, 36, 30, 45, 35, 64, 52, 59, 36, 39]
}
])

</script>


<style scoped>

ion-row{
overflow: hidden;
}

ion-col {
max-height: 100%;
--ion-grid-column-padding:10px;
}

/* Caja de cada columna */
.box {
background: #1E1E1E;
height: 100%;
max-height: 100%;
overflow: hidden;
border-radius:5px;
display: flex;
justify-content: center;
align-items: start;
}

/* Layout responsive */
@media (min-width: 992px) {

ion-grid{
height: 100%;
}

.ion-row-1{
height: 20%;
max-height: 20%;
}

.ion-row-2{
height: 40%;
max-height: 40%;
}

.ion-row-3{
height: 40%;
max-height: 40%;
}

}

</style>