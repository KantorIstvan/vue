<template>
  <div class="max-w-7xl mx-auto space-y-6">
    <!-- Page Header -->
    <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
      <div class="flex items-center justify-between">
        <div>
          <h2 class="text-3xl font-bold text-gray-900">Service Packs</h2>
          <p class="text-gray-600 mt-1">Manage your service packages and offerings</p>
        </div>
        <div class="hidden md:block">
          <div class="w-16 h-16 bg-gradient-to-br from-purple-500 to-pink-600 rounded-2xl flex items-center justify-center shadow-lg">
            <span class="text-white text-2xl">📦</span>
          </div>
        </div>
      </div>
    </div>

    <!-- Stats Overview -->
    <div class="grid grid-cols-1 md:grid-cols-4 gap-6">
      <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
        <div class="flex items-center">
          <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
            <span class="text-2xl">📊</span>
          </div>
          <div class="ml-4">
            <p class="text-sm font-medium text-gray-600">Total Packs</p>
            <p class="text-2xl font-bold text-gray-900">{{ stats.totalPacks }}</p>
          </div>
        </div>
      </div>

      <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
        <div class="flex items-center">
          <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center">
            <span class="text-2xl">✅</span>
          </div>
          <div class="ml-4">
            <p class="text-sm font-medium text-gray-600">Active Packs</p>
            <p class="text-2xl font-bold text-gray-900">{{ stats.activePacks }}</p>
          </div>
        </div>
      </div>

      <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
        <div class="flex items-center">
          <div class="w-12 h-12 bg-yellow-100 rounded-lg flex items-center justify-center">
            <span class="text-2xl">💰</span>
          </div>
          <div class="ml-4">
            <p class="text-sm font-medium text-gray-600">Revenue</p>
            <p class="text-2xl font-bold text-gray-900">${{ stats.revenue.toLocaleString() }}</p>
          </div>
        </div>
      </div>

      <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
        <div class="flex items-center">
          <div class="w-12 h-12 bg-purple-100 rounded-lg flex items-center justify-center">
            <span class="text-2xl">👥</span>
          </div>
          <div class="ml-4">
            <p class="text-sm font-medium text-gray-600">Subscribers</p>
            <p class="text-2xl font-bold text-gray-900">{{ stats.subscribers }}</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Service Packs Grid -->
    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
      <div
        v-for="pack in servicePacks"
        :key="pack.id"
        class="bg-white rounded-xl shadow-sm border border-gray-200 overflow-hidden hover:shadow-md transition-all duration-200"
        :class="{ 'ring-2 ring-blue-500 ring-opacity-50': pack.featured }"
      >
        <!-- Pack Header -->
        <div class="p-6 pb-0">
          <div class="flex items-center justify-between mb-4">
            <div class="flex items-center space-x-3">
              <div :class="pack.iconBg" class="w-12 h-12 rounded-lg flex items-center justify-center">
                <span class="text-2xl">{{ pack.icon }}</span>
              </div>
              <div>
                <h3 class="text-xl font-bold text-gray-900">{{ pack.name }}</h3>
                <p class="text-sm text-gray-600">{{ pack.category }}</p>
              </div>
            </div>
            <div v-if="pack.featured" class="px-3 py-1 bg-blue-100 text-blue-800 text-xs font-medium rounded-full">
              Popular
            </div>
          </div>

          <p class="text-gray-600 mb-4">{{ pack.description }}</p>

          <div class="flex items-baseline mb-4">
            <span class="text-3xl font-bold text-gray-900">${{ pack.price }}</span>
            <span class="text-gray-600 ml-2">/{{ pack.billing }}</span>
          </div>
        </div>

        <!-- Features List -->
        <div class="px-6 pb-6">
          <ul class="space-y-2">
            <li
              v-for="feature in pack.features"
              :key="feature"
              class="flex items-center text-sm text-gray-600"
            >
              <span class="text-green-500 mr-2">✓</span>
              {{ feature }}
            </li>
          </ul>

          <div class="mt-6 flex items-center justify-between">
            <div class="flex items-center space-x-2">
              <div class="w-2 h-2 rounded-full" :class="pack.status === 'active' ? 'bg-green-500' : 'bg-gray-400'"></div>
              <span class="text-sm font-medium" :class="pack.status === 'active' ? 'text-green-700' : 'text-gray-500'">
                {{ pack.status === 'active' ? 'Active' : 'Inactive' }}
              </span>
            </div>
            <span class="text-sm text-gray-500">{{ pack.subscribers }} subscribers</span>
          </div>
        </div>

        <!-- Pack Actions -->
        <div class="px-6 py-4 bg-gray-50 border-t border-gray-200">
          <div class="flex space-x-3">
            <button
              class="flex-1 px-4 py-2 bg-blue-600 hover:bg-blue-700 text-white font-medium rounded-lg transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
            >
              Edit Pack
            </button>
            <button
              class="px-4 py-2 text-gray-600 hover:text-gray-800 border border-gray-300 hover:border-gray-400 rounded-lg transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-gray-500 focus:ring-offset-2"
            >
              View Details
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Action Buttons -->
    <div class="flex flex-col sm:flex-row gap-4">
      <button class="flex items-center justify-center space-x-2 px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white font-medium rounded-lg transition-all duration-200 shadow-sm hover:shadow-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
        <span class="text-lg">➕</span>
        <span>Create New Pack</span>
      </button>
      <button class="flex items-center justify-center space-x-2 px-6 py-3 bg-gray-600 hover:bg-gray-700 text-white font-medium rounded-lg transition-all duration-200 shadow-sm hover:shadow-md focus:outline-none focus:ring-2 focus:ring-gray-500 focus:ring-offset-2">
        <span class="text-lg">📊</span>
        <span>View Analytics</span>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const stats = ref({
  totalPacks: 12,
  activePacks: 8,
  revenue: 24750,
  subscribers: 1234
})

const servicePacks = ref([
  {
    id: 1,
    name: 'Starter Pack',
    category: 'Basic',
    description: 'Perfect for small businesses getting started with our services.',
    price: 29,
    billing: 'month',
    icon: '🚀',
    iconBg: 'bg-blue-100',
    status: 'active',
    subscribers: 156,
    featured: false,
    features: [
      'Up to 5 users',
      'Basic analytics',
      'Email support',
      '10GB storage',
      'Standard templates'
    ]
  },
  {
    id: 2,
    name: 'Professional Pack',
    category: 'Business',
    description: 'Advanced features for growing businesses and teams.',
    price: 79,
    billing: 'month',
    icon: '💼',
    iconBg: 'bg-purple-100',
    status: 'active',
    subscribers: 234,
    featured: true,
    features: [
      'Up to 25 users',
      'Advanced analytics',
      'Priority support',
      '100GB storage',
      'Custom templates',
      'API access'
    ]
  },
  {
    id: 3,
    name: 'Enterprise Pack',
    category: 'Enterprise',
    description: 'Complete solution for large organizations with custom needs.',
    price: 199,
    billing: 'month',
    icon: '🏢',
    iconBg: 'bg-green-100',
    status: 'active',
    subscribers: 89,
    featured: false,
    features: [
      'Unlimited users',
      'Real-time analytics',
      'Dedicated support',
      'Unlimited storage',
      'White-label solution',
      'Custom integrations'
    ]
  }
])
</script>
