<template>
  <div>
    <header class="page-header">
      <div class="page-header__inner container">
        <hgroup class="page-title">
          <p>2025年11月開講 Webプログラミング科</p>
          <h1>授業ロードマップ</h1>
        </hgroup>
      </div>
    </header>

    <div class="container">
      <ol class="roadmap">
        <RoadmapPhase v-for="(phase, index) in phases" :key="index" :phase="phase" :index="index"></RoadmapPhase>
      </ol>
    </div>
  </div>
</template>

<script setup>
import phases from './data/roadmap.json'
import RoadmapPhase from './components/RoadmapPhase.vue'
console.log(phases)
</script>

<style scoped></style>
