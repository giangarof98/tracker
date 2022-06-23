<template>
  <main v-if="!loading">
    <DataTitle :text='title' :dataDate="dataDate" />
    <DataBoxes :stats='stats'/>
    <CountrySelect @get-country="getCountry" :countries='countries' />
    <button @click="clearCountry()" v-if="stats.Country" class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600">Clear Country</button>
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
      <h3 :src="loadingText" class="w-24 m-auto"></h3>
    </div>
  </main>
</template>

<script>

import DataTitle from '@/components/title'
import DataBoxes from '@/components/dataBoxes'
import CountrySelect from '@/components/countrySelect'

export default {
  name: 'Home',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },
  data(){
    return {
      loading: true,
      title: 'Global',
      stats: {},
      countries: [],
      loadingText: 'Loading'

    }
  },
  methods: {
    async fetchData(){
      const res = await fetch('https://api.covid19api.com/summary');
      const data = await res.json();
      return data;
    },
    getCountry(country){
      this.stats = country
      this.title = country.Country
    },
    async clearCountry(){
      this.loading = true;
      const data = await this.fetchData();
      this.title = "Global";
      this.stats = data.Global;
      this.loading = false
    },
  },
  async created(){
    const data = await this.fetchData();
    this.dataDate = data.Date 
    this.stats = data.Global
    this.countries = data.Countries
    this.loading = false
  }
}
</script>
