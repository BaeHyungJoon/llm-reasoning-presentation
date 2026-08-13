<script setup lang="ts">
withDefaults(defineProps<{ tone?: 'neutral' | 'architecture' | 'rl' | 'agency'; label?: string }>(), { tone: 'neutral' })
</script>

<template>
  <div class="flow-arrow-wrap">
    <span v-if="label" class="flow-arrow-label">{{ label }}</span>
    <span class="flow-arrow" :class="`flow-arrow--${tone}`" aria-hidden="true">
      <i class="flow-arrow__line" /><i class="flow-arrow__head" />
    </span>
  </div>
</template>

<style scoped>
.flow-arrow-wrap { display: inline-flex; flex-direction: column; align-items: center; gap: var(--space-1); }
.flow-arrow-label { color: var(--color-muted); font-size: 11px; }
</style>
