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
            <!-- Service packs header icon removed -->
          </div>
        </div>
      </div>
    </div>

    <!-- Stats Overview -->
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
    icon: '',
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
    icon: '',
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
    icon: '',
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
