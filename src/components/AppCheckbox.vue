<script setup>
import { useVModel } from '@/composables/useVModel'
import { defineProps } from 'vue'

const props = defineProps({ value: { type: Boolean, required: true } })
const value = useVModel(props, 'value')

const updateValue = () => {
  console.log(value.value)
  value.value = !value.value
}
</script>
<template lang="pug">
.app-checkbox
  span.checkbox--custom(v-if="value")
  input(type="checkbox" v-model="value" @click="updateValue")
</template>

<style lang="sass">
.app-checkbox
  position: relative
  border: 1px solid $custom-black
  border-radius: 5px
  height: 32px
  width: 32px
  @include box-shadow(2px 2px 10px rgba(0, 0, 0, 0.1))
  @media (max-width: 600px)
    height: 20px
    width: 20px
  input[type="checkbox"]
    position: absolute !important
    opacity: 0 !important
    cursor: pointer !important
    height: 100%
    width: 100%
  .checkbox--custom
    position: absolute
    width: 18px
    height: 14px
    background-repeat: no-repeat no-repeat
    background-position: center center
    background-size: cover
    top: 50%
    left: 50%
    @include transform(translate(-50%, -50%))
    @include background-image(url("data:image/svg+xml,%3Csvg width='18' height='14' viewBox='0 0 18 14' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1 7L6 12L16.5 1.5' stroke='%23020056' stroke-width='2'/%3E%3C/svg%3E"))
    @media (max-width: 600px)
      width: 14px
      height: 14px
      @include background-image(url("data:image/svg+xml,%3Csvg width='14' height='14' viewBox='0 0 14 14' fill='none' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Crect width='14' height='14' fill='url(%23pattern0)'/%3E%3Cdefs%3E%3Cpattern id='pattern0' patternContentUnits='objectBoundingBox' width='1' height='1'%3E%3Cuse xlink:href='%23image0_10_92' transform='scale(0.0104167)'/%3E%3C/pattern%3E%3Cimage id='image0_10_92' width='96' height='96' xlink:href='data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAGAAAABgCAYAAADimHc4AAAABmJLR0QA/wD/AP+gvaeTAAABZElEQVR4nO3ZsUoDQRiF0ftQWllYKSn0jVJY+rKCCBKstNAlQaLJZmf3j845sP343ZHVJAEAAAAAAAAAOBOrJOvqQ/TqNskmyXuSx+KzdGc3/vAYYSH74hthIb/FN8LMVjkcf3i8mBs75uYPz1uSu5pj/k/iFxK/kPiFxC8kfiHxC4lfSPxC4hcSv5D4hcQvJH4h8QuJX0j8Ql3GX+fzK7xqY75G3OQ8zjzZQ7a36b7wHF3e/CH+7g9WMYL4qRtB/D3PUiN0GX+d83jJdfnCTcbfujl+E7q8+bsqR+g+/qBiBPG/WXIE8X+wxAjiHzDnCOIfaY4RxB+p5Qjin6jFCOJPNGUE8Rs5ZQTxGxv7eU2Xn+3MbcytdvNn0moE8SeYOoL4DZw6gvgNjR1B/BkcO4L4Mzo0gvgL+On/BH/nL+g6yUu28V+T3JSeqEOXSZ6SPCe5Kj5Lty6+HgAAAAAAAAAA/rQPBtXeBBmHu/sAAAAASUVORK5CYII='/%3E%3C/defs%3E%3C/svg%3E"))
</style>
