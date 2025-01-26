<script setup>
  import { RouterView } from 'vue-router'
  import SiteHeader from './components/SiteHeader.vue'
</script>

<template>
  <SiteHeader />
  <main>
    <router-view v-slot="{ Component }">
      <transition name="fade">
        <component :is="Component" />
      </transition>
    </router-view>
  </main>
</template>

<style scoped>
  /* transition animations */
  .fade-enter-active {
    transition: opacity 1s ease;
  }
  .fade-enter-from {
    opacity: 0;
  }
  .fade-leave-active {
    transition: opacity 0 ease;
  }
  .fade-leave-to {
    opacity: 0;
  }
</style>
