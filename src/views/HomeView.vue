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
  message.value = 'Welcome to Our Project! This site is currently under construction.'
  sortFeatures()
})

const sortFeatures = () => {
  completedFeatures.value = features.value.filter((feature) => feature.status === 'Completed')
  inProgressFeatures.value = features.value.filter((feature) => feature.status === 'In Progress')
  plannedFeatures.value = features.value.filter((feature) => feature.status === 'Planned')
}
</script>

<template>
  <main class="max-w-3xl mx-auto p-5">
    <h1 class="text-center text-2xl font-bold mb-4">{{ message }}</h1>
    <p class="text-center mb-6">We're currently working on this small project. Here's a sneak peek at what we're building:</p>

    <section v-if="inProgressFeatures.length > 0" class="mb-8">
      <h2 class="text-xl font-semibold mb-3">In Progress</h2>
      <ul>
        <li v-for="feature in inProgressFeatures" :key="feature.id" class="p-4 mb-3 border-l-4 border-orange-500 bg-orange-100 rounded">
          <h3 class="font-medium">{{ feature.name }}</h3>
          <p>{{ feature.description }}</p>
        </li>
      </ul>
    </section>

    <section v-if="completedFeatures.length > 0" class="mb-8">
      <h2 class="text-xl font-semibold mb-3">Completed</h2>
      <ul>
        <li v-for="feature in completedFeatures" :key="feature.id" class="p-4 mb-3 border-l-4 border-green-500 bg-green-100 rounded">
          <h3 class="font-medium">{{ feature.name }}</h3>
          <p>{{ feature.description }}</p>
        </li>
      </ul>
    </section>

    <section v-if="plannedFeatures.length > 0" class="mb-8">
      <h2 class="text-xl font-semibold mb-3">Planned</h2>
      <ul>
        <li v-for="feature in plannedFeatures" :key="feature.id" class="p-4 mb-3 border-l-4 border-blue-500 bg-blue-100 rounded">
          <h3 class="font-medium">{{ feature.name }}</h3>
          <p>{{ feature.description }}</p>
        </li>
      </ul>
    </section>

    <p class="text-center">Check back soon for updates!</p>
    <p class="text-center text-gray-500 italic">Last updated: {{ new Date().toLocaleDateString() }}</p>
  </main>
</template>

<style scoped>
/* Tailwind CSS handles all styling */
</style>