<script setup>
import { ref, provide } from 'vue'
import Sidebar from './components/Sidebar.vue'
import Header from './components/Header.vue'
import Profile from './components/Profile.vue'
import ServicePacks from './components/ServicePacks.vue'
import Subscriptions from './components/Subscriptions.vue'

const currentPage = ref('profile')

const setCurrentPage = (page) => {
  currentPage.value = page
}

// Provide the navigation function to child components
provide('setCurrentPage', setCurrentPage)
</script>

<template>
  <div class="flex h-screen bg-gray-50">
    <!-- Fixed Sidebar -->
    <Sidebar :currentPage="currentPage" @navigate="setCurrentPage" />

    <!-- Main Content Area -->
    <div class="flex-1 flex flex-col">
      <Header />
      <main class="flex-1 overflow-auto">
        <div class="p-6">
          <Profile v-if="currentPage === 'profile'" />
          <ServicePacks v-if="currentPage === 'service-packs'" />
          <Subscriptions v-if="currentPage === 'subscriptions'" />
        </div>
      </main>
    </div>
  </div>
</template>

<style>
/* Global styles to override default constraints */
#app {
  max-width: none !important;
  margin: 0 !important;
  padding: 0 !important;
  display: block !important;
  grid-template-columns: none !important;
}

body {
  margin: 0;
  padding: 0;
  display: block !important;
  place-items: initial !important;
}

* {
  box-sizing: border-box;
}
</style>
