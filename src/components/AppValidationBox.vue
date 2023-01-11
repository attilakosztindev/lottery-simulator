<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  msg: { type: String, required: true },
  rule: { type: Boolean, required: true }
})
</script>

<template lang="pug">
.app-validation
  Transition(name="slide-fade")
    .validation-box(v-if="rule")
      .validation-box--icon
      p.validation-box--message {{props.msg}}
</template>

<style lang="sass">
.app-validation
  min-height: 42px
  @media (max-width: 600px)
    max-width: 300px
  .validation-box
    display: flex
    align-items: center
    grid-gap: 10px
    margin-bottom: 18px
    .validation-box--icon
      height: 24px
      width: 24px
      background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 512 512'%3E%3Cpath fill='red' d='M256 32c14.2 0 27.3 7.5 34.5 19.8l216 368c7.3 12.4 7.3 27.7 .2 40.1S486.3 480 472 480H40c-14.3 0-27.6-7.7-34.7-20.1s-7-27.8 .2-40.1l216-368C228.7 39.5 241.8 32 256 32zm0 128c-13.3 0-24 10.7-24 24V296c0 13.3 10.7 24 24 24s24-10.7 24-24V184c0-13.3-10.7-24-24-24zm32 224c0-17.7-14.3-32-32-32s-32 14.3-32 32s14.3 32 32 32s32-14.3 32-32z'/%3E%3C/svg%3E")
      background-repeat: no-repeat no-repeat
      background-position: center center
    .validation-box--message
      color: red
      font-size: 16px
      @media (max-width: 600px)
        font-size: 12px
  .slide-fade-enter-active
    transition: all 0.3s ease-out
  .slide-fade-leave-active
    transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1)
  .slide-fade-enter-from,
  .slide-fade-leave-to
    @include transform(translateY(-10px))
    opacity: 0
</style>
