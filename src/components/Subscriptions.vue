<template>
  <div class="max-w-6xl mx-auto space-y-6">
    <!-- Page Header -->
    <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
      <div class="flex items-center justify-between">
        <div>
          <h2 class="text-3xl font-bold text-gray-900">Subscriptions</h2>
          <p class="text-gray-600 mt-1">View and manage your active subscriptions</p>
        </div>
        <div class="hidden md:block">
          <div class="w-16 h-16 bg-gradient-to-br from-green-500 to-teal-600 rounded-2xl flex items-center justify-center shadow-lg">
            <span class="text-white text-2xl">💳</span>
          </div>
        </div>
      </div>
    </div>

    <!-- Subscription Overview Cards -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
      <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
        <div class="flex items-center">
          <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
            <span class="text-2xl">📊</span>
          </div>
          <div class="ml-4">
            <p class="text-sm font-medium text-gray-600">Active Subscriptions</p>
            <p class="text-2xl font-bold text-gray-900">{{ overview.active }}</p>
          </div>
        </div>
      </div>

      <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
        <div class="flex items-center">
          <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center">
            <span class="text-2xl">💰</span>
          </div>
          <div class="ml-4">
            <p class="text-sm font-medium text-gray-600">Monthly Spend</p>
            <p class="text-2xl font-bold text-gray-900">${{ overview.monthlySpend }}</p>
          </div>
        </div>
      </div>

      <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
        <div class="flex items-center">
          <div class="w-12 h-12 bg-yellow-100 rounded-lg flex items-center justify-center">
            <span class="text-2xl">📅</span>
          </div>
          <div class="ml-4">
            <p class="text-sm font-medium text-gray-600">Next Billing</p>
            <p class="text-lg font-bold text-gray-900">{{ overview.nextBilling }}</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Current Subscriptions -->
    <div class="bg-white rounded-xl shadow-sm border border-gray-200">
      <div class="p-6 border-b border-gray-200">
        <div class="flex items-center justify-between">
          <h3 class="text-xl font-semibold text-gray-900">Current Subscriptions</h3>
          <button class="flex items-center space-x-2 px-4 py-2 bg-blue-600 hover:bg-blue-700 text-white font-medium rounded-lg transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
            <span class="text-sm">➕</span>
            <span>Add New</span>
          </button>
        </div>
      </div>

      <div class="divide-y divide-gray-200">
        <div
          v-for="subscription in subscriptions"
          :key="subscription.id"
          class="p-6 hover:bg-gray-50 transition-colors duration-150"
        >
          <div class="flex items-center justify-between">
            <div class="flex items-center space-x-4">
              <div :class="subscription.iconBg" class="w-12 h-12 rounded-lg flex items-center justify-center">
                <span class="text-xl">{{ subscription.icon }}</span>
              </div>
              <div>
                <h4 class="text-lg font-semibold text-gray-900">{{ subscription.name }}</h4>
                <p class="text-sm text-gray-600">{{ subscription.description }}</p>
                <div class="flex items-center mt-2 space-x-4">
                  <div class="flex items-center space-x-2">
                    <div class="w-2 h-2 rounded-full" :class="getStatusColor(subscription.status)"></div>
                    <span class="text-sm font-medium" :class="getStatusTextColor(subscription.status)">
                      {{ subscription.status }}
                    </span>
                  </div>
                  <span class="text-sm text-gray-500">
                    Next billing: {{ subscription.nextBilling }}
                  </span>
                </div>
              </div>
            </div>

            <div class="flex items-center space-x-6">
              <div class="text-right">
                <p class="text-2xl font-bold text-gray-900">${{ subscription.price }}</p>
                <p class="text-sm text-gray-600">/{{ subscription.billing }}</p>
              </div>

              <div class="flex items-center space-x-2">
                <button class="p-2 text-gray-400 hover:text-blue-600 transition-colors duration-150">
                  <span class="text-lg">✏️</span>
                </button>
                <button class="p-2 text-gray-400 hover:text-red-600 transition-colors duration-150">
                  <span class="text-lg">🗑️</span>
                </button>
              </div>
            </div>
          </div>

          <!-- Usage Progress Bar (for subscriptions with usage limits) -->
          <div v-if="subscription.usage" class="mt-4">
            <div class="flex items-center justify-between text-sm text-gray-600 mb-2">
              <span>Usage this month</span>
              <span>{{ subscription.usage.used }} / {{ subscription.usage.limit }} {{ subscription.usage.unit }}</span>
            </div>
            <div class="w-full bg-gray-200 rounded-full h-2">
              <div
                class="h-2 rounded-full transition-all duration-300"
                :class="getUsageBarColor(subscription.usage.percentage)"
                :style="{ width: subscription.usage.percentage + '%' }"
              ></div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Billing History -->
    <div class="bg-white rounded-xl shadow-sm border border-gray-200">
      <div class="p-6 border-b border-gray-200">
        <div class="flex items-center justify-between">
          <h3 class="text-xl font-semibold text-gray-900">Recent Billing History</h3>
          <button class="text-blue-600 hover:text-blue-700 font-medium transition-colors">
            View All
          </button>
        </div>
      </div>

      <div class="divide-y divide-gray-200">
        <div
          v-for="bill in billingHistory"
          :key="bill.id"
          class="p-6 flex items-center justify-between hover:bg-gray-50 transition-colors duration-150"
        >
          <div class="flex items-center space-x-4">
            <div :class="bill.statusBg" class="w-10 h-10 rounded-lg flex items-center justify-center">
              <span class="text-sm">{{ bill.icon }}</span>
            </div>
            <div>
              <h4 class="font-medium text-gray-900">{{ bill.description }}</h4>
              <p class="text-sm text-gray-600">{{ bill.date }}</p>
            </div>
          </div>

          <div class="flex items-center space-x-4">
            <span class="text-lg font-semibold text-gray-900">${{ bill.amount }}</span>
            <span :class="getBillStatusClass(bill.status)" class="px-3 py-1 rounded-full text-xs font-medium">
              {{ bill.status }}
            </span>
          </div>
        </div>
      </div>
    </div>

    <!-- Action Buttons -->
    <div class="flex flex-col sm:flex-row gap-4">
      <button class="flex items-center justify-center space-x-2 px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white font-medium rounded-lg transition-all duration-200 shadow-sm hover:shadow-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
        <span class="text-lg">📊</span>
        <span>Usage Analytics</span>
      </button>
      <button class="flex items-center justify-center space-x-2 px-6 py-3 bg-gray-600 hover:bg-gray-700 text-white font-medium rounded-lg transition-all duration-200 shadow-sm hover:shadow-md focus:outline-none focus:ring-2 focus:ring-gray-500 focus:ring-offset-2">
        <span class="text-lg">💳</span>
        <span>Payment Methods</span>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const overview = ref({
  active: 5,
  monthlySpend: 287,
  nextBilling: 'Jan 15'
})

