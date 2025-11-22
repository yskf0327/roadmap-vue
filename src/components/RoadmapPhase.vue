<template>
  <li class="roadmap-phase">
    <header class="roadmap-phase__header">
      <h2 class="roadmap-phase__title"><span>{{ phase.title }}</span></h2>
      <p class="roadmap-phase__period">
        <time :datetime="phase.start">{{ formatDate(phase.start) }}</time> -
        <time :datetime="phase.end">{{ formatDate(phase.end) }}</time>
      </p>
    </header>

    <div class="roadmap-phase__content">
      <ul>
        <li v-for="(item, index) in phase.items" :key="index">
          {{ item }}
        </li>
      </ul>

      <div class="roadmap-phase__note">
        <p v-if="phase.note" v-for="(para, index) in phase.note" :key="index">{{ para }}</p>
      </div>
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

<style scoped>
.roadmap-phase {
  display: flex;
  flex-direction: column;
  gap: 21px;
  background: var(--color-primary);
  color: var(--color-background);
  /* clip-path: polygon(100% 0, 100% 90%, 50% 100%, 0 90%, 0 0, 50% 10%); */
  padding-inline: var(--s-md);
  padding-block: var(--s-2xl) var(--s-xl);
  position: relative;

  &::before,
  &::after {
    position: absolute;
    left: 0;
    display: block;
    content: "";
    width: 100%;
    height: 30px;
    clip-path: polygon(50% 100%, 0 1%, 100% 1%);
  }

  &::before {
    top: -1px;
    background-color: var(--color-background);
  }

  &::after {
    bottom: -29px;
    background-color: var(--color-primary);
  }
}

.roadmap-phase__title {
  /* font-size: var(--fz-lg); */
  font-weight: bold;

  span {
    background-image: linear-gradient(180deg, transparent 70%, var(--color-secondary) 20%);
  }
}

.roadmap-phase__period {
  font-size: var(--fz-base);
  margin-block-start: var(--s-sm);

}

.roadmap-phase__content {
  display: flex;
  flex-direction: column;
  gap: 13px;

  ul>li,
  p {
    line-height: 1.7;
  }



  ul {
    margin-inline-start: 0.5em;

    li {
      padding-inline-start: 0.3em;

      &::marker {
        content: "-";
      }
    }
  }
}

.roadmap-phase__note {
  background-color: var(--color-text);
  /* color: var(--color-text); */
  border-radius: var(--s-sm);
  padding: var(--s-sm);

  p+p {
    margin-block-start: var(--s-md);
  }
}

/* .roadmap-phase__content p {
  white-space: pre-line;
} */
</style>