<script setup lang="ts">
withDefaults(defineProps<{ source: string; slide?: string | number }>(), { slide: '' })
</script>

<template>
  <footer class="source-footer">
    <span class="source-footer__label">Source</span>
    <span class="source-footer__text">{{ source }}</span>
    <span v-if="slide" class="source-footer__slide">{{ slide }}</span>
  </footer>
</template>

<style scoped>
.source-footer__slide { flex: 0 0 auto; font-variant-numeric: tabular-nums; }
</style>
