<script setup>
  import { ref, watch } from 'vue'

  // state
  const rootFontSize = 16
  const valuePx = ref(16)
  const valueRem = ref(1)
  let timeout = null

  // watch for changes in pixels and update rem
  watch(valuePx, (newPx) => {
    clearTimeout(timeout)
    timeout = setTimeout(() => {
      if (newPx === '' || isNaN(newPx)) {
        resetValues()
      } else {
        valueRem.value = parseFloat(newPx) / rootFontSize
      }
    }, 500)
  })

  // watch for changes in rem and update pixels
  watch(valueRem, (newRem) => {
    clearTimeout(timeout)
    timeout = setTimeout(() => {
      if (newRem === '' || isNaN(newRem)) {
        resetValues()
      } else {
        valuePx.value = parseFloat(newRem) * rootFontSize
      }
    }, 500)
  })

  // reset if input is empty
  const resetValues = () => {
    valuePx.value = 16
    valueRem.value = 1
  }

  // select the text when input is focused (makes it easy to copy or change all)
  const selectText = (event) => {
    event.target.select()
  }
</script>

<template>
  <div class="component-container">
    <h2 class="text-md">PX to REM</h2>

    <!-- form -->
    <div class="grid-x grid-padding-x form-general m-b-0">
      <div class="cell medium-6">
        <label for="valPx">pixels</label>
        <input
          id="valPx"
          v-model.number="valuePx"
          type="number"
          @focus="selectText"
          @blur="valuePx === '' ? resetValues() : null"
        />
      </div>
      <div class="cell medium-6">
        <label for="valRem">rem</label>
        <input
          id="valRem"
          v-model.number="valueRem"
          type="number"
          @focus="selectText"
          @blur="valueRem === '' ? resetValues() : null"
        />
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
