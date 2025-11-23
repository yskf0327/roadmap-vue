<template>
  <li class="roadmap-phase">
    <header class="roadmap-phase__header">
      <h2 class="roadmap-phase__title"><span>{{ `${index + 1}.${phase.title}` }}</span></h2>
      <p class="roadmap-phase__period">
        <time :datetime="phase.start">{{ formatDate(phase.start) }}</time> -
        <time :datetime="phase.end">{{ formatDate(phase.end) }}</time>
      </p>
    </header>

    <!-- <div class="roadmap-phase__content"> -->
    <ul class="roadmap-phase__todo">
      <li v-for="(item, index) in phase.items" :key="index">
        {{ item }}
      </li>
    </ul>

    <div v-if="phase.note" class="roadmap-phase__note">
      <p v-for="(para, index) in phase.note" :key="index">{{ para }}</p>
    </div>
    <!-- </div> -->
  </li>
</template>

<script setup>
defineProps({
  phase: {
    type: Object,
    required: true
  },
  index: Number
});

const formatDate = (datetime) => {
  const sep = '.';
  if (!datetime) return '';
  const dateObj = new Date(datetime);
  const y = dateObj.getFullYear();
  const n = dateObj.getMonth() + 1;
  const j = dateObj.getDate();

  return `${y}.${n}.${j}`;
}
</script>

<style scoped></style>