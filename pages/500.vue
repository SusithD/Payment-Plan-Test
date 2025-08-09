<template>
  <div class="min-h-screen bg-gray-50 flex flex-col">
    <div class="flex-1 flex items-center justify-center px-4 sm:px-6 lg:px-8">
      <div class="max-w-md w-full">
        <div class="text-center fade-in">
          <!-- Server Error Icon -->
          <div class="mx-auto h-24 w-24 mb-8 relative">
            <div class="absolute inset-0 rounded-full bg-gradient-to-br from-error-500 to-error-600 opacity-20 animate-pulse"></div>
            <div class="relative h-full w-full rounded-full bg-gradient-to-br from-error-500 to-error-600 flex items-center justify-center">
              <svg class="h-12 w-12 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
              </svg>
            </div>
          </div>

          <!-- Error Code -->
          <h1 class="text-6xl md:text-7xl font-bold gradient-text mb-4">
            500
          </h1>

          <!-- Error Message -->
          <h2 class="text-2xl md:text-3xl font-semibold text-gray-800 mb-4">
            Server Error
          </h2>

          <p class="text-lg text-gray-600 mb-8 max-w-sm mx-auto">
            We're experiencing technical difficulties. Our team has been notified and is working to resolve this issue.
          </p>

          <!-- Status Information -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 mb-8">
            <div class="flex items-center justify-center mb-4">
              <div class="flex items-center space-x-2">
                <div class="h-3 w-3 bg-error-500 rounded-full animate-pulse"></div>
                <span class="text-sm font-medium text-gray-700">Service Status</span>
              </div>
            </div>
            <p class="text-sm text-gray-600 mb-4">
              We're working to restore full functionality as quickly as possible.
            </p>
            <div class="bg-gray-50 rounded-lg p-3">
              <div class="flex items-center justify-between text-xs text-gray-500">
                <span>Estimated Resolution</span>
                <span class="font-medium">{{ estimatedTime }}</span>
              </div>
            </div>
          </div>

          <!-- Action Buttons -->
          <div class="space-y-4 sm:space-y-0 sm:space-x-4 sm:flex sm:justify-center">
            <button
              @click="refreshPage"
              class="w-full sm:w-auto btn-primary px-8 py-3 text-base font-medium"
              :disabled="isRefreshing"
            >
              <svg v-if="!isRefreshing" class="w-5 h-5 mr-2 inline" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
              </svg>
              <svg v-else class="animate-spin w-5 h-5 mr-2 inline" fill="none" viewBox="0 0 24 24">
                <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
              </svg>
              {{ isRefreshing ? 'Refreshing...' : 'Try Again' }}
            </button>

            <NuxtLink
              to="/support"
              class="w-full sm:w-auto btn-outline px-8 py-3 text-base font-medium inline-flex items-center justify-center"
            >
              <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
              </svg>
              Report Issue
            </NuxtLink>
          </div>

          <!-- Additional Information -->
          <div class="mt-8 text-xs text-gray-500">
            <p>Error ID: {{ errorId }}</p>
            <p>{{ new Date().toLocaleString() }}</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Footer -->
    <div class="py-6 text-center text-sm text-gray-500">
      <p>&copy; {{ new Date().getFullYear() }} PaymentPlan. All rights reserved.</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const isRefreshing = ref(false)
const estimatedTime = ref('< 30 minutes')
const errorId = ref('')

onMounted(() => {
  // Generate a random error ID for tracking
  errorId.value = Math.random().toString(36).substr(2, 9).toUpperCase()
})

const refreshPage = async () => {
  isRefreshing.value = true

  // Simulate a brief delay before refresh
  await new Promise(resolve => setTimeout(resolve, 1500))

  // Refresh the page
  window.location.reload()
}
</script>

<style scoped>
.gradient-text {
  background: linear-gradient(135deg, #eb2f2f 0%, #d41f1f 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.fade-in {
  animation: fadeIn 0.5s ease-in-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
