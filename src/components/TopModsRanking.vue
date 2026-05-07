<template>
    <div class="ranking-container">
      <div v-for="mod in mods" :key="mod.name" class="mod-row">
        <div class="mod-info">
          <span class="mod-name">{{ mod.name }}</span>
          <span class="mod-value">{{ mod.usage }}%</span>
        </div>
        <div class="progress-bg">
          <div 
            class="progress-fill" 
            :style="{ width: mod.usage + '%', backgroundColor: mod.color }"
          ></div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  const mods = [
  { name: 'BMW M4 GT3', usage: 88, color: '#00d2ff' },     
  { name: 'Porsche 911 GT3', usage: 62, color: '#9d50bb' },  
  { name: 'Formula Hybrid', usage: 45, color: '#6e48aa' }  
];

  </script>
  
  <style scoped>
  .ranking-container {
    width: 100%;
    padding: 10px;
  }
  .mod-row {
    margin-bottom: 15px;
  }
  .mod-info {
    display: flex;
    justify-content: space-between;
    margin-bottom: 5px;
    color: white;
    font-size: 0.9em;
  }
  .progress-bg {
    background: #333;
    height: 8px;
    border-radius: 10px;
    overflow: hidden;
  }
  .progress-fill {
    height: 100%;
    border-radius: 10px;
    transition: width 1.5s ease-in-out;
  }
  </style>