<template>
  <div>
    <BlossomingFlowers />
  </div>
</template>

<script setup>
// App.vue - Root component with BlossomingFlowers component
</script>

<style>
*, *::after, *::before {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

:root {
  --dark-color: #2a1810;
  --flower-1: #ffd4b8;
  --flower-2: #ffb88c;
  --flower-3: #ff9966;
  --center: #fff5e6;
  --accent: #ffcc99;
  --leaf-1: #e8b896;
  --leaf-2: #d4a574;
  --bg-color: #2a1810;
  --smooth: cubic-bezier(0.4, 0.0, 0.2, 1);
  --organic: cubic-bezier(0.34, 1.56, 0.64, 1);
  
}
.flower,
.leaf,
.grass,
.light {
  will-change: transform, opacity, filter;
  transform-style: preserve-3d;
}

.scene {
  perspective: 1000px;
}
body {
  display: flex;
  align-items: flex-end;
  justify-content: center;
  min-height: 100vh;
  background-color: var(--dark-color);
  overflow: hidden;
  perspective: 1000px;
}
</style>