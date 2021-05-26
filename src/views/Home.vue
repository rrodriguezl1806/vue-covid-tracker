<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <DataBoxes :stats="stats" />
    <CountrySelected @get-country="getCountryData" :countries="countries"/>
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      <i class="fa fa-spinner fa-spin mr-2" aria-hidden="true"></i>
      Fetching Data
    </div>
  </main>
</template>

<script>
// @ is an alias to /src

import DataTitle from "../components/DataTitle";
import DataBoxes from "../components/DataBoxes";
import CountrySelected from "../components/CountrySelected";

export default {
  name: 'Home',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelected
  },
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: false
    }
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary')
      return res.json()
    },
    getCountryData(country) {
      this.stats = country
      this.title = country.Country
    }
  },
  async created() {
    const data = await this.fetchCovidData()
    this.dataDate = data.Date
    this.stats = data.Global
    this.countries = data.Countries
    this.loading = false

  }
}
</script>
