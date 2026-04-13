<template>
  <div>

    <select v-model="selectedBorough">
      <option value="All">All</option>
      <option value="Manhattan">Manhattan</option>
      <option value="Brooklyn">Brooklyn</option>
      <option value="Queens">Queens</option>
      <option value="Bronx">Bronx</option>
      <option value="Staten Island">Staten Island</option>
    </select>

    <ul>
      <li v-for="item in filteredStations" :key="item.facilityname">
        {{ item.facilityname }} - {{ item.facilityaddress }} - {{ item.borough }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'

const firehouses = ref([])
const selectedBorough = ref('All')

onMounted(async () => {
  try {
    const res = await fetch(
      'https://data.cityofnewyork.us/resource/hc8x-tcnd.json'
    )
    firehouses.value = await res.json()
  } catch (error) {
    alert('Error fetching data: ' + error.message)
  }
})


const filteredStations = computed(() => {
  if (selectedBorough.value === 'All') {
    return firehouses.value
  }

  return firehouses.value.filter(
    station => station.borough === selectedBorough.value
  )
})
</script>