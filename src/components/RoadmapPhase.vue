<template>
  <div class="timeline-item" :class="`is-${phase.status}`">
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

        <div v-if="phase.note && mode === 'teacher'" class="phase-notes">
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
  index: Number,
  mode: String
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
  border: 1px solid var(--color-border-subtle);
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
  box-shadow: 0 0 0 4px var(--color-bg), 0 0 10px var(--color-glow-primary);
  transition: all 0.3s ease;
}

.timeline-item:hover .timeline-content::before {
  background-color: var(--color-primary);
  box-shadow: 0 0 0 4px var(--color-bg), 0 0 20px var(--color-primary);
}

.timeline-item:hover .timeline-content {
  transform: translateY(-4px);
  box-shadow: 0 10px 30px var(--color-shadow-dark);
  border-color: var(--color-border-medium);
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
  border-top: 1px solid var(--color-border-medium);
  padding-top: var(--s-md);
}

/* Status-based styling */
.timeline-item.is-completed {
  opacity: 0.6;
}

.timeline-item.is-completed .timeline-content {
  background: linear-gradient(145deg, var(--color-completed-bg-1), var(--color-completed-bg-2));
  border-color: var(--color-border-faint);
}

.timeline-item.is-completed .timeline-content::before {
  background-color: var(--color-primary);
  border-color: var(--color-primary);
  box-shadow: 0 0 0 4px var(--color-bg), 0 0 8px var(--color-glow-faint);
}

.timeline-item.is-completed .phase-number {
  color: var(--color-text-muted);
}

.timeline-item.is-completed .phase-title {
  text-decoration: line-through;
  text-decoration-thickness: 1px;
  color: var(--color-text-muted);
}

.timeline-item.is-current .timeline-content {
  background: linear-gradient(145deg, var(--color-card-bg), var(--color-bg));
  border: 2px solid var(--color-accent);
  box-shadow: 0 0 30px var(--color-glow-soft);
  animation: pulse 3s cubic-bezier(0.4, 0, 0.2, 1) infinite;
}

.timeline-item.is-current .timeline-content::before {
  background-color: var(--color-primary);
  border-color: var(--color-primary);
  box-shadow: 0 0 0 4px var(--color-bg), 0 0 15px var(--color-primary);
}

.timeline-item.is-current .phase-number {
  color: var(--color-primary);
  font-size: 1rem;
}

.timeline-item.is-current .phase-title {
  color: var(--color-primary);
}

.timeline-item.is-upcoming .timeline-content {
  background: linear-gradient(145deg, var(--color-upcoming-bg-1), var(--color-upcoming-bg-2));
  border-color: var(--color-border-subtle);
}

.timeline-item.is-upcoming .timeline-content::before {
  background-color: var(--color-bg);
  border-color: var(--color-border-light);
  box-shadow: 0 0 0 4px var(--color-bg);
}

.timeline-item.is-upcoming .phase-number {
  color: var(--color-upcoming-accent);
}

@keyframes pulse {

  0%,
  100% {
    box-shadow:
      0 0 0 3px var(--color-bg),
      0 0 15px var(--color-primary),
      0 0 21px var(--color-glow-medium);
  }

  50% {
    box-shadow:
      0 0 0 3px var(--color-bg),
      0 0 21px var(--color-primary),
      0 0 34px var(--color-glow-medium);
  }

}
</style>