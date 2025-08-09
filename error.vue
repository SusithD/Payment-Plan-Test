<template>
  <div class="min-h-screen bg-gray-50 flex flex-col">
    <div class="flex-1 flex items-center justify-center px-4 sm:px-6 lg:px-8">
      <div class="max-w-md w-full">
        <div class="text-center">
          <!-- Error Icon -->
          <div class="mx-auto h-24 w-24 mb-8 relative">
            <div class="absolute inset-0 rounded-full bg-gradient-to-br from-error-500 to-error-600 opacity-20 animate-pulse"></div>
            <div class="relative h-full w-full rounded-full bg-gradient-to-br from-error-500 to-error-600 flex items-center justify-center">
              <svg class="h-12 w-12 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4c-.77-.833-1.964-.833-2.732 0L4.082 16.5c-.77.833.192 2.5 1.732 2.5z" />
              </svg>
            </div>
          </div>

          <!-- Error Code -->
          <h1 class="text-6xl md:text-7xl font-bold gradient-text mb-4">
            {{ error.statusCode }}
          </h1>

          <!-- Error Message -->
          <h2 class="text-2xl md:text-3xl font-semibold text-gray-800 mb-4">
            {{ getErrorTitle(error.statusCode) }}
          </h2>

          <p class="text-lg text-gray-600 mb-8 max-w-sm mx-auto">
            {{ getErrorMessage(error.statusCode) }}
          </p>

          <!-- Action Buttons -->
          <div class="space-y-4 sm:space-y-0 sm:space-x-4 sm:flex sm:justify-center">
            <button
              @click="handleClearError"
              class="w-full sm:w-auto btn-primary px-8 py-3 text-base font-medium"
            >
              <svg class="w-5 h-5 mr-2 inline" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h10a8 8 0 018 8v2M3 10l6 6m-6-6l6-6" />
              </svg>
              Try Again
            </button>

            <NuxtLink
              to="/dashboard"
              class="w-full sm:w-auto btn-outline px-8 py-3 text-base font-medium inline-flex items-center justify-center"
            >
              <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
              </svg>
              Go to Dashboard
            </NuxtLink>
          </div>

          <!-- Additional Help -->
          <div class="mt-12 p-6 bg-white rounded-xl shadow-sm border border-gray-100">
            <h3 class="text-lg font-semibold text-gray-800 mb-3">Need Help?</h3>
            <p class="text-gray-600 mb-4">
              If you continue to experience issues, our support team is here to help.
            </p>
            <NuxtLink
              to="/support"
              class="inline-flex items-center text-primary-600 hover:text-primary-800 font-medium"
            >
              Contact Support
              <svg class="w-4 h-4 ml-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
            </NuxtLink>
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
// Define error handling
const props = defineProps(['error'])

// Handle clearing error
const handleClearError = async () => {
  await clearError({ redirect: '/dashboard' })
}

// Get error title based on status code
const getErrorTitle = (statusCode) => {
  switch (statusCode) {
    case 404:
      return 'Page Not Found'
    case 403:
      return 'Access Denied'
    case 500:
      return 'Server Error'
    case 503:
      return 'Service Unavailable'
    default:
      return 'Something Went Wrong'
  }
}

// Get error message based on status code
const getErrorMessage = (statusCode) => {
  switch (statusCode) {
    case 404:
      return "The page you're looking for doesn't exist or has been moved."
    case 403:
      return "You don't have permission to access this resource."
    case 500:
      return "We're experiencing technical difficulties. Please try again later."
    case 503:
      return "Our service is temporarily unavailable. We're working to fix this."
    default:
      return "An unexpected error occurred. Please try again or contact support if the issue persists."
  }
}
</script>

<style scoped>
.gradient-text {
  background: linear-gradient(135deg, #2C4880 0%, #4476b0 100%);
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
