<template lang="pug">
header.app-header
  .app-header--icon
  h1.app-header--title Lottery simulator
</template>

<style lang="sass">
.app-header
  display: flex
  color: white
  align-items: center
  height: 60px
  @include linear-gradient(#A5D9C8, (270deg, #F6F0C6 0%, #D9135D 0.01%, rgba(214, 19, 92, 0.996895) 0.02%, #F6F0C6 0.03%, #A6D9C8 80.73%, #A5D9C8 100%))
  .app-header--icon
    height: 29px
    width: 28px
    margin: 0 16px 0 20px
    @include background-image(url("data:image/svg+xml,%3Csvg width='28' height='29' viewBox='0 0 28 29' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M27.9283 12.8135H16.1097V0.0852661L11.8888 4.49772V12.8135H0.0701904V17.0562H11.8888V28.9358H16.1097V17.0562H27.9283V12.8135Z' fill='white'/%3E%3C/svg%3E"))
    background-repeat: no-repeat no-repeat
    background-position: center center
    background-size: cover
  .app-header--title
    color: #fff
    font-size: 40px
    line-height: 55px
    @media (max-width: 600px)
      font-size: 20px
      line-height: 27px
</style>
