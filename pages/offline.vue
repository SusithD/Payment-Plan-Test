<template>
  <div class="fade-in bg-gray-50 min-h-screen flex items-center justify-center">
    <div class="container-custom py-16">
      <div class="max-w-2xl mx-auto text-center">
        <!-- Offline Icon -->
        <div class="mb-8">
          <div class="h-24 w-24 bg-gray-100 text-gray-400 rounded-full flex items-center justify-center mx-auto mb-6">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18.364 5.636l-3.536 3.536m0 5.656l3.536 3.536M9.172 9.172L5.636 5.636m3.536 9.192L5.636 18.364M12 2.18l.09-.012a10 10 0 017.274 7.274.657.657 0 01-.372.59L12 12l-.09-.012a10 10 0 01-7.274-7.274.657.657 0 01.372-.59L12 2.18z" />
            </svg>
          </div>
          
          <!-- Status Badge -->
          <div class="inline-flex items-center px-4 py-2 rounded-full bg-gray-100 text-gray-600 text-sm font-medium">
            <div class="h-2 w-2 bg-gray-400 rounded-full mr-2"></div>
            You're Offline
          </div>
        </div>

        <!-- Main Content -->
        <div class="bg-white rounded-2xl shadow-xl p-8 mb-8">
          <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
            No Internet Connection
          </h1>
          
          <p class="text-xl text-gray-600 mb-6 leading-relaxed">
            It looks like you're not connected to the internet. Some features may not be available until you reconnect.
          </p>

          <!-- Connection Status -->
          <div class="bg-gray-50 border border-gray-200 rounded-lg p-6 mb-6">
            <div class="flex items-center justify-center mb-3">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-400 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.111 16.404a5.5 5.5 0 017.778 0M12 20h.01m-7.08-7.071c3.904-3.905 10.236-3.905 14.141 0M1.394 9.393c5.857-5.857 15.355-5.857 21.213 0" />
              </svg>
              <h3 class="text-lg font-semibold text-gray-700">Connection Status</h3>
            </div>
            <div class="text-center">
              <div class="text-lg font-medium text-gray-600 mb-2">
                <span id="connection-status" :class="isOnline ? 'text-success-600' : 'text-error-600'">
                  {{ isOnline ? 'Connected' : 'Disconnected' }}
                </span>
              </div>
              <button 
                @click="checkConnection"
                class="btn btn-outline-primary text-sm"
                :disabled="checking"
              >
                <span v-if="checking">Checking...</span>
                <span v-else>Check Connection</span>
              </button>
            </div>
          </div>

          <!-- Available Offline Features -->
          <div class="text-left mb-6">
            <h3 class="text-lg font-semibold text-gray-900 mb-4">Available offline:</h3>
            <div class="space-y-3">
              <div class="flex items-start">
                <div class="h-2 w-2 bg-success-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
                <span class="text-gray-600">View cached payment history</span>
              </div>
              <div class="flex items-start">
                <div class="h-2 w-2 bg-success-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
                <span class="text-gray-600">Access previously viewed invoices</span>
              </div>
              <div class="flex items-start">
                <div class="h-2 w-2 bg-success-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
                <span class="text-gray-600">Review account information</span>
              </div>
              <div class="flex items-start">
                <div class="h-2 w-2 bg-warning-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
                <span class="text-gray-600">Browse help articles (cached)</span>
              </div>
            </div>
          </div>

          <!-- Unavailable Features -->
          <div class="text-left mb-6">
            <h3 class="text-lg font-semibold text-gray-900 mb-4">Requires internet connection:</h3>
            <div class="space-y-3">
              <div class="flex items-start">
                <div class="h-2 w-2 bg-error-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
                <span class="text-gray-600">Make new payments</span>
              </div>
              <div class="flex items-start">
                <div class="h-2 w-2 bg-error-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
                <span class="text-gray-600">Update payment methods</span>
              </div>
              <div class="flex items-start">
                <div class="h-2 w-2 bg-error-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
                <span class="text-gray-600">Real-time account sync</span>
              </div>
              <div class="flex items-start">
                <div class="h-2 w-2 bg-error-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
                <span class="text-gray-600">Customer support chat</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Offline Actions -->
        <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 mb-8">
          <h3 class="text-lg font-semibold text-gray-900 mb-4">What you can do:</h3>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <button 
              @click="goToHistory"
              class="flex items-center p-4 text-left border border-gray-200 rounded-lg hover:border-primary-300 hover:bg-primary-50 transition-all"
            >
              <div class="h-10 w-10 bg-secondary-100 text-secondary-600 rounded-full flex items-center justify-center mr-3">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
                </svg>
              </div>
              <div>
                <div class="font-semibold text-gray-900">View History</div>
                <div class="text-sm text-gray-600">Browse cached transactions</div>
              </div>
            </button>
            
            <button 
              @click="goToProfile"
              class="flex items-center p-4 text-left border border-gray-200 rounded-lg hover:border-primary-300 hover:bg-primary-50 transition-all"
            >
              <div class="h-10 w-10 bg-accent-100 text-accent-600 rounded-full flex items-center justify-center mr-3">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                </svg>
              </div>
              <div>
                <div class="font-semibold text-gray-900">View Profile</div>
                <div class="text-sm text-gray-600">Review account details</div>
              </div>
            </button>
          </div>
        </div>

        <!-- Troubleshooting -->
        <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 mb-8">
          <h3 class="text-lg font-semibold text-gray-900 mb-4">Troubleshooting Tips</h3>
          
          <div class="space-y-4 text-left">
            <div class="flex items-start">
              <div class="flex-shrink-0 w-6 h-6 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mr-3 mt-0.5">
                <span class="text-xs font-bold">1</span>
              </div>
              <div>
                <h4 class="font-medium text-gray-900 mb-1">Check your connection</h4>
                <p class="text-sm text-gray-600">Make sure you're connected to Wi-Fi or have mobile data enabled.</p>
              </div>
            </div>
            
            <div class="flex items-start">
              <div class="flex-shrink-0 w-6 h-6 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mr-3 mt-0.5">
                <span class="text-xs font-bold">2</span>
              </div>
              <div>
                <h4 class="font-medium text-gray-900 mb-1">Refresh the page</h4>
                <p class="text-sm text-gray-600">Try refreshing your browser or pulling down to refresh on mobile.</p>
              </div>
            </div>
            
            <div class="flex items-start">
              <div class="flex-shrink-0 w-6 h-6 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mr-3 mt-0.5">
                <span class="text-xs font-bold">3</span>
              </div>
              <div>
                <h4 class="font-medium text-gray-900 mb-1">Check for outages</h4>
                <p class="text-sm text-gray-600">Visit our status page or contact support if the problem persists.</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Contact Support -->
        <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6">
          <h3 class="text-lg font-semibold text-gray-900 mb-4">Need Help?</h3>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div class="text-center p-4 bg-gray-50 rounded-lg">
              <div class="h-10 w-10 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mx-auto mb-2">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                </svg>
              </div>
              <h4 class="font-semibold text-gray-900 mb-1">Email Support</h4>
              <p class="text-sm text-gray-600 mb-2">Available 24/7</p>
              <a href="mailto:support@coveragex.com" class="text-primary-600 hover:text-primary-700 text-sm font-medium">
                support@coveragex.com
              </a>
            </div>
            
            <div class="text-center p-4 bg-gray-50 rounded-lg">
              <div class="h-10 w-10 bg-accent-100 text-accent-600 rounded-full flex items-center justify-center mx-auto mb-2">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 18h.01M8 21h8a2 2 0 002-2V5a2 2 0 00-2-2H8a2 2 0 00-2 2v14a2 2 0 002 2z" />
                </svg>
              </div>
              <h4 class="font-semibold text-gray-900 mb-1">Phone Support</h4>
              <p class="text-sm text-gray-600 mb-2">Mon-Fri 8AM-8PM EST</p>
              <a href="tel:+18001234567" class="text-accent-600 hover:text-accent-700 text-sm font-medium">
                +1 (800) 123-4567
              </a>
            </div>
          </div>
        </div>

        <!-- Auto Retry Notice -->
        <div class="mt-8 text-center">
          <p class="text-sm text-gray-500">
            We'll automatically retry connecting in the background.
            <br>
            <span v-if="retryCount > 0">Retry attempts: {{ retryCount }}</span>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

