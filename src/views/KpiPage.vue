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
    title: "Aumentar visitas",
    description: "Aumentar las visitas de nuestro sitio web en un 50% (de 1000 a 1500) en los siguientes 30 días, al duplicar la distribución de contenido y con el fin de prepararnos para el lanzamiento de nuestro nuevo producto",
    smart: [
      { letter: "S", content: "Aumentar las visitas de nuestro sitio web en un 50%" },
      { letter: "M", content: "50% (de 1,000 a 1,500)" },
      { letter: "A", content: "duplicando la distribución de contenido" },
      { letter: "R", content: "para prepararnos para el lanzamiento de nuestro nuevo producto." },
      { letter: "T", content: "en los siguientes 30 días" }
    ]
  },
  {
    id: 2,
    title: "Aumentar ventas",
    description: "Aumentar las ventas en un 20% (de $200,000 a $240,000) en los próximos 12 meses, ofreciendo nuestros nuevos productos a los clientes existentes.",
    smart: [
      { letter: "S", content: "Aumentar las ventas en un 20%" },
      { letter: "M", content: "20% (de $200,000 a $240,000)" },
      { letter: "A", content: "ofreciendo nuestros nuevos productos a los clientes existentes" },
      { letter: "R", content: "(retención de clientes y aumentar ventas)" },
      { letter: "T", content: "próximos 12 meses" }
    ]
  },
  {
    id: 3,
    title: "Ampliar equipo de marketing",
    description: "Ampliar el equipo de marketing en un 10% (de 100 a 110 empleados) para finales del primer trimestre del próximo año, al contratar 3 empleados cada 3 meses para completar el equipo de creación de contenido.",
    smart: [
      { letter: "S", content: "Ampliar el equipo de marketing en un 10%" },
      { letter: "M", content: "10% (de 100 a 110 empleados)" },
      { letter: "A", content: "contratando a 3 empleados cada 3 meses" },
      { letter: "R", content: "para completar el equipo de creación de contenido" },
      { letter: "T", content: "para finales del primer trimestre del próximo año" }
    ]
  },
  {
    id: 4,
    title: "Alianzas estratégicas",
    description: "Crear 10 alianzas estratégicas en el próximo bienio por medio de la organización de foros, y así obtener más exposición de marca y mejorar la red de proveedores.",
    smart: [
      { letter: "S", content: "Crear alianzas estratégicas" },
      { letter: "M", content: "10 alianzas estratégicas" },
      { letter: "A", content: "por medio de la organización de foros" },
      { letter: "R", content: "obtener más exposición de marca y mejorar la red de proveedores" },
      { letter: "T", content: "en 2 años" }
    ]
  },
  {
    id: 5,
    title: "Leads calificados",
    description: "Aumentar la cantidad de leads calificados de 300 a 3000 en un período de 6 meses con la creación de 5 nuevas ofertas de contenido.",
    smart: [
      { letter: "S", content: "Aumentar la cantidad de leads calificados" },
      { letter: "M", content: "de 300 a 3000" },
      { letter: "A", content: "con la creación de 5 nuevas ofertas de contenido" },
      { letter: "R", content: "(aumentar las posibilidades de venta)" },
      { letter: "T", content: "en un período de 6 meses" }
    ]
  }
]);

const smartGoalsTecnico = ref<SmartGoal[]>([
  {
    id: 1,
    title: "Estado de Microservicios",
    description: "Garantizar que Auth Server, Race Engine y DB Cluster se mantengan en estado 'online', resolviendo la alerta de latencia en Assetto API para alcanzar un uptime del 99%.",
    smart: [
      { letter: "S", content: "Mantener los indicadores de la status-list en color verde (clase .online)." },
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
      { letter: "M", content: "Reducir el pico actual de 145ms a una media inferior a 50ms." },
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
      { letter: "S", content: "Controlar el valor de la clase .live-number y el ancho de .progress-fill." },
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
