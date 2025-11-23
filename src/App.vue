<template>
  <div>
    <header class="page-header">
      <div class="container">
        <hgroup class="page-title">
          <p>2025年11月開講 Webプログラミング科</p>
          <h1>授業ロードマップ</h1>
        </hgroup>
      </div>
    </header>

    <main class="container">
      <div class="timeline">
        <div class="timeline-line"></div>
        <RoadmapPhase v-for="(phase, index) in phases" :key="index" :phase="phase" :index="index" />
      </div>
    </main>
  </div>
</template>

<script setup>
import phases from './data/roadmap.json'
import RoadmapPhase from './components/RoadmapPhase.vue'
</script>

<style scoped>
.timeline {
  position: relative;
  padding: var(--s-lg) 0;
  max-width: 800px;
  margin: 0 auto;
}

.timeline-line {
  position: absolute;
  left: 20px;
  /* Adjust based on node size */
  top: 0;
  bottom: 0;
  width: 2px;
  background: var(--color-line);
}
</style>
