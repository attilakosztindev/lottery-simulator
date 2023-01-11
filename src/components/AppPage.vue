<template lang="pug">
main.app-page
  slot(name="pageContent")
</template>

<style lang="sass">
.app-page
  min-height: calc(100vh - 60px)
  background-color: #E5E5E5
  padding: 24px 24px 24px 16px
  @media (min-width: 601px)
    @include flex-center
</style>
