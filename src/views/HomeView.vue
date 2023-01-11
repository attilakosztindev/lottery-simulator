<script setup>
import { computed, ref, onMounted, watch } from 'vue'
import slider from 'vue3-slider'
import AppCheckbox from '@/components/AppCheckbox'
import AppPage from '@/components/AppPage'
import AppValidationBox from '@/components/AppValidationBox'

onMounted(() => {
  countMatches(generatedCryptoNumbers.value, inputNumbers.value)
  if (isAuto.value) inputNumbers.value = generateCryptoNumbers()
})

const generatedCryptoNumbers = ref(new Array(5).fill(0))
const inputNumbers = ref([1, 2, 3, 4, 5])
const isAuto = ref(false)
const generationSpeed = ref(1000)
const numberOfTickets = ref(0)
let intervalId = null
const matches = ref([
  {
    label: '2 matches',
    value: 0
  },
  {
    label: '3 matches',
    value: 0
  },
  {
    label: '4 matches',
    value: 0
  },
  {
    label: '5 matches',
    value: 0
  }
])

const totalCost = computed(() => {
  return numberOfTickets.value * 300
})
const yearsSpent = computed(() => {
  return Math.floor(numberOfTickets.value / 52)
})
const summary = computed(() => {
  return [
    {
      label: 'Number of tickets:',
      value: formatNumber(numberOfTickets.value)
    },
    {
      label: 'Years spent:',
      value: yearsSpent.value
    },
    {
      label: 'Cost of tickets:',
      value: formatCurrency(totalCost.value)
    }
  ]
})

const itemClass = computed(() => ({
  'result--summary-item-win': matches.value[matches.value.length - 1].value > 0
}))

const inputClass = (number) => {
  const uniqueNumber =
    inputNumbers.value.filter((n) => n === number).length === 1
  if (number < 1 || number > 90 || !uniqueNumber) {
    return 'result--input-number-error'
  }
}
watch(isAuto, (val) => {
  if (val) {
    inputNumbers.value = generateCryptoNumbers()
    updateInterval(generationSpeed.value)
  }
})

watch(generationSpeed, (val) => {
  updateInterval(val)
})

const formatNumber = (val) => {
  return val
    .toString()
    .toString()
    .replace(/\B(?=(\d{3})+(?!\d))/g, ' ')
}

const formatCurrency = (val) => {
  return new Intl.NumberFormat('hu-HU', {
    style: 'currency',
    currency: 'HUF'
  }).format(val)
}
const validateInputNumbers = () => {
  if (inputNumbers.value.length !== 5) return false
  for (const number of inputNumbers.value) {
    if (number < 1 || number > 90) return false
  }
  const numberSet = new Set(inputNumbers.value)
  return numberSet.size === inputNumbers.value.length
}

const generateCryptoNumbers = () => {
  const numbers = new Set()
  while (numbers.size < 5) {
    const array = new Uint8Array(1)
    window.crypto.getRandomValues(array)
    numbers.add((array[0] % 90) + 1)
  }
  return Array.from(numbers).sort((a, b) => a - b)
}

const countMatches = (lotteryNumbers, inputNumbers) => {
  let count = 0
  for (let i = 0; i < lotteryNumbers.length; i++) {
    if (lotteryNumbers[i] === inputNumbers[i]) {
      count++
    }
  }
  updateInterval(generationSpeed.value)
  if (count >= 2 && count <= 5) {
    matches.value[count - 2].value++
  }
  if (count === 5) clearInterval(intervalId)
  numberOfTickets.value++
}

const updateInterval = (speed) => {
  clearInterval(intervalId)
  if (generatedCryptoNumbers.value !== inputNumbers.value) {
    intervalId = setInterval(() => {
      generatedCryptoNumbers.value = generateCryptoNumbers()
      if (isAuto.value || validateInputNumbers) {
        countMatches(generatedCryptoNumbers.value, inputNumbers.value)
      }
    }, speed)
  }
}
</script>

