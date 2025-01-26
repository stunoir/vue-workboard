<script setup>
  import ToDoList from '@/components/ToDoList.vue'
</script>

<template>
  <div class="wrapper-section wrapper-section--white">
    <div class="grid-container">
      <div class="grid-x grid-padding-x">
        <div class="cell medium-12">
          <ToDoList view="weekly" />
          <ToDoList view="monthly" />
        </div>
      </div>
    </div>
  </div>
</template>