definePageMeta({
  title: 'Offline - CoverageX Payment Solutions',
  description: 'You\'re currently offline. Some features may not be available.'
});

// Reactive state
const isOnline = ref(navigator.onLine);
const checking = ref(false);
const retryCount = ref(0);
let retryInterval = null;

// Methods
function checkConnection() {
  checking.value = true;
  
  // Simulate checking connection
  setTimeout(() => {
    isOnline.value = navigator.onLine;
    checking.value = false;
    
    if (isOnline.value) {
      // Redirect to main app when back online
      window.location.reload();
    }
  }, 1000);
}

function handleOnline() {
  isOnline.value = true;
  // Automatically redirect when back online
  setTimeout(() => {
    window.location.reload();
  }, 1000);
}

function handleOffline() {
  isOnline.value = false;
}

function autoRetryConnection() {
  if (!isOnline.value) {
    retryCount.value++;
    checkConnection();
  }
}

function goToHistory() {
  // Navigate to cached history page
  navigateTo('/history');
}

function goToProfile() {
  // Navigate to cached profile page
  navigateTo('/profile');
}

onMounted(() => {
  // Listen for online/offline events
  window.addEventListener('online', handleOnline);
  window.addEventListener('offline', handleOffline);
  
  // Set up auto retry every 30 seconds
  retryInterval = setInterval(autoRetryConnection, 30000);
});

onUnmounted(() => {
  window.removeEventListener('online', handleOnline);
  window.removeEventListener('offline', handleOffline);
  
  if (retryInterval) {
    clearInterval(retryInterval);
  }
});
</script>

<style scoped>
/* Ensure smooth transitions for status changes */
#connection-status {
  transition: color 0.3s ease;
}
</style>