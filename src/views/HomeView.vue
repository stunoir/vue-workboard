<script setup>
  import ToDoList from '@/components/ToDoList.vue'
  import PxToRemCalc from '@/components/PxToRemCalc.vue'
  import ClampCalc from '@/components/ClampCalc.vue'
  import LinksList from '@/components/LinksList.vue'
</script>

<template>
  <div class="wrapper-section wrapper-section--white">
    <div class="grid-container">
      <div class="grid-x grid-row-gap grid-padding-x">
        <div class="cell large-7">
          <ToDoList />
        </div>
        <div class="cell large-5">
          <PxToRemCalc />
          <ClampCalc />
          <LinksList />
        </div>
      </div>
    </div>
  </div>
</template>
