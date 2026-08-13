<script setup lang="ts">
withDefaults(defineProps<{ label: string; tone?: 'neutral' | 'architecture' | 'rl' | 'agency' }>(), { tone: 'neutral' })
</script>

<template>
  <div class="section-label" :class="`section-label--${tone}`">{{ label }}</div>
</template>

<style scoped>
.section-label--architecture { color: var(--color-architecture); }
.section-label--rl { color: var(--color-rl); }
.section-label--agency { color: var(--color-agency); }
</style>
