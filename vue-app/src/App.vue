<script setup>
import { computed, ref } from 'vue'
import Stat from './components/Stat.vue';
import CitySelect from './components/CitySelect.vue';

const API_ENDPOINT = 'https:/api.weatherapi.com/v1'
// const currentDate = new Date().toLocaleDateString()

let data = ref({
  humidity: 90,
  rain: 20,
  wind: 77
})

const dataModified = computed(() => {
  return [{
    label: "Влажность",
    stat: data.value.humidity + '%',
  },
  {
    label: "Облачность",
    stat: data.value.rain + '%',
  }, {
    label: "Ветер",
    stat: data.value.wind + 'м/ч',
  }]
})

async function getCity(city) {
  const params = new URLSearchParams({

    q: city,
    lang: "ru",
    key: "7cdaf9706e94460aba4172333251306",
    days: 3,

  })
  const res = await fetch(`${API_ENDPOINT}/forecast.json?${params.toString()}`)
  const data = await res.json()
  console.log(params)
  console.log(data)
}

</script>

<template>
  <main class="main">
    {{ savedCity }}
    <Stat v-for="item in dataModified" v-bind="item" :key="item.label" />
    {{ key }}
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
