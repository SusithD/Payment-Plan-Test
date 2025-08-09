<template>
  <div class="min-h-screen bg-gray-50 flex flex-col">
    <div class="flex-1 flex items-center justify-center px-4 sm:px-6 lg:px-8">
      <div class="max-w-md w-full">
        <div class="text-center fade-in">
          <!-- Access Denied Icon -->
          <div class="mx-auto h-24 w-24 mb-8 relative">
            <div class="absolute inset-0 rounded-full bg-gradient-to-br from-warning-500 to-warning-600 opacity-20 animate-pulse"></div>
            <div class="relative h-full w-full rounded-full bg-gradient-to-br from-warning-500 to-warning-600 flex items-center justify-center">
              <svg class="h-12 w-12 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
              </svg>
            </div>
          </div>

          <!-- Error Code -->
          <h1 class="text-6xl md:text-7xl font-bold gradient-text mb-4">
            403
          </h1>

          <!-- Error Message -->
          <h2 class="text-2xl md:text-3xl font-semibold text-gray-800 mb-4">
            Access Denied
          </h2>

          <p class="text-lg text-gray-600 mb-8 max-w-sm mx-auto">
            You don't have permission to access this resource. Please check your account status or contact support.
          </p>

          <!-- Possible Reasons -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 mb-8 text-left">
            <h3 class="text-lg font-semibold text-gray-800 mb-4 text-center">Common Reasons</h3>
            <ul class="space-y-3 text-sm text-gray-600">
              <li class="flex items-start">
                <svg class="w-5 h-5 text-warning-500 mr-3 mt-0.5 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
                Your session may have expired
              </li>
              <li class="flex items-start">
                <svg class="w-5 h-5 text-warning-500 mr-3 mt-0.5 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
                Account verification is required
              </li>
              <li class="flex items-start">
                <svg class="w-5 h-5 text-warning-500 mr-3 mt-0.5 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
                Insufficient account permissions
              </li>
            </ul>
          </div>

          <!-- Action Buttons -->
          <div class="space-y-4 sm:space-y-0 sm:space-x-4 sm:flex sm:justify-center">
            <NuxtLink
              to="/auth/login"
              class="w-full sm:w-auto btn-primary px-8 py-3 text-base font-medium inline-flex items-center justify-center"
            >
              <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 16l-4-4m0 0l4-4m-4 4h14m-5 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h7a3 3 0 013 3v1" />
              </svg>
              Sign In Again
            </NuxtLink>

            <NuxtLink
              to="/support"
              class="w-full sm:w-auto btn-outline px-8 py-3 text-base font-medium inline-flex items-center justify-center"
            >
              <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18.364 5.636l-3.536 3.536m0 5.656l3.536 3.536M9.172 9.172L5.636 5.636m3.536 9.192L5.636 18.364M12 12l.01-.01M12 12l.01.01M12 12l.01.01M12 12l.01.01" />
              </svg>
              Get Help
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

<style scoped>
.gradient-text {
  background: linear-gradient(135deg, #ffb100 0%, #f99f0b 100%);
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
