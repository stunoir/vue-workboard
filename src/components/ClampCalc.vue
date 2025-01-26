<script setup>
  import { ref, watch } from 'vue'

  // state
  const minView = ref(320)
  const maxView = ref(1440)
  const minSize = ref(1)
  const maxSize = ref(3)
  const outputClamp = ref('')

  let timeout = null
  const rootFontSize = 16

  // debounce calculations - essentially delay every input and re-clear on a change
  const debounce = (fn, delay) => {
    clearTimeout(timeout)
    timeout = setTimeout(fn, delay)
  }

  // calculate clamp()
  const calculateClamp = () => {
    const minVRem = parseFloat(minView.value) / rootFontSize
    const maxVRem = parseFloat(maxView.value) / rootFontSize
    const minS = parseFloat(minSize.value)
    const maxS = parseFloat(maxSize.value)

    const slope = ((maxS - minS) / (maxVRem - minVRem)) * 100
    const intercept = minS - (slope / 100) * minVRem

    outputClamp.value = `clamp(${minS}rem, ${intercept.toFixed(4)}rem + ${slope.toFixed(4)}vw, ${maxS}rem)`
  }

  // watch inputs and recalculate on change with debounce, 'immediate' to run right away for initial calc
  watch(
    [minView, maxView, minSize, maxSize],
    () => {
      debounce(calculateClamp, 500)
    },
    { immediate: true }
  )

  // select the text when input is focused (makes it easy to copy or change all)
  const selectText = (event) => {
    event.target.select()
  }
</script>

<template>
  <div class="component-container">
    <h2 class="text-md">Clamp Calc</h2>

    <div class="form-general m-b-0">
      <div class="grid-x grid-padding-x">
        <div class="cell medium-6">
          <label for="minView">min viewport (px)</label>
          <input id="minView" v-model="minView" type="number" @focus="selectText" />
        </div>
        <div class="cell medium-6">
          <label for="maxView">max viewport (px)</label>
          <input id="maxView" v-model="maxView" type="number" @focus="selectText" />
        </div>
        <div class="cell medium-6">
          <label for="minSize">min size (rem)</label>
          <input id="minSize" v-model="minSize" type="number" @focus="selectText" />
        </div>
        <div class="cell medium-6">
          <label for="maxSize">max size (rem)</label>
          <input id="maxSize" v-model="maxSize" type="number" @focus="selectText" />
        </div>
      </div>
      <div class="cell medium-12">
        <h3 class="text-sm m-b-1">css output</h3>
        <label for="outputClamp" class="show-for-sr">clamp output</label>
        <input id="outputClamp" v-model="outputClamp" type="text" @focus="selectText" />
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
