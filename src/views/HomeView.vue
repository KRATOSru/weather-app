<template>
  <main class="container text-white">
    <div class="pt-4 mb-8 relative">
      <input
        type="text"
        v-model="searchQuery"
        @input="getSearchResults"
        placeholder="Search for a sity or state"
        class="py-2 px-1 w-full bg-transparent border-b focus:border-weather-secondary focus:outline-none focus:shadow-[0px_1px_0_0_#004E71]"
      />
      <ul
        class="absolute bg-weather-secondary text-white w-full shadow-md py-2 px-1 top-[66px]"
        v-if="mapboxSearchResult"
      >
        <li
          v-for="searchResult in mapboxSearchResult"
          :key="searchResult.id"
          class="py-2 cursor-pointer"
        >
          {{ searchResult.place_name }}
        </li>
      </ul>
    </div>
  </main>
</template>

<script setup>
import {ref} from 'vue'
import axios from 'axios'

const mapboxAPIKey =
  'pk.eyJ1IjoidmxhZGltaXIxOTgwIiwiYSI6ImNsY21odTFqcjFjdm4zdm10eDZ3ODM3cDAifQ.om0PCy92D_6DCATF_ltI0A'
const searchQuery = ref('')
const queryTimeout = ref(null)
const mapboxSearchResult = ref(null)

const getSearchResults = () => {
  clearTimeout(queryTimeout.value)
  queryTimeout.value = setTimeout(async () => {
    if (searchQuery.value !== '') {
      const result = await axios.get(
        `https://api.mapbox.com/geocoding/v5/mapbox.places/${searchQuery.value}.json?access_token=${mapboxAPIKey}&types=place`
      )
      mapboxSearchResult.value = result.data.features
      console.log(mapboxSearchResult.value)
      return
    }
    mapboxSearchResult.value = null
  }, 300)
}
</script>
