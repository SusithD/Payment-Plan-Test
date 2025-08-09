<template>
  <div class="fade-in bg-gray-50 min-h-screen flex items-center justify-center">
    <div class="container-custom py-16">
      <div class="max-w-2xl mx-auto text-center">
        <!-- Maintenance Icon -->
        <div class="mb-8">
          <div class="h-24 w-24 bg-warning-100 text-warning-600 rounded-full flex items-center justify-center mx-auto mb-6">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
            </svg>
          </div>
          
          <!-- Status Badge -->
          <div class="inline-flex items-center px-4 py-2 rounded-full bg-warning-100 text-warning-800 text-sm font-medium">
            <div class="h-2 w-2 bg-warning-500 rounded-full mr-2 animate-pulse"></div>
            System Under Maintenance
          </div>
        </div>

        <!-- Main Content -->
        <div class="bg-white rounded-2xl shadow-xl p-8 mb-8">
          <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
            We'll Be Right Back
          </h1>
          
          <p class="text-xl text-gray-600 mb-6 leading-relaxed">
            We're currently performing scheduled maintenance to improve your experience. Our payment platform will be back online shortly.
          </p>

          <!-- Estimated Time -->
          <div class="bg-primary-50 border border-primary-200 rounded-lg p-6 mb-6">
            <div class="flex items-center justify-center mb-3">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
              <h3 class="text-lg font-semibold text-primary-900">Estimated Duration</h3>
            </div>
            <div class="text-center">
              <div class="text-2xl font-bold text-primary-700 mb-1">{{ estimatedTime }}</div>
              <div class="text-sm text-primary-600">Expected completion: {{ expectedCompletion }}</div>
            </div>
          </div>

          <!-- What We're Doing -->
          <div class="text-left mb-6">
            <h3 class="text-lg font-semibold text-gray-900 mb-4">What we're working on:</h3>
            <div class="space-y-3">
              <div class="flex items-start">
                <div class="h-2 w-2 bg-success-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
                <span class="text-gray-600">Upgrading payment processing systems</span>
              </div>
              <div class="flex items-start">
                <div class="h-2 w-2 bg-success-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
                <span class="text-gray-600">Enhancing security measures</span>
              </div>
              <div class="flex items-start">
                <div class="h-2 w-2 bg-warning-500 rounded-full mt-2 mr-3 flex-shrink-0 animate-pulse"></div>
                <span class="text-gray-600">Improving database performance</span>
              </div>
              <div class="flex items-start">
                <div class="h-2 w-2 bg-gray-300 rounded-full mt-2 mr-3 flex-shrink-0"></div>
                <span class="text-gray-600">Testing system reliability</span>
              </div>
            </div>
          </div>

          <!-- Progress Bar -->
          <div class="mb-6">
            <div class="flex justify-between text-sm text-gray-600 mb-2">
              <span>Progress</span>
              <span>{{ progress }}%</span>
            </div>
            <div class="w-full bg-gray-200 rounded-full h-2">
              <div 
                class="bg-primary-500 h-2 rounded-full transition-all duration-1000 ease-out"
                :style="{ width: progress + '%' }"
              ></div>
            </div>
          </div>
        </div>

        <!-- Contact Information -->
        <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 mb-8">
          <h3 class="text-lg font-semibold text-gray-900 mb-4">Need Immediate Assistance?</h3>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div class="text-center p-4 bg-gray-50 rounded-lg">
              <div class="h-10 w-10 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mx-auto mb-2">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                </svg>
              </div>
              <h4 class="font-semibold text-gray-900 mb-1">Email Support</h4>
              <p class="text-sm text-gray-600 mb-2">For non-urgent inquiries</p>
              <a href="mailto:support@coveragex.com" class="text-primary-600 hover:text-primary-700 text-sm font-medium">
                support@coveragex.com
              </a>
            </div>
            
            <div class="text-center p-4 bg-gray-50 rounded-lg">
              <div class="h-10 w-10 bg-error-100 text-error-600 rounded-full flex items-center justify-center mx-auto mb-2">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 18h.01M8 21h8a2 2 0 002-2V5a2 2 0 00-2-2H8a2 2 0 00-2 2v14a2 2 0 002 2z" />
                </svg>
              </div>
              <h4 class="font-semibold text-gray-900 mb-1">Emergency Contact</h4>
              <p class="text-sm text-gray-600 mb-2">For urgent payment issues</p>
              <a href="tel:+18001234567" class="text-error-600 hover:text-error-700 text-sm font-medium">
                +1 (800) 123-4567
              </a>
            </div>
          </div>
        </div>

        <!-- Status Updates -->
        <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6">
          <h3 class="text-lg font-semibold text-gray-900 mb-4">Recent Updates</h3>
          
          <div class="space-y-4 text-left">
            <div v-for="update in statusUpdates" :key="update.id" class="flex items-start">
              <div class="flex-shrink-0 w-2 h-2 bg-primary-500 rounded-full mt-2 mr-3"></div>
              <div class="flex-1">
                <div class="flex items-center justify-between mb-1">
                  <span class="text-sm font-medium text-gray-900">{{ update.title }}</span>
                  <span class="text-xs text-gray-500">{{ update.time }}</span>
                </div>
                <p class="text-sm text-gray-600">{{ update.description }}</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Auto Refresh Notice -->
        <div class="mt-8 text-center">
          <p class="text-sm text-gray-500">
            This page automatically refreshes every 30 seconds to provide the latest updates.
            <br>
            Last updated: {{ lastUpdated }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

definePageMeta({
  title: 'System Maintenance - CoverageX Payment Solutions',
  description: 'Our payment platform is currently under maintenance. We\'ll be back online shortly.'
});

// Reactive state
const progress = ref(65);
const estimatedTime = ref('30 minutes');
const expectedCompletion = ref('');
const lastUpdated = ref('');
let refreshInterval = null;
let progressInterval = null;

// Sample status updates
const statusUpdates = ref([
  {
    id: 1,
    title: 'Database optimization in progress',
    description: 'Currently optimizing database queries for better performance.',
    time: '10 minutes ago'
  },
  {
    id: 2,
    title: 'Security enhancements completed',
    description: 'Successfully upgraded security protocols and encryption.',
    time: '25 minutes ago'
  },
  {
    id: 3,
    title: 'Maintenance window started',
    description: 'Scheduled maintenance has begun. Estimated duration: 1 hour.',
    time: '45 minutes ago'
  }
]);

// Methods
function updateLastUpdated() {
  const now = new Date();
  lastUpdated.value = now.toLocaleTimeString('en-US', {
    hour: '2-digit',
    minute: '2-digit',
    second: '2-digit',
    hour12: true
  });
}

function updateExpectedCompletion() {
  const now = new Date();
  const completion = new Date(now.getTime() + 30 * 60000); // 30 minutes from now
  expectedCompletion.value = completion.toLocaleTimeString('en-US', {
    hour: '2-digit',
    minute: '2-digit',
    hour12: true
  });
}

function simulateProgress() {
  // Slowly increase progress
  if (progress.value < 95) {
    progress.value += Math.random() * 2;
    if (progress.value > 95) progress.value = 95;
  }
  
  // Update estimated time based on progress
  if (progress.value > 80) {
    estimatedTime.value = '10 minutes';
  } else if (progress.value > 70) {
    estimatedTime.value = '20 minutes';
  }
}

function refreshPage() {
  updateLastUpdated();
  updateExpectedCompletion();
  
  // In a real scenario, you might check server status here
  // and redirect to the main site if maintenance is complete
}

onMounted(() => {
  updateLastUpdated();
  updateExpectedCompletion();
  
  // Set up auto refresh every 30 seconds
  refreshInterval = setInterval(refreshPage, 30000);
  
  // Set up progress simulation every 10 seconds
  progressInterval = setInterval(simulateProgress, 10000);
});

onUnmounted(() => {
  if (refreshInterval) {
    clearInterval(refreshInterval);
  }
  if (progressInterval) {
    clearInterval(progressInterval);
  }
});
</script>

<style scoped>
@keyframes pulse {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.5;
  }
}

.animate-pulse {
  animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
</style>