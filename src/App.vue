<template>
  <div class="mx-auto">
    <Header />
    <div class="container mx-auto">
      <router-view />
    </div>
  </div>
</template>

<script>

import Header from "@/components/header.vue";

export default {
  components: {
    Header
  }
}
</script>