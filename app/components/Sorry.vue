<template>
  <div class="sorry-container">
    <!-- Glowing background accents -->
    <div class="glow glow-1"></div>
    <div class="glow glow-2"></div>
    


    <!-- Chart Section -->
    <div class="chart-section" :class="{ 'visible': loaded }">
      <!-- Bar 1: Unnecessary dragging time -->
      <div class="bar-container">
        <div class="bar-label">
          <Clock :size="18" class="bar-icon warning" />
          <span>Benim Gereksiz Uzatma Sürem</span>
        </div>
        <div class="bar-track">
          <div 
            class="bar bar-warning" 
            :class="{ 'animate': loaded, 'shake': loaded }"
            :style="{ '--target-width': '85%' }"
          >
          </div>
        </div>
      </div>

      <!-- Bar 2: Love bar (infinite overflow) -->
      <div class="bar-container">
        <div class="bar-label">
          <HeartHandshake :size="18" class="bar-icon love" />
          <span>Sana Duyduğum Sevgi ( Ekrana Sığmıyor :p )</span>
        </div>
        <div class="bar-track overflow-visible">
          <div 
            class="bar bar-love" 
            :class="{ 'animate': loaded, 'infinite': loaded }"
          >
            <span class="bar-value infinite-text">∞</span>
            <Sparkles :size="16" class="sparkle sparkle-1" />
            <Sparkles :size="14" class="sparkle sparkle-2" />
            <Sparkles :size="16" class="sparkle sparkle-3" />
          </div>
        </div>
      </div>
    </div>

    <!-- Caption -->
    <p class="caption" :class="{ 'visible': loaded }">
      veriler yalan söylemez :)
    </p>

    <!-- Heart decoration -->
    <div class="floating-hearts" :class="{ 'visible': loaded }">
      <Heart 
        v-for="n in 6" 
        :key="n" 
        :size="12 + n * 3" 
        :class="`floating-heart heart-${n}`"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Heart, Clock, HeartHandshake, Sparkles } from 'lucide-vue-next'

const loaded = ref(false)

onMounted(() => {
  setTimeout(() => {
    loaded.value = true
  }, 300)
})
</script>

<style scoped>
/* Import a handwritten/elegant font */
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;1,400&family=Dancing+Script:wght@500;700&display=swap');

.sorry-container {
  position: fixed;
  inset: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  z-index: 1000;
  overflow: hidden;
  background: transparent;
}

/* Glowing orbs for atmosphere */
.glow {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.4;
  pointer-events: none;
}

.glow-1 {
  width: 300px;
  height: 300px;
  background: radial-gradient(circle, var(--flower-2) 0%, transparent 70%);
  top: 10%;
  left: 20%;
  animation: float-glow 8s ease-in-out infinite alternate;
}

.glow-2 {
  width: 250px;
  height: 250px;
  background: radial-gradient(circle, var(--flower-1) 0%, transparent 70%);
  bottom: 20%;
  right: 15%;
  animation: float-glow 6s ease-in-out infinite alternate-reverse;
}

@keyframes float-glow {
  0% { transform: translate(0, 0) scale(1); }
  100% { transform: translate(20px, -20px) scale(1.1); }
}

/* Title Section */
.title-wrapper {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 3rem;
  opacity: 0;
  transform: translateY(-30px);
  transition: all 0.8s cubic-bezier(0.34, 1.56, 0.64, 1);
}

.title-wrapper.visible {
  opacity: 1;
  transform: translateY(0);
}

.heart-icon {
  color: var(--flower-2);
  filter: drop-shadow(0 0 10px var(--flower-2));
  animation: pulse-heart 1.5s ease-in-out infinite;
}

@keyframes pulse-heart {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.15); }
}

.title {
  font-family: 'Dancing Script', cursive;
  font-size: clamp(2.5rem, 6vw, 4rem);
  font-weight: 700;
  background: linear-gradient(135deg, var(--flower-1), var(--flower-2), var(--flower-3));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-shadow: 0 0 30px rgba(255, 184, 140, 0.3);
  letter-spacing: 0.05em;
}

/* Chart Section */
.chart-section {
  width: 100%;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  gap: 2rem;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.8s 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
}

.chart-section.visible {
  opacity: 1;
  transform: translateY(0);
}

.bar-container {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.bar-label {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.4rem;
  font-weight: 700;
  color: var(--center);
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.5);
  letter-spacing: 0.02em;
}

.bar-icon {
  flex-shrink: 0;
}

.bar-icon.warning {
  color: #ffb88c;
}

.bar-icon.love {
  color: var(--flower-2);
  animation: pulse-heart 1.5s ease-in-out infinite;
}

.bar-track {
  position: relative;
  height: 2.5rem;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 1.25rem;
  overflow: hidden;
  border: 1px solid rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
}

.bar-track.overflow-visible {
  overflow: visible;
}

.bar {
  position: absolute;
  left: 0;
  top: 0;
  height: 100%;
  border-radius: 1.25rem;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  padding-right: 1rem;
  width: 0;
  transition: width 2s cubic-bezier(0.34, 1.56, 0.64, 1);
}