<template lang="pug">
app-page
  template.home-view(#pageContent)
    section.result
      h1.result--title Result
      section.result--summary
        article.result--summary-row(v-for="(data, index) in summary" :key="index")
          label.result--summary-item {{ data.label }}
          p.result--summary-item(:class="itemClass") {{ data.value }}
      section.result--matches
        article.result--match(v-for="(match, index) in matches" :key="index")
          label.result--match-label {{match.label}}
          p.result--match-value {{match.value}}
      .section.result--generated
        label.result--generated-label Winning numbers:
        .result--generated-numbers
          input.result--generated-number(v-for="number in generatedCryptoNumbers" :value="number" type="number" readonly)
      section.result--input
        label.result--input-label Your numbers:
        section.result--input-numbers
          input.result--input-number(v-for="(number, index) in inputNumbers" v-model="inputNumbers[index]" :key="index" type="number" :class="inputClass(number)" @input="validateInputNumbers()" :readonly="isAuto")
      app-validation-box(:rule="!validateInputNumbers()" msg="Each input number should be unique and between 1 and 90!")
      section.result--auto
        label.result--auto-label Play with random numbers:
        app-checkbox.result--auto-checkbox(v-model:value="isAuto")
      section.result--slide
        label.result--slide-label Speed
        slider.result--slide-slider(v-model="generationSpeed" :min="1" :max="1000" color="#A5D9C8" track-color="#E9F5F1" :height="4" always-show-handle sticky)
</template>

<style lang="sass">
.result
  @include box-shadow(2px 2px 10px rgba(0, 0, 0, 0.1))
  border-radius: 24px
  max-width: 792px
  width: 100%
  background: #fff
  padding: 48px 78px
  @media (max-width: 600px)
    width: initial
    border-radius: 2px
    padding: 16px 16px 32px 16px
  .result--title
    color: $custom-black
    margin-bottom: 32px
    font-size: 32px !important
    line-height: 44px
  .result--summary
    display: flex
    flex-direction: column
    background-color: $custom-green
    border-radius: 10px
    padding: 18px 19px 11px 24px
    color: #fff
    margin-bottom: 32px
    & > :not(:last-child)
      margin-bottom: 6px
    @media (min-width: 601px)
      max-width: 325px
    & > .result--summary-row:nth-child(2) > .result--summary-item-win
      font-weight: 800 !important
    .result--summary-row
      display: flex
      align-items: center
      grid-gap: 24px
      font-weight: 700
      font-size: 14px
      line-height: 19px
      @media (max-width: 600px)
        grid-gap: 19px
      label
        min-width: 140px
      &:first-child
        line-height: 22px !important
        font-size: 16px !important
        font-weight: 800 !important
        @media (max-width: 600px)
          font-size: 14px
          line-height: 19px
  .result--matches
    display: grid
    grid-template-columns: repeat(4, 1fr)
    border-radius: 10px
    max-width: 508px
    margin-bottom: 32px
    @include box-shadow(2px 2px 10px rgba(0, 0, 0, 0.1))
    @media (max-width: 600px)
      grid-template-columns: repeat(2, 1fr)
    $parts: 4
    @for $i from 1 through $parts
      .result--match:nth-child(#{$i})
        @if $i == 1
          border-right: 1px solid $custom-yellow
          @media (max-width: 600px)
            border-bottom: 1px solid $custom-yellow
        @else if $i == 2
          border-right: 1px solid $custom-yellow
          @media (max-width: 600px)
            border-right: none
            border-bottom: 1px solid $custom-yellow
        @else if $i == 3
          border-right: 1px solid $custom-yellow
    .result--match
      height: 72px
      flex-direction: column
      @include flex-center
      .result--match-label
        font-weight: 700
        font-size: 12px
        line-height: 16px
        color: $custom-black
        margin-bottom: 9px
      .result--match-value
        font-weight: 800
        font-size: 16px
        line-height: 22px
        color: $custom-black
  .result--generated
    margin-bottom: 24px
  .result--input
    margin-bottom: 10px
  .result--generated, .result--input
    display: flex
    justify-content: space-between
    max-width: 394px
    align-items: center
    .result--generated-numbers, .result--input-numbers
      display: flex
      grid-gap: 16px
      @media (max-width: 375px)
        grid-gap: 10px
      .result--input-number-error
        border: 1px solid red !important
      .result--generated-number, .result--input-number
        background: #FFFFFF
        border: 1px solid $custom-green
        border-radius: 10px
        width: 34px
        height: 38px
        text-align: center
        font-size: 16px
        transition: border .4s
        @media (max-width: 600px)
          font-size: 12px
          width: 22px
          height: 25px
          border-radius: 5px
        @include box-shadow(2px 2px 10px rgba(0, 0, 0, 0.1))
    .result--generated-label, .result--input-label
      font-size: 16px
      line-height: 22px
      color: $custom-black
      @media (max-width: 600px)
        font-size: 12px
  .result--auto
    margin-bottom: 18px
    display: flex
    align-items: center
    .result--auto-label
      margin-right: 57px
      font-size: 16px
      line-height: 22px
      color: $custom-black
      @media (max-width: 600px)
        margin-right: 27px
        font-size: 12px
  .result--slide
    display: flex
    flex-direction: column
    width: calc(100% - 10px)
    .result--slide-label
      margin-bottom: 11px
      font-size: 16px
      line-height: 22px
      color: $custom-black
      @media (max-width: 600px)
        font-size: 12px
    .result--slide-slider
      .track-filled
        height: 10px
        @include transform(translateY(-50%))
        top: 50%
        border-radius: 10px 0 0 10px
      .handle
        @include transform(translateY(-50%))
        top: 50%
        width: 20px
        height: 20px
        border-radius: 100%
        border: solid 1px $custom-green
        background-color: white
        @media (max-width: 600px)
          @include transform(translate(-3px, -50%))
</style>
