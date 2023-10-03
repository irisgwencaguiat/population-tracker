<template>
  <main>
    <CountrySelect @get-country-iso3="getCountryPopulationData" :countries="countries"/>
    <main class="text-center" v-if="loading">
      <div class="text-gray-500 text-3xl mt-10 mb-6">
        Fetching Data
      </div>
      <img :src="loadingImage" class="w-44 m-auto">
    </main>
    <PopulationTable v-if="countrySelected && !loading" :populations="populations" />
  </main>
</template>

<script>
import CountrySelect from "@/components/CountrySelect";
import PopulationTable from "@/components/PopulationTable";

export default {
  name: 'HomeView',
  components: {
    CountrySelect,
    PopulationTable
  },
  data () {
    return {
      countries: [],
      populations: [],
      loading: false,
      loadingImage: require('../assets/hourglass-loop-motion-design-animation-hourglass-motion-design.gif'),
      countrySelected: false
    }
  },
  methods: {
    async fetchCountries () {
      const res = await fetch('https://countriesnow.space/api/v0.1/countries')
      const data = await res.json()
      return data
    },
    async getCountryPopulationData (iso3) {
      if (iso3 == 0) {
        this.countrySelected = false
        this.loading = false
      } else {
        this.loading = true
        const requestOptions = {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ iso3: iso3 })
        }
        const res = await fetch('https://countriesnow.space/api/v0.1/countries/population', requestOptions)
        const data = await res.json();
        this.populations = data.data.populationCounts
        this.countrySelected = true
        this.loading = false
      }

    }

  },
  async created () {
    const data = await this.fetchCountries()
    this.countries = data.data
  }
}
</script>
