<script setup lang="ts">
withDefaults(defineProps<{ title: string; eyebrow?: string; tone?: 'neutral' | 'architecture' | 'rl' | 'agency' }>(), { tone: 'neutral' })
</script>

<template>
  <div class="concept-card" :class="`concept-card--${tone}`">
    <div v-if="eyebrow" class="concept-card__eyebrow">{{ eyebrow }}</div>
    <div class="concept-card__title">{{ title }}</div>
    <div class="concept-card__body"><slot /></div>
  </div>
</template>

<style scoped>
.concept-card { min-height: 108px; }
.concept-card__eyebrow { color: var(--color-muted); font-size: 12px; letter-spacing: .08em; margin-bottom: var(--space-2); text-transform: uppercase; }
.concept-card__title { color: var(--color-text); font-size: 20px; font-weight: 720; line-height: 1.25; }
.concept-card__body { color: var(--color-muted); font-size: 14px; margin-top: var(--space-2); }
.concept-card--architecture { border-color: rgba(49,215,244,.48); }.concept-card--architecture .concept-card__title { color: var(--color-architecture); }
.concept-card--rl { border-color: rgba(173,124,255,.48); }.concept-card--rl .concept-card__title { color: var(--color-rl); }
.concept-card--agency { border-color: rgba(255,180,84,.48); }.concept-card--agency .concept-card__title { color: var(--color-agency); }
</style>
