<script setup>
import { computed, ref } from 'vue'
import Stat from './components/Stat.vue';
import CitySelect from './components/CitySelect.vue';


// const currentDate = new Date().toLocaleDateString()

let data = ref({
  humidity: 90,
})

const dataModified = computed(() => {
  return {
    label: "Влажность",
    stat: data.value.humidity + '%',
  }
})

let savedCity = ref("Москва");

function getCity(city) {
  savedCity.value = city
  data.value.stat = "33%"
}
</script>

<template>
  <main class="main">
    {{ savedCity }}
    <Stat v-bind="dataModified" />
    <Stat label="Осадки" stat="0%" />
    <CitySelect @select-city="getCity" />
  </main>
</template>

<style scoped>
.main {
  background: var(--color-bg-main);
  padding: 60px 50px;
  border-radius: 25px;
}
</style>
