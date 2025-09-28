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
            <!-- Subscriptions header icon removed -->
          </div>
        </div>
      </div>
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
    icon: '',
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
    icon: '',
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
    icon: '',
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
    icon: '',
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
    icon: '',
    statusBg: 'bg-green-100'
  },
  {
    id: 2,
    description: 'Cloud Storage Plus - Monthly',
    date: 'December 20, 2023',
    amount: 19,
    status: 'Paid',
    icon: '',
    statusBg: 'bg-green-100'
  },
  {
    id: 3,
    description: 'Analytics Pro - Monthly',
    date: 'December 10, 2023',
    amount: 49,
    status: 'Paid',
    icon: '',
    statusBg: 'bg-green-100'
  },
  {
    id: 4,
    description: 'Professional Plan - Monthly',
    date: 'November 15, 2023',
    amount: 79,
    status: 'Failed',
    icon: '',
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
