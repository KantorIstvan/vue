<template>
  <div class="bg-eerie_black-500 w-72 h-screen p-6 border-r shadow-sm transition-all duration-300 flex flex-col">
    <div class="mb-8">
      <h2 class="text-2xl font-bold text-seasalt border-gray-100">Service Manager</h2>
    </div>

    <nav class="flex-1 mb-8">
      <div>
        <p class="text-sm font-semibold text-seasalt-200 uppercase tracking-wide mb-4">Navigation</p>
        <ul class="space-y-2">
          <li>
            <a href="#" @click.prevent="navigate('profile')"
               :class="{
                 'bg-seasalt text-eerie_black-500 border-l-4 border-seasalt-300': currentPage === 'profile',
                 'text-gray-500 hover:bg-gray-50 hover:text-gray-700': currentPage !== 'profile'
               }"
               class="flex items-center px-4 py-3 rounded-lg transition-all duration-200 font-medium group hover:translate-x-1 hover:shadow-sm">
              <div class="mr-3 flex items-center justify-center w-6 h-6">
              </div>
              <span>Profile</span>
            </a>
          </li>
          <li>
            <a href="#" @click.prevent="navigate('service-packs')"
               :class="{
                 'bg-seasalt text-eerie_black-500 border-l-4 border-seasalt-300': currentPage === 'service-packs',
                 'text-gray-500 hover:bg-gray-50 hover:text-gray-700': currentPage !== 'service-packs'
               }"
               class="flex items-center px-4 py-3 rounded-lg transition-all duration-200 font-medium group hover:translate-x-1 hover:shadow-sm">
              <div class="mr-3 flex items-center justify-center w-6 h-6">
              </div>
              <span>Service Packs</span>
            </a>
          </li>
          <li>
            <a href="#" @click.prevent="navigate('subscriptions')"
               :class="{
                 'bg-seasalt text-eerie_black-500 border-l-4 border-seasalt-300': currentPage === 'subscriptions',
                 'text-gray-500 hover:bg-gray-50 hover:text-gray-700': currentPage !== 'subscriptions'
               }"
               class="flex items-center px-4 py-3 rounded-lg transition-all duration-200 font-medium group hover:translate-x-1 hover:shadow-sm">
              <div class="mr-3 flex items-center justify-center w-6 h-6">
              </div>
              <span>Subscriptions</span>
            </a>
          </li>
        </ul>
      </div>
    </nav>

    <div class="mt-auto">
      <button @click="logout"
              class="flex items-center w-full px-4 py-3 rounded-lg text-red-600 font-medium cursor-pointer transition-all duration-200 hover:bg-red-100 hover:border-red-300 hover:-translate-y-0.5 hover:shadow-md active:translate-y-0 active:shadow-sm group focus:outline-none focus:ring-2 focus:ring-red-600 focus:ring-offset-2">
        <div class="mr-3 flex items-center justify-center w-6 h-6">
        </div>
        <span>Sign Out</span>
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  currentPage: {
    type: String,
    default: 'profile'
  }
})

const emit = defineEmits(['navigate'])

const navigate = (page) => {
  emit('navigate', page)
}

const logout = () => {
  console.log('Logging out...')
  // Add logout logic here
}
</script>
