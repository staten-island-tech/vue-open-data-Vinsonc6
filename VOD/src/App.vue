<template>
  <div>
    <ul>
      <li v-for="item in firehouses" :key="item.facilityname">
        {{ item.facilityname }} - {{ item.primary_facilityaddress }}
        {{ item.facilityaddress }} - {{ item.borough }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const firehouses = ref([])

onMounted(async () => {
  const res = await fetch('https://data.cityofnewyork.us/resource/hc8x-tcnd.json?$limit=25')
  firehouses.value = await res.json()
})
</script>