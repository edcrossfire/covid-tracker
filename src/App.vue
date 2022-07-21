<template>
    <div class="h-screen w-screen bg-indigo-50">
      <div class="bg-gradient-to-br from-indigo-400 to-indigo-700 text-center p-4 text-4xl lg:text-5xl text-indigo-50 mb-10 font-bold max-w-screen-sm md:max-w-screen-md lg:max-w-screen-lg mx-auto shadow-xl rounded-b-xl">
          <Header />
      </div>
      <main v-if="!loading">
        <DataTitle :text="title" :dataDate="dataDate" />
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

export default {
  components: {
    Header,
    DataTitle,
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
    }
  },
  async created() {
    const data = await this.fetchCovidData()
    this.dataDate = data.dataDate
    this.stats = data.Global
    this.countries = data.countries
    this.loading = false
  },
}
</script>