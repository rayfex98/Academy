<template>
  <span
    class="shiny-text"
    :style="shinyStyle"
  >
    <slot />
  </span>
</template>

<script setup lang="ts">
import { computed } from 'vue'

interface Props {
  baseColor?: string
  shineColor?: string
  speed?: number   // seconds per cycle
  spread?: number  // gradient degrees
}

const props = withDefaults(defineProps<Props>(), {
  baseColor: '#64CEFB',
  shineColor: '#ffffff',
  speed: 3,
  spread: 100,
})

const shinyStyle = computed(() => ({
  backgroundImage: `linear-gradient(
    ${props.spread}deg,
    ${props.baseColor} 0%,
    ${props.baseColor} 35%,
    ${props.shineColor} 50%,
    ${props.baseColor} 65%,
    ${props.baseColor} 100%
  )`,
  backgroundSize: '200% auto',
  backgroundClip: 'text',
  WebkitBackgroundClip: 'text',
  color: 'transparent',
  WebkitTextFillColor: 'transparent',
  animation: `shine ${props.speed}s linear infinite`,
  display: 'inline',
}))
</script>

<style scoped>
.shiny-text {
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  /* Inherit typography from parent */
  font-size: inherit;
  font-weight: inherit;
  line-height: inherit;
  letter-spacing: inherit;
}

@keyframes shine {
  0%   { background-position: -200% center; }
  100% { background-position: 200% center; }
}
</style>
