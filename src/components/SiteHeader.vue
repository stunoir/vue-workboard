<script setup>
  import { RouterLink } from 'vue-router'
</script>

<template>
  <header class="wrapper-header">
    <div class="grid-container">
      <div class="grid-x grid-padding-x">
        <div class="cell medium-6">
          <div class="profile-card">
            <RouterLink href="/" class="pc-img">
              <img alt="workboard homepage" src="@/assets/img/layout/strike-s.svg" />
            </RouterLink>
            <div class="pc-content">
              <h1 class="pc-title">stuart's workboard</h1>
            </div>
          </div>
        </div>
        <div class="cell medium-6 align-self-middle">
          <div class="flex-container flex-gap-15 align-right">
            <RouterLink class="btn-main btn-main--ghost btn-main--xs" to="/">workboard</RouterLink>
            <RouterLink class="btn-main btn-main--ghost btn-main--xs" to="/week">week/month</RouterLink>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<style scoped>
  /* active link colours */
  .btn-main.router-link-exact-active {
    background-color: #333;
    color: #fff;
    border-color: #333;
  }
</style>
