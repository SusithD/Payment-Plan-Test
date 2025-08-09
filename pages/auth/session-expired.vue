<template>
  <div class="fade-in bg-gray-50 min-h-screen flex items-center justify-center">
    <div class="container-custom py-16">
      <div class="max-w-xl mx-auto text-center">
        <!-- Session Expired Icon -->
        <div class="mb-8">
          <div class="h-20 w-20 bg-warning-100 text-warning-600 rounded-full flex items-center justify-center mx-auto mb-6">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
          </div>
          
          <!-- Status Badge -->
          <div class="inline-flex items-center px-4 py-2 rounded-full bg-warning-100 text-warning-800 text-sm font-medium">
            <div class="h-2 w-2 bg-warning-500 rounded-full mr-2"></div>
            Session Expired
          </div>
        </div>

        <!-- Main Content -->
        <div class="bg-white rounded-2xl shadow-xl p-8 mb-8">
          <h1 class="text-2xl md:text-3xl font-bold text-gray-900 mb-4">
            Your Session Has Expired
          </h1>
          
          <p class="text-lg text-gray-600 mb-6 leading-relaxed">
            For your security, we've logged you out after a period of inactivity. Please sign in again to continue.
          </p>

          <!-- Security Message -->
          <div class="bg-primary-50 border border-primary-200 rounded-lg p-4 mb-6">
            <div class="flex items-start">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-primary-600 mr-2 mt-0.5 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
              </svg>
              <div>
                <h3 class="font-semibold text-primary-900 mb-1">Your account is secure</h3>
                <p class="text-sm text-primary-700">We automatically log out inactive sessions to protect your payment information and personal data.</p>
              </div>
            </div>
          </div>

          <!-- Action Buttons -->
          <div class="space-y-3">
            <NuxtLink to="/auth/login" class="btn btn-primary w-full justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 16l-4-4m0 0l4-4m-4 4h14m-5 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h7a3 3 0 013 3v1" />
              </svg>
              Sign In Again
            </NuxtLink>
            
            <NuxtLink to="/" class="btn btn-outline-primary w-full justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
              </svg>
              Go to Homepage
            </NuxtLink>
          </div>
        </div>

        <!-- Security Tips -->
        <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 mb-8">
          <h3 class="text-lg font-semibold text-gray-900 mb-4">Security Tips</h3>
          
          <div class="space-y-4 text-left">
            <div class="flex items-start">
              <div class="flex-shrink-0 w-6 h-6 bg-success-100 text-success-600 rounded-full flex items-center justify-center mr-3 mt-0.5">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-3 w-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                </svg>
              </div>
              <div>
                <h4 class="font-medium text-gray-900 mb-1">Stay active during sessions</h4>
                <p class="text-sm text-gray-600">Sessions remain active when you're using the platform. We only log you out after extended inactivity.</p>
              </div>
            </div>
            
            <div class="flex items-start">
              <div class="flex-shrink-0 w-6 h-6 bg-success-100 text-success-600 rounded-full flex items-center justify-center mr-3 mt-0.5">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-3 w-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                </svg>
              </div>
              <div>
                <h4 class="font-medium text-gray-900 mb-1">Always log out on shared devices</h4>
                <p class="text-sm text-gray-600">Remember to manually log out when using public or shared computers for added security.</p>
              </div>
            </div>
            
            <div class="flex items-start">
              <div class="flex-shrink-0 w-6 h-6 bg-success-100 text-success-600 rounded-full flex items-center justify-center mr-3 mt-0.5">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-3 w-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                </svg>
              </div>
              <div>
                <h4 class="font-medium text-gray-900 mb-1">Enable two-factor authentication</h4>
                <p class="text-sm text-gray-600">Add an extra layer of security to your account with 2FA for enhanced protection.</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Session Information -->
        <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6">
          <h3 class="text-lg font-semibold text-gray-900 mb-4">Session Information</h3>
          
          <div class="grid grid-cols-2 gap-4 text-sm">
            <div>
              <div class="text-gray-500 mb-1">Last Activity</div>
              <div class="font-medium text-gray-900">{{ lastActivity }}</div>
            </div>
            <div>
              <div class="text-gray-500 mb-1">Session Duration</div>
              <div class="font-medium text-gray-900">{{ sessionDuration }}</div>
            </div>
            <div>
              <div class="text-gray-500 mb-1">Device</div>
              <div class="font-medium text-gray-900">{{ deviceInfo }}</div>
            </div>
            <div>
              <div class="text-gray-500 mb-1">Location</div>
              <div class="font-medium text-gray-900">{{ location }}</div>
            </div>
          </div>
          
          <div class="mt-4 pt-4 border-t border-gray-100">
            <p class="text-xs text-gray-500">
              If you notice any suspicious activity, please <NuxtLink to="/support" class="text-primary-600 hover:text-primary-700">contact our support team</NuxtLink> immediately.
            </p>
          </div>
        </div>

        <!-- Auto-redirect countdown -->
        <div v-if="showCountdown" class="mt-6 text-center">
          <p class="text-sm text-gray-500">
            Redirecting to login page in {{ countdown }} seconds...
            <button @click="cancelRedirect" class="text-primary-600 hover:text-primary-700 ml-2">Cancel</button>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

