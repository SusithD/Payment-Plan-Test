<template>
  <div class="min-h-screen bg-gray-50 flex flex-col">
    <div class="flex-1 flex items-center justify-center px-4 sm:px-6 lg:px-8">
      <div class="max-w-lg w-full">
        <div class="text-center fade-in">
          <!-- 404 Illustration -->
          <div class="mx-auto h-32 w-32 mb-8 relative">
            <div class="absolute inset-0 rounded-full bg-gradient-to-br from-primary-500 to-primary-600 opacity-10 animate-pulse"></div>
            <div class="relative h-full w-full rounded-full bg-gradient-to-br from-primary-500 to-primary-600 flex items-center justify-center">
              <svg class="h-16 w-16 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9.172 16.172a4 4 0 015.656 0M9 12h6m-6-4h6m6 5a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
          </div>

          <!-- 404 Text -->
          <h1 class="text-8xl md:text-9xl font-bold gradient-text mb-6 tracking-tight">
            404
          </h1>

          <h2 class="text-3xl md:text-4xl font-semibold text-gray-800 mb-4">
            Page Not Found
          </h2>

          <p class="text-xl text-gray-600 mb-8 max-w-md mx-auto leading-relaxed">
            Oops! The page you're looking for seems to have wandered off. Let's get you back on track.
          </p>

          <!-- Search Suggestions -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 mb-8">
            <h3 class="text-lg font-semibold text-gray-800 mb-4">Popular Pages</h3>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
              <NuxtLink
                to="/dashboard"
                class="flex items-center p-3 rounded-lg border border-gray-200 hover:border-primary-300 hover:bg-primary-50 transition-all duration-200 group"
              >
                <div class="h-8 w-8 rounded-lg bg-primary-100 flex items-center justify-center mr-3 group-hover:bg-primary-200">
                  <svg class="h-4 w-4 text-primary-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
                  </svg>
                </div>
                <span class="text-sm font-medium text-gray-700 group-hover:text-primary-700">Dashboard</span>
              </NuxtLink>

              <NuxtLink
                to="/payments"
                class="flex items-center p-3 rounded-lg border border-gray-200 hover:border-primary-300 hover:bg-primary-50 transition-all duration-200 group"
              >
                <div class="h-8 w-8 rounded-lg bg-primary-100 flex items-center justify-center mr-3 group-hover:bg-primary-200">
                  <svg class="h-4 w-4 text-primary-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
                  </svg>
                </div>
                <span class="text-sm font-medium text-gray-700 group-hover:text-primary-700">Payments</span>
              </NuxtLink>

              <NuxtLink
                to="/history"
                class="flex items-center p-3 rounded-lg border border-gray-200 hover:border-primary-300 hover:bg-primary-50 transition-all duration-200 group"
              >
                <div class="h-8 w-8 rounded-lg bg-primary-100 flex items-center justify-center mr-3 group-hover:bg-primary-200">
                  <svg class="h-4 w-4 text-primary-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                </div>
                <span class="text-sm font-medium text-gray-700 group-hover:text-primary-700">History</span>
              </NuxtLink>

              <NuxtLink
                to="/profile"
                class="flex items-center p-3 rounded-lg border border-gray-200 hover:border-primary-300 hover:bg-primary-50 transition-all duration-200 group"
              >
                <div class="h-8 w-8 rounded-lg bg-primary-100 flex items-center justify-center mr-3 group-hover:bg-primary-200">
                  <svg class="h-4 w-4 text-primary-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                  </svg>
                </div>
                <span class="text-sm font-medium text-gray-700 group-hover:text-primary-700">Profile</span>
              </NuxtLink>
            </div>
          </div>

          <!-- Action Buttons -->
          <div class="space-y-4 sm:space-y-0 sm:space-x-4 sm:flex sm:justify-center">
            <button
              @click="goBack"
              class="w-full sm:w-auto btn-primary px-8 py-3 text-base font-medium"
            >
              <svg class="w-5 h-5 mr-2 inline" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" />
              </svg>
              Go Back
            </button>

            <NuxtLink
              to="/dashboard"
              class="w-full sm:w-auto btn-outline px-8 py-3 text-base font-medium inline-flex items-center justify-center"
            >
              <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
              </svg>
              Home
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
const goBack = () => {
  if (window.history.length > 1) {
    window.history.back()
  } else {
    navigateTo('/dashboard')
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
  animation: fadeIn 0.6s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
