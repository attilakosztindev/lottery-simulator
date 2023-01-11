<script setup>
import AppHeader from '@/components/AppHeader'
</script>

<template lang="pug">
div
  app-header
  router-view
</template>

<style lang="sass">
#app
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
</style>
