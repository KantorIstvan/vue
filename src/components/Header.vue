<template>
  <header class="bg-white border-b border-gray-200 shadow-sm">
    <div class="px-6 py-4 flex items-center justify-between">
      <div class="flex items-center space-x-4">
        <div class="w-8 h-8 bg-gradient-to-br from-blue-500 to-purple-600 rounded-lg flex items-center justify-center">
          <span class="text-white text-sm font-bold">D</span>
        </div>
        <div>
          <h1 class="text-2xl font-bold text-gray-900">Dashboard</h1>
          <p class="text-sm text-gray-500">Welcome to your workspace</p>
        </div>
      </div>

      <div class="flex items-center space-x-4">
        <button
          @click="login"
          v-if="!isLoggedIn"
          class="flex items-center space-x-2 px-4 py-2 bg-blue-600 hover:bg-blue-700 text-white font-medium rounded-lg transition-all duration-200 shadow-sm hover:shadow-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
          <span class="text-lg">🔐</span>
          <span>Sign In</span>
        </button>

        <div v-else class="flex items-center space-x-3">
          <div class="flex items-center space-x-2 px-4 py-2 bg-green-50 border border-green-200 rounded-lg">
            <div class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></div>
            <span class="text-green-700 font-medium">Welcome back!</span>
          </div>

          <div class="w-8 h-8 bg-gradient-to-br from-green-400 to-blue-500 rounded-full flex items-center justify-center">
            <span class="text-white text-sm font-bold">U</span>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref } from 'vue'

const isLoggedIn = ref(false)

const login = () => {
  console.log('Login clicked...')
  // Add login logic here
  isLoggedIn.value = true
}
</script>