.bar.animate {
  width: var(--target-width, 100%);
}

.bar-warning {
  background: linear-gradient(90deg, 
    rgba(255, 153, 102, 0.8) 0%, 
    rgba(255, 140, 105, 0.9) 50%, 
    rgba(255, 127, 80, 1) 100%
  );
  box-shadow: 
    0 0 20px rgba(255, 140, 105, 0.4),
    inset 0 2px 4px rgba(255, 255, 255, 0.2);
}

.bar-warning.shake {
  animation: subtle-shake 0.5s 2.2s ease-in-out 3;
}

@keyframes subtle-shake {
  0%, 100% { transform: translateX(0); }
  25% { transform: translateX(-3px); }
  75% { transform: translateX(3px); }
}

.bar-love {
  background: linear-gradient(90deg, 
    rgba(255, 212, 184, 0.9) 0%, 
    rgba(255, 184, 140, 1) 30%, 
    rgba(255, 204, 153, 1) 60%,
    rgba(255, 215, 0, 0.9) 100%
  );
  box-shadow: 
    0 0 30px rgba(255, 184, 140, 0.5),
    0 0 60px rgba(255, 215, 0, 0.3),
    inset 0 2px 4px rgba(255, 255, 255, 0.3);
  z-index: 10;
}

.bar-love.infinite {
  animation: grow-infinite 2.5s 0.5s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

@keyframes grow-infinite {
  0% { width: 0; }
  30% { width: 100%; }
  100% { width: calc(100% + 8000px); }
}

.bar-value {
  font-family: 'Cormorant Garamond', serif;
  font-weight: 800;
  font-size: 1.2rem;
  color: var(--dark-color);
  text-shadow: 0 1px 3px rgba(255, 255, 255, 0.5);
  white-space: nowrap;
}

.infinite-text {
  font-size: 1.5rem;
  margin-right: 0.5rem;
  animation: pulse-infinity 1s ease-in-out infinite;
}

@keyframes pulse-infinity {
  0%, 100% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.2); opacity: 0.8; }
}

/* Sparkles on love bar */
.sparkle {
  position: absolute;
  color: #fff;
  animation: sparkle-float 2s ease-in-out infinite;
  opacity: 0.9;
  filter: drop-shadow(0 0 4px rgba(255, 255, 255, 0.8));
}

.sparkle-1 {
  right: 60px;
  top: 2px;
  animation-delay: 0s;
}

.sparkle-2 {
  right: 30px;
  top: 8px;
  animation-delay: 0.3s;
}

.sparkle-3 {
  right: 90px;
  top: 5px;
  animation-delay: 0.6s;
}

@keyframes sparkle-float {
  0%, 100% { 
    transform: translateY(0) rotate(0deg); 
    opacity: 0.8;
  }
  50% { 
    transform: translateY(-8px) rotate(15deg); 
    opacity: 1;
  }
}

/* Caption */
.caption {
  margin-top: 3rem;
  font-family: 'Cormorant Garamond', serif;
  font-style: italic;
  font-weight: 700;
  font-size: clamp(1.2rem, 3vw, 1.6rem);
  color: var(--center);
  text-align: center;
  max-width: 550px;
  line-height: 1.6;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.6);
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.8s 1.5s ease-out;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
}

.caption.visible {
  opacity: 0.9;
  transform: translateY(0);
}

/* Floating hearts background */
.floating-hearts {
  position: absolute;
  inset: 0;
  pointer-events: none;
  opacity: 0;
  transition: opacity 1s 2s ease-out;
}

.floating-hearts.visible {
  opacity: 1;
}

.floating-heart {
  position: absolute;
  color: var(--flower-2);
  opacity: 0.3;
  animation: float-up 8s ease-in-out infinite;
}

.heart-1 { left: 10%; bottom: -50px; animation-delay: 0s; }
.heart-2 { left: 25%; bottom: -50px; animation-delay: 1.5s; }
.heart-3 { left: 50%; bottom: -50px; animation-delay: 0.8s; }
.heart-4 { left: 70%; bottom: -50px; animation-delay: 2.2s; }
.heart-5 { left: 85%; bottom: -50px; animation-delay: 1s; }
.heart-6 { left: 40%; bottom: -50px; animation-delay: 3s; }

@keyframes float-up {
  0% {
    transform: translateY(0) rotate(0deg) scale(1);
    opacity: 0;
  }
  10% {
    opacity: 0.4;
  }
  90% {
    opacity: 0.4;
  }
  100% {
    transform: translateY(-100vh) rotate(360deg) scale(0.5);
    opacity: 0;
  }
}

/* Responsive adjustments */
@media (max-width: 640px) {
  .sorry-container {
    padding: 1rem;
  }
  
  .chart-section {
    max-width: 100%;
  }
  
  .bar-label {
    font-size: 0.95rem;
  }
  
  .bar-track {
    height: 2rem;
  }
  
  .bar-love.infinite {
    animation: grow-infinite-mobile 2.5s 0.5s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
  }
  
  @keyframes grow-infinite-mobile {
    0% { width: 0; }
    30% { width: 100%; }
    100% { width: calc(100% + 400px); }
  }
}
</style>
