<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>🎯 KPIs</ion-title>
      </ion-toolbar>
    </ion-header>


    <ion-content :fullscreen="true" class="ion-padding">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">🎯 KPIs</ion-title>
        </ion-toolbar>
      </ion-header>


      <h1 class="ion-padding">🚀 KPIs de Negocio</h1>
      <ion-accordion-group expand="inset" :multiple="true">
        <ion-accordion v-for="item in smartGoalsNegocio" :key="item.id" :value="item.id.toString()">
          <ion-item slot="header">
            <ion-label>{{ item.id }}. {{ item.title }}</ion-label>
          </ion-item>
          <div class="ion-padding" slot="content">
            <p>{{ item.description }}</p>
            <ion-list :inset="true">
              <ion-item v-for="(element, index) in item.smart" :key="index">
                <ion-label><b>{{ element.letter }}</b> → {{ element.content }}</ion-label>
              </ion-item>
            </ion-list>
          </div>
        </ion-accordion>
      </ion-accordion-group>
      <br>
      <h1 class="ion-padding">📈 KPIs Técnicos</h1>
      <ion-accordion-group expand="inset" :multiple="true">
        <ion-accordion v-for="item in smartGoalsTecnico" :key="item.id" :value="item.id.toString()">
          <ion-item slot="header">
            <ion-label>{{ item.id }}. {{ item.title }}</ion-label>
          </ion-item>
          <div class="ion-padding" slot="content">
            <p>{{ item.description }}</p>
            <ion-list :inset="true">
              <ion-item v-for="(element, index) in item.smart" :key="index">
                <ion-label><b>{{ element.letter }}</b> → {{ element.content }}</ion-label>
              </ion-item>
            </ion-list>
          </div>
        </ion-accordion>
      </ion-accordion-group>
    </ion-content>
  </ion-page>
</template>


<script setup lang="ts">
import { IonButtons, IonContent, IonHeader, IonMenuButton, IonPage, IonTitle, IonToolbar, IonAccordionGroup, IonAccordion, IonItem, IonLabel, IonList } from '@ionic/vue';
import { ref } from 'vue';


// Definición de la estructura de datos para un objetivo SMART
interface SmartElement {
  letter: string;
  content: string;
}


interface SmartGoal {
  id: number;
  title: string;
  description: string;
  smart: SmartElement[];
}