definePageMeta({
  title: 'Session Expired - CoverageX Payment Solutions',
  description: 'Your session has expired. Please sign in again to continue.',
  layout: 'auth'
});

// Reactive state
const lastActivity = ref('');
const sessionDuration = ref('');
const deviceInfo = ref('');
const location = ref('');
const countdown = ref(10);
const showCountdown = ref(true);
let countdownInterval = null;

// Methods
function getLastActivity() {
  // In a real app, this would come from the session data
  const now = new Date();
  const lastActiveTime = new Date(now.getTime() - 15 * 60000); // 15 minutes ago
  lastActivity.value = lastActiveTime.toLocaleString('en-US', {
    month: 'short',
    day: 'numeric',
    hour: '2-digit',
    minute: '2-digit',
    hour12: true
  });
}

function getSessionDuration() {
  // Calculate session duration (example: 2 hours 15 minutes)
  sessionDuration.value = '2h 15m';
}

function getDeviceInfo() {
  // Get basic device information
  const userAgent = navigator.userAgent;
  if (userAgent.includes('Chrome')) {
    deviceInfo.value = 'Chrome Browser';
  } else if (userAgent.includes('Firefox')) {
    deviceInfo.value = 'Firefox Browser';
  } else if (userAgent.includes('Safari')) {
    deviceInfo.value = 'Safari Browser';
  } else {
    deviceInfo.value = 'Web Browser';
  }
}

function getLocation() {
  // In a real app, this would come from the server/session data
  location.value = 'United States';
}

function startCountdown() {
  countdownInterval = setInterval(() => {
    countdown.value--;
    if (countdown.value <= 0) {
      redirectToLogin();
    }
  }, 1000);
}

function cancelRedirect() {
  showCountdown.value = false;
  if (countdownInterval) {
    clearInterval(countdownInterval);
  }
}

function redirectToLogin() {
  navigateTo('/auth/login');
}

onMounted(() => {
  getLastActivity();
  getSessionDuration();
  getDeviceInfo();
  getLocation();
  
  // Start auto-redirect countdown
  startCountdown();
  
  // Clear any existing session data
  if (process.client) {
    localStorage.removeItem('authToken');
    sessionStorage.clear();
  }
});

onUnmounted(() => {
  if (countdownInterval) {
    clearInterval(countdownInterval);
  }
});
</script>

<style scoped>
/* Ensure consistent spacing and typography */
.btn {
  @apply inline-flex items-center justify-center px-6 py-3 border border-transparent text-base font-medium rounded-lg shadow-sm transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-offset-2;
}

.btn-primary {
  @apply text-white bg-primary-600 hover:bg-primary-700 focus:ring-primary-500;
}

.btn-outline-primary {
  @apply text-primary-600 bg-white border-primary-600 hover:bg-primary-50 focus:ring-primary-500;
}
</style>