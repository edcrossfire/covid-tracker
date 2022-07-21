<template>
    <div class="h-screen w-screen bg-indigo-50">
      <div class="bg-gradient-to-br from-indigo-400 to-indigo-700 text-center p-4 text-4xl lg:text-5xl text-indigo-50 mb-10 font-bold max-w-screen-sm md:max-w-screen-md lg:max-w-screen-lg mx-auto shadow-xl rounded-b-xl">
          <Header />
      </div>
      <main v-if="!loading">
        <DataTitle :text="title" :dataDate="dataDate" />
        <DataBoxes :stats="stats" />
        <CountrySelect @get-country="getCountryData" :countries="countries" />
        <button @click="clearCountryData" v-if="stats.Country" class="bg-indigo-700 text-indigo-50 rounded-xl p-3 focus:outline-none hover:bg-indigo-600 w-96 max-w-screen-sm md:max-w-screen-md lg:max-w-screen-lg grid mx-auto">Clear Country</button>
      </main>
      <main class="flex flex-col items-center space-y-3" v-else>
        <div class="text-2xl">
          Fetching Data
        </div>
        <img :src="loadingImage" alt="loading" class="w-12 m-auto" />
      </main>
    </div>
    
</template>

<script>
import Header from "@/components/Header.vue"
import DataTitle from "@/components/DataTitle.vue"
import DataBoxes from "@/components/DataBoxes.vue"
import CountrySelect from "./components/CountrySelect.vue"

export default {
  components: {
    Header,
    DataTitle,
    DataBoxes,
    CountrySelect,
    CountrySelect
},
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      status: {},
      countries: [],
      loadingImage: require('./assets/loading.gif')
    }
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary')
      const data = await res.json()
      return data
    },
    getCountryData(country) {
      this.stats = country
      this.title = country.Country
    },
    async clearCountryData() {
      this.loading = true
      const data = await this.fetchCovidData()
      this.title = 'Global'
      this.stats = data.Global
      this.loading = false
    }
  },
  async created() {
    const data = await this.fetchCovidData()
    this.dataDate = data.Date
    this.stats = data.Global
    this.countries = data.Countries
    this.loading = false
  },
}
</script>