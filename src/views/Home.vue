<template>
  <div class="home">
    Hello 
  </div>
</template>

<script>

export default {
  name: 'Home',
  components: {},
  methods: {
    async fetchData(){
      const res = await fetch('https://api.covid19api.com/summary');
      const data = await res.json();
      return data;
    }
  },
  async created(){
    const data = await this.fetchData();
    console.log(data)
  }
}
</script>
