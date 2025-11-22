<template>
  <div>
    <h1>roadmap</h1>

    <div class="container">
      <ol class="roadmap">
        <RoadmapPhase v-for="(phase,index) in phases" :key="index" :phase="phase"></RoadmapPhase>
      </ol>
    </div>
  </div>
</template>

<script setup>

import phases from './data/radmap.json'
import RoadmapPhase from './components/RoadmapPhase.vue';

</script>

<style scoped>

</style>
