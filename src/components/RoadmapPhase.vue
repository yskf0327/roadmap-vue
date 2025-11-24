<template>
  <div class="timeline-item" :class="{ 'is-even': index % 2 === 0, 'is-odd': index % 2 !== 0 }">
    <div class="timeline-content">
      <header class="phase-header">
        <div class="phase-meta">
          <span class="phase-number">Phase {{ index + 1 }}</span>
          <span class="phase-period">
            <time :datetime="phase.start">{{ formatDate(phase.start) }}</time> -
            <time :datetime="phase.end">{{ formatDate(phase.end) }}</time>
          </span>
        </div>
        <h2 class="phase-title">{{ phase.title }}</h2>
      </header>

      <div class="phase-body">
        <ul class="phase-items">
          <li v-for="(item, i) in phase.items" :key="i">
            {{ item }}
          </li>
        </ul>

        <div v-if="phase.note" class="phase-notes">
          <p v-for="(para, i) in phase.note" :key="i">{{ para }}</p>
        </div>
      </div>
    </div>
  </div>
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
  if (!datetime) return '';
  const dateObj = new Date(datetime);
  return dateObj.toLocaleDateString('ja-JP', { month: 'short', day: 'numeric' });
}
</script>

<style scoped>
.timeline-item {
  position: relative;
  margin-bottom: var(--s-xl);
  width: 100%;
}

.timeline-content {
  position: relative;
  margin-left: 50px;
  background: linear-gradient(145deg, var(--color-card-bg), var(--color-bg));
  padding: var(--s-lg);
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.05);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.timeline-content::before {
  content: '';
  position: absolute;
  left: -30px;
  top: 0;
  width: 16px;
  height: 16px;
  background-color: var(--color-bg);
  border: 2px solid var(--color-primary);
  border-radius: 50%;
  transform: translateX(-50%);
  z-index: 1;
  box-shadow: 0 0 0 4px var(--color-bg), 0 0 10px rgba(59, 130, 246, 0.5);
  transition: all 0.3s ease;
}

.timeline-item:hover .timeline-content::before {
  background-color: var(--color-primary);
  box-shadow: 0 0 0 4px var(--color-bg), 0 0 20px var(--color-primary);
}

.timeline-item:hover .timeline-content {
  transform: translateY(-4px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
  border-color: rgba(255, 255, 255, 0.1);
}

.phase-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--s-sm);
  font-size: 0.875rem;
  color: var(--color-text-muted);
}

.phase-number {
  color: var(--color-accent);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.phase-title {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: var(--s-md);
  color: var(--color-text);
}

.phase-items {
  list-style: none;
  padding: 0;
  margin: 0 0 var(--s-md);
}

.phase-items li {
  position: relative;
  padding-left: 1.5em;
  margin-bottom: 0.5em;
  color: var(--color-text);
}

.phase-items li::before {
  content: "•";
  position: absolute;
  left: 0;
  color: var(--color-primary);
}

.phase-notes {
  font-size: 0.9rem;
  color: var(--color-text-muted);
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding-top: var(--s-md);
}
</style>