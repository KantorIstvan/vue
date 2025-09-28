<template>
  <div class="max-w-4xl mx-auto space-y-6">
    <!-- Page Header -->
    <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
      <div class="flex items-center justify-between">
        <div>
          <h2 class="text-3xl font-bold text-gray-900">Profile Information</h2>
          <p class="text-gray-600 mt-1">Manage your personal information and account settings</p>
        </div>
        <div class="hidden md:block">
          <div class="w-16 h-16 bg-gradient-to-br from-blue-500 to-purple-600 rounded-2xl flex items-center justify-center shadow-lg">
            <!-- Profile header icon removed -->
          </div>
        </div>
      </div>
    </div>

    <!-- Profile Content -->
    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
      <!-- Profile Header Card -->
      <div class="lg:col-span-1">
        <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6 text-center">
          <div class="relative inline-block mb-4">
            <div class="w-24 h-24 bg-gradient-to-br from-blue-500 to-purple-600 rounded-full flex items-center justify-center text-white text-2xl font-bold shadow-lg">
              <span>{{ userInitials }}</span>
            </div>
            <div class="absolute -bottom-1 -right-1 w-8 h-8 bg-green-500 rounded-full flex items-center justify-center border-4 border-white shadow-sm">
              <!-- Checkmark icon removed -->
            </div>
          </div>
          <h3 class="text-xl font-bold text-gray-900 mb-2">{{ user.firstName }} {{ user.lastName }}</h3>
          <span :class="roleClass" class="inline-flex items-center px-3 py-1 rounded-full text-sm font-medium bg-blue-100 text-blue-800">
            <span class="w-2 h-2 bg-blue-500 rounded-full mr-2"></span>
            {{ user.role }}
          </span>
        </div>
      </div>

      <!-- Profile Information Grid -->
      <div class="lg:col-span-2 space-y-6">
        <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
          <h4 class="text-lg font-semibold text-gray-900 mb-4">Personal Information</h4>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div class="space-y-2">
              <label class="flex items-center text-sm font-medium text-gray-700">
                Email Address
              </label>
              <div class="p-3 bg-gray-50 border border-gray-200 rounded-lg text-gray-900 font-medium">
                {{ user.email }}
              </div>
            </div>

            <div class="space-y-2">
              <label class="flex items-center text-sm font-medium text-gray-700">
                First Name
              </label>
              <div class="p-3 bg-gray-50 border border-gray-200 rounded-lg text-gray-900 font-medium">
                {{ user.firstName }}
              </div>
            </div>

            <div class="space-y-2">
              <label class="flex items-center text-sm font-medium text-gray-700">
                Last Name
              </label>
              <div class="p-3 bg-gray-50 border border-gray-200 rounded-lg text-gray-900 font-medium">
                {{ user.lastName }}
              </div>
            </div>

            <div class="space-y-2">
              <label class="flex items-center text-sm font-medium text-gray-700">
                Password
              </label>
              <div class="p-3 bg-gray-50 border border-gray-200 rounded-lg flex items-center justify-between">
                <span class="text-gray-900 font-medium">
                  {{ showPassword ? user.password : '••••••••••••' }}
                </span>
                <button @click="togglePassword" class="text-gray-500 hover:text-gray-700 transition-colors">
                  <!-- Eye icons removed -->
                </button>
              </div>
            </div>
          </div>
        </div>

        <!-- User Role Section -->
        <div class="bg-white rounded-xl shadow-sm border border-gray-200 p-6">
          <label class="flex items-center text-lg font-semibold text-gray-900 mb-4">
            User Role & Permissions
          </label>
          <div class="bg-gradient-to-br from-blue-50 to-purple-50 border border-blue-200 rounded-lg p-4">
            <div class="flex items-center justify-between">
              <div class="flex-1">
                <div class="flex items-center mb-2">
                  <span :class="roleClass" class="inline-flex items-center px-3 py-1 rounded-full text-sm font-medium bg-blue-100 text-blue-800">
                    <span class="w-2 h-2 bg-blue-500 rounded-full mr-2"></span>
                    {{ user.role }}
                  </span>
                </div>
                <p class="text-gray-700">Full administrative access to all dashboard features</p>
              </div>
              <!-- Lightning emoji removed -->
            </div>
          </div>
        </div>


      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const showPassword = ref(false)

// Sample user data - in a real app this would come from an API
const user = ref({
  firstName: 'John',
  lastName: 'Doe',
  email: 'john.doe@example.com',
  password: 'mypassword123',
  role: 'Admin'
})

const userInitials = computed(() => {
  return user.value.firstName.charAt(0) + user.value.lastName.charAt(0)
})

const roleClass = computed(() => {
  return user.value.role.toLowerCase() === 'admin' ? 'admin-role' : 'user-role'
})

const togglePassword = () => {
  showPassword.value = !showPassword.value
}
</script>

<style scoped>
@media (max-width: 768px) {
  .profile-card {
    padding: 20px;
  }

  .profile-actions {
    flex-direction: column;
  }
}
</style>
