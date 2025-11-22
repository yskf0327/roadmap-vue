<template>
  <li class="roadmap-phase">
    <h2 class="roadmap-phase__title">{{ phase.title }}</h2>

    <p class="roadmap-phase__period">
      <time :datetime="phase.start">{{ phase.start }}</time> -
      <time :datetime="phase.end">{{ phase.end }}</time>
    </p>

    <div class="roadmap-phase__content">
      <ul>
        <li v-for="(item, index) in phase.items" :key="index">
          {{ item }}
        </li>
      </ul>

      <p v-if="phase.note">{{ phase.note }}</p>
    </div>
  </li>
</template>

<script setup>
defineProps({
  phase: {
    type: Object,
    required: true
  }
});
</script>

<style scoped>
.roadmap-phase { background: var(--color-primary); color: var(--color-background); clip-path: polygon(100% 0, 100% 85%, 50% 100%, 0 85%, 0 0, 50% 15%); padding: 55px; } 
</style>