// Array de objetivos SMART
const smartGoalsNegocio = ref<SmartGoal[]>([
  {
    id: 1,
    title: "Optimización de Infraestructura (ApexCharts)",
    description: "Mantener la ocupación de servidores por debajo del 85% de la capacidad máxima visualizada en el gráfico de área, escalando recursos si se superan los 25 servidores activos de forma constante.",
    smart: [
      { letter: "S", content: "Monitorear la serie 'Servidores Activos' frente a 'Capacidad Máxima' en el ApexMixedChart." },
      { letter: "M", content: "No exceder el 85% de ocupación (máximo 25/30 servidores)." },
      { letter: "A", content: "Ajustando el balanceo de carga y activando nodos adicionales en el VPS." },
      { letter: "R", content: "Garantizar que siempre haya slots libres para nuevos alquileres de servidores." },
      { letter: "T", content: "Revisión de logs de infraestructura cada domingo." }
    ]
  },
  {
    id: 2,
    title: "Preferencia de Contenido (Chart.js)",
    description: "Lograr que el circuito 'Nordschleife' alcance al menos un 30% de cuota en el gráfico de Doughnut, promocionando eventos específicos para diversificar el uso más allá de Monza.",
    smart: [
      { letter: "S", content: "Aumentar el segmento correspondiente a 'Nordschleife' en el gráfico de circuitos." },
      { letter: "M", content: "Alcanzar un 30% de preferencia (actualmente en 20%)." },
      { letter: "A", content: "Lanzando una campaña de 'Especial Resistencia' en redes sociales." },
      { letter: "R", content: "Rentabilizar la inversión en mods y circuitos premium menos utilizados." },
      { letter: "T", content: "Medición al finalizar el próximo mes." }
    ]
  },
  {
    id: 3,
    title: "Conversión de Embudo (ECharts)",
    description: "Mejorar la tasa de conversión en el gráfico de Funnel, logrando que el 25% de los usuarios que 'Configuran Server' terminen en 'Server Lanzado'.",
    smart: [
      { letter: "S", content: "Reducir la brecha entre el segundo y cuarto nivel del EchartsFunnel." },
      { letter: "M", content: "Subir la conversión final del 20% actual al 25%." },
      { letter: "A", content: "Simplificando el formulario de registro y los pasos de pago." },
      { letter: "R", content: "Maximizar el retorno de inversión (ROI) del tráfico web atraído." },
      { letter: "T", content: "Evaluación en el dashboard de negocio en 60 días." }
    ]
  },
  {
    id: 4,
    title: "Popularidad de Flota (Gráfico Propio)",
    description: "Posicionar el 'Porsche 911 GT3' como el coche más usado en el Ranking de Mods, incrementando su barra de progreso hasta el 90% mediante la actualización de sus físicas.",
    smart: [
      { letter: "S", content: "Subir el valor de .bar-fill para el Porsche en el componente TopModsRanking." },
      { letter: "M", content: "Pasar del 62% al 90% de uso detectado por los logs." },
      { letter: "A", content: "Actualizando el mod a la versión 2026 con mejores sonidos y físicas." },
      { letter: "R", content: "Mantener a la comunidad interesada en el contenido técnico de alta calidad." },
      { letter: "T", content: "Trimestre en curso." }
    ]
  },
  {
    id: 5,
    title: "Crecimiento de Comunidad (Tiempo Real)",
    description: "Estabilizar el indicador de 'Pilotos en Vivo' por encima de los 150 usuarios concurrentes durante las horas pico de la tarde.",
    smart: [
      { letter: "S", content: "Mantener el valor de .live-number por encima de 150 de forma sostenida." },
      { letter: "M", content: "Incrementar la media de 128 a 150 pilotos concurrentes." },
      { letter: "A", content: "Organizando torneos diarios de 19:00 a 22:00 CET." },
      { letter: "R", content: "Fomentar una comunidad activa que atraiga a nuevos suscriptores por efecto red." },
      { letter: "T", content: "Monitoreo diario con reporte de picos cada 24 horas." }
    ]
  },
  {
    id: 6,
    title: "Captación de Nuevos Clientes (Sparkline)",
    description: "Aumentar la tendencia del gráfico morado de 'Nuevos Usuarios' para captar 60 nuevos registros semanales de forma orgánica.",
    smart: [
      { letter: "S", content: "Mantener la curva del SparkLine morado con tendencia ascendente." },
      { letter: "M", content: "Llegar a una media de 60 usuarios nuevos (actualmente 42)." },
      { letter: "A", content: "Mejorando el SEO de la plataforma JPA Servers." },
      { letter: "R", content: "Asegurar el crecimiento constante de la base de datos de clientes." },
      { letter: "T", content: "Análisis de tendencia en los próximos 30 días." }
    ]
  }
]);

const smartGoalsTecnico = ref<SmartGoal[]>([
  {
    id: 1,
    title: "Estado de Microservicios",
    description: "Garantizar que Auth Server, Race Engine y DB Cluster se mantengan en estado 'online', resolviendo la alerta de latencia en Assetto API para alcanzar un uptime del 99%.",
    smart: [
      { letter: "S", content: "Mantener los indicadores de la status-list en color verde." },
      { letter: "M", content: "Lograr un 99% de disponibilidad mensual en los 4 servicios core." },
      { letter: "A", content: "Interviniendo el servicio Assetto API que actualmente reporta 145ms." },
      { letter: "R", content: "Asegurar que los usuarios puedan autenticarse y competir sin desconexiones." },
      { letter: "T", content: "Evaluación al cierre del mes en curso." }
    ]
  },
  {
    id: 2,
    title: "Latencia de Red (MS)",
    description: "Estabilizar la curva del gráfico de latencia para eliminar picos de 145ms, estableciendo un techo máximo de 50ms mediante la optimización de rutas.",
    smart: [
      { letter: "S", content: "Suavizar la fluctuación en el apexchart de latencia de red." },
      { letter: "M", content: "Reducir el pico actual de 60ms - 65ms a una media inferior a 50ms." },
      { letter: "A", content: "Optimizando los tiempos de respuesta del Race Engine y Assetto API." },
      { letter: "R", content: "Eliminar el lag percibido por los pilotos durante las carreras." },
      { letter: "T", content: "Implementación y mejora en los próximos 15 días." }
    ]
  },
  {
    id: 3,
    title: "Uso de CPU Global",
    description: "Optimizar el consumo de recursos para que la fluctuación de la carga técnica se mantenga siempre por debajo del umbral del 70%, evitando saturaciones.",
    smart: [
      { letter: "S", content: "Controlar el valor del uso de la CPU y el ancho de banda." },
      { letter: "M", content: "No exceder el 70% de uso de CPU en el dashboard en tiempo real." },
      { letter: "A", content: "Ajustando la carga de procesos distribuidos en el grid del servidor." },
      { letter: "R", content: "Prevenir bloqueos del sistema o sobrecalentamiento de los nodos." },
      { letter: "T", content: "Monitoreo constante con revisión de cumplimiento a fin de mes." }
    ]
  },
  {
    id: 4,
    title: "HTTP STATUS CODES (API)",
    description: "Reducir la incidencia de errores 404 y 500 visualizados en el BarChart, bajando el volumen de peticiones fallidas a la mitad para mejorar la estabilidad.",
    smart: [
      { letter: "S", content: "Disminuir la altura de las barras de error (colores amarillo y rojo)." },
      { letter: "M", content: "Reducir los 570 errores registrados actualmente en un 50%." },
      { letter: "A", content: "Depurando los endpoints de la API que generan respuestas 500 ERR." },
      { letter: "R", content: "Mejorar la fiabilidad de las peticiones que realizan las aplicaciones cliente." },
      { letter: "T", content: "Meta a alcanzar en el próximo trimestre." }
    ]
  },
  {
    id: 5,
    title: "Distribución de RAM",
    description: "Optimizar la asignación de memoria en el gráfico circular, reduciendo el peso de AC Physics y el consumo base de Ubuntu Server en un 15%.",
    smart: [
      { letter: "S", content: "Liberar memoria RAM reflejada en el v-chart de ECharts." },
      { letter: "M", content: "Reducir el consumo total de memoria en un 15% sobre los valores actuales." },
      { letter: "A", content: "Cerrando procesos inactivos y optimizando el motor de física de AC." },
      { letter: "R", content: "Permitir que el servidor opere de forma más fluida y soporte más usuarios." },
      { letter: "T", content: "Ejecución de limpieza de procesos en un plazo de 30 días." }
    ]
  },
  {
    id: 6,
    title: "Logs de Uso de Servidores",
    description: "Mantener la carga de los 3 servidores en niveles 'Bajo' o 'Medio' (tonos azules), evitando que el Servidor 3 alcance el estado 'Crítico' de 90.",
    smart: [
      { letter: "S", content: "Evitar la aparición del color azul oscuro (#004A6B) en el heatmap." },
      { letter: "M", content: "Mantener todos los puntos de datos del mapa de calor por debajo de 60." },
      { letter: "A", content: "Balanceando el tráfico hacia el Servidor 3 durante las horas pico." },
      { letter: "R", content: "Asegurar un rendimiento constante sin degradación durante picos de uso." },
      { letter: "T", content: "Lograr estabilidad en los registros en las próximas 3 semanas." }
    ]
  }
]);
</script>


<style scoped>


ion-accordion.accordion-collapsing ion-item[slot='header'],
  ion-accordion.accordion-collapsed ion-item[slot='header'] {
    --background: var(--ion-color-light);
    --color: var(--ion-color-light-contrast);
  }


  ion-accordion.accordion-expanding ion-item[slot='header'],
  ion-accordion.accordion-expanded ion-item[slot='header'] {
    --background: rgba(var(--ion-color-primary-rgb), 0.14);
    color: var(--ion-color-primary);
  }


</style>
