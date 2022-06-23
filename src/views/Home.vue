<template>
  <main v-if="!loading">
    <DataTitle :text='title' :dataDate="dataDate" />
    <DataBoxes :stats='stats'/>
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

export default {
  name: 'Home',
  components: {
    DataTitle,
    DataBoxes
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
    }
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