const subscriptions = ref([
  {
    id: 1,
    name: 'Professional Plan',
    description: 'Advanced features for business users',
    icon: '💼',
    iconBg: 'bg-blue-100',
    price: 79,
    billing: 'month',
    status: 'Active',
    nextBilling: 'Jan 15, 2024',
    usage: {
      used: 45,
      limit: 100,
      unit: 'GB',
      percentage: 45
    }
  },
  {
    id: 2,
    name: 'Cloud Storage Plus',
    description: 'Extended storage capacity',
    icon: '☁️',
    iconBg: 'bg-green-100',
    price: 19,
    billing: 'month',
    status: 'Active',
    nextBilling: 'Jan 20, 2024',
    usage: {
      used: 850,
      limit: 1000,
      unit: 'GB',
      percentage: 85
    }
  },
  {
    id: 3,
    name: 'Analytics Pro',
    description: 'Advanced analytics and reporting',
    icon: '📈',
    iconBg: 'bg-purple-100',
    price: 49,
    billing: 'month',
    status: 'Active',
    nextBilling: 'Jan 10, 2024'
  },
  {
    id: 4,
    name: 'Support Premium',
    description: '24/7 priority support',
    icon: '🎧',
    iconBg: 'bg-yellow-100',
    price: 25,
    billing: 'month',
    status: 'Paused',
    nextBilling: 'Feb 1, 2024'
  }
])

const billingHistory = ref([
  {
    id: 1,
    description: 'Professional Plan - Monthly',
    date: 'December 15, 2023',
    amount: 79,
    status: 'Paid',
    icon: '✅',
    statusBg: 'bg-green-100'
  },
  {
    id: 2,
    description: 'Cloud Storage Plus - Monthly',
    date: 'December 20, 2023',
    amount: 19,
    status: 'Paid',
    icon: '✅',
    statusBg: 'bg-green-100'
  },
  {
    id: 3,
    description: 'Analytics Pro - Monthly',
    date: 'December 10, 2023',
    amount: 49,
    status: 'Paid',
    icon: '✅',
    statusBg: 'bg-green-100'
  },
  {
    id: 4,
    description: 'Professional Plan - Monthly',
    date: 'November 15, 2023',
    amount: 79,
    status: 'Failed',
    icon: '❌',
    statusBg: 'bg-red-100'
  }
])

const getStatusColor = (status) => {
  switch (status.toLowerCase()) {
    case 'active': return 'bg-green-500'
    case 'paused': return 'bg-yellow-500'
    case 'expired': return 'bg-red-500'
    default: return 'bg-gray-400'
  }
}

const getStatusTextColor = (status) => {
  switch (status.toLowerCase()) {
    case 'active': return 'text-green-700'
    case 'paused': return 'text-yellow-700'
    case 'expired': return 'text-red-700'
    default: return 'text-gray-500'
  }
}

const getUsageBarColor = (percentage) => {
  if (percentage >= 90) return 'bg-red-500'
  if (percentage >= 75) return 'bg-yellow-500'
  return 'bg-green-500'
}

const getBillStatusClass = (status) => {
  switch (status.toLowerCase()) {
    case 'paid': return 'bg-green-100 text-green-800'
    case 'failed': return 'bg-red-100 text-red-800'
    case 'pending': return 'bg-yellow-100 text-yellow-800'
    default: return 'bg-gray-100 text-gray-800'
  }
}
</script>
