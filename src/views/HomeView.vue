<script setup>
import { ref, onMounted } from 'vue'

const message = ref('')
const features = ref([
  {
    id: 1,
    name: 'Senator Database',
    status: 'In Progress',
    description: 'Collecting all data regarding the candidates.',
  },
  {
    id: 2,
    name: 'UI',
    status: 'Planned',
    description: 'To create a user interface where users can interact with the data information.',
  },
])

const completedFeatures = ref([])
const inProgressFeatures = ref([])
const plannedFeatures = ref([])

onMounted(() => {
  message.value = 'Welcome to Our Project!  This site is currently under construction.'
  sortFeatures()
})

const sortFeatures = () => {
  completedFeatures.value = features.value.filter((feature) => feature.status === 'Completed')
  inProgressFeatures.value = features.value.filter((feature) => feature.status === 'In Progress')
  plannedFeatures.value = features.value.filter((feature) => feature.status === 'Planned')
}
</script>

<template>
  <main>
    <div class="container">
      <h1>{{ message }}</h1>
      <p>
        We're currently working on this small project. Here's a sneak peek at what we're building:
      </p>

      <section v-if="inProgressFeatures.length > 0" class="feature-section">
        <h2>In Progress</h2>
        <ul>
          <li
            v-for="feature in inProgressFeatures"
            :key="feature.id"
            class="feature-item in-progress"
          >
            <h3>{{ feature.name }}</h3>
            <p>{{ feature.description }}</p>
          </li>
        </ul>
      </section>

      <section v-if="completedFeatures.length > 0" class="feature-section">
        <h2>Completed</h2>
        <ul>
          <li v-for="feature in completedFeatures" :key="feature.id" class="feature-item completed">
            <h3>{{ feature.name }}</h3>
            <p>{{ feature.description }}</p>
          </li>
        </ul>
      </section>

      <section v-if="plannedFeatures.length > 0" class="feature-section">
        <h2>Planned</h2>
        <ul>
          <li v-for="feature in plannedFeatures" :key="feature.id" class="feature-item planned">
            <h3>{{ feature.name }}</h3>
            <p>{{ feature.description }}</p>
          </li>
        </ul>
      </section>

      <p>Check back soon for updates!</p>
      <p class="last-updated">Last updated: {{ new Date().toLocaleDateString() }}</p>
    </div>
  </main>
</template>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: sans-serif;
}

h1 {
  text-align: center;
  margin-bottom: 1rem;
}

.feature-section {
  margin-bottom: 2rem;
}

.feature-item {
  border: 1px solid #ddd;
  padding: 1rem;
  margin-bottom: 0.5rem;
  border-radius: 5px;
}

.in-progress {
  border-left: 4px solid orange; /* Visual indicator for in-progress */
  background-color: #fff3cd;
}

.completed {
  border-left: 4px solid green;
  background-color: #d4edda;
}

.planned {
  border-left: 4px solid #0dcaf0;
  background-color: #cff4fc;
}

.last-updated {
  text-align: center;
  font-style: italic;
  color: #777;
}

/* Responsive adjustments */
@media (max-width: 600px) {
  .container {
    padding: 10px;
  }
}
</style>
