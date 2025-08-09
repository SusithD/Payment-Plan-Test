<template>
  <div class="fade-in bg-gray-50 min-h-screen">
    <!-- Header Section -->
    <section class="bg-gradient-to-r from-primary-600 to-primary-800 text-white">
      <div class="container-custom py-16">
        <div class="max-w-3xl mx-auto text-center">
          <div class="inline-block mb-4">
            <span class="bg-primary-800 text-primary-100 text-sm font-medium py-1 px-3 rounded-full">
              Product Updates
            </span>
          </div>
          <h1 class="text-4xl md:text-5xl font-bold mb-4 text-white">What's New</h1>
          <p class="text-xl text-primary-100 leading-relaxed">
            Stay up to date with the latest features, improvements, and updates to our payment platform.
          </p>
        </div>
      </div>
    </section>

    <!-- Content Section -->
    <section class="py-16">
      <div class="container-custom">
        <div class="max-w-4xl mx-auto">
          <!-- Filter Options -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 mb-8">
            <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4">
              <h2 class="text-xl font-bold text-gray-900">Changelog</h2>
              
              <div class="flex flex-col sm:flex-row gap-3">
                <select v-model="selectedCategory" class="form-input text-sm">
                  <option value="all">All Categories</option>
                  <option value="feature">New Features</option>
                  <option value="improvement">Improvements</option>
                  <option value="bugfix">Bug Fixes</option>
                  <option value="security">Security</option>
                </select>
                
                <div class="flex items-center gap-2">
                  <label class="text-sm text-gray-600">Show only major updates:</label>
                  <input 
                    type="checkbox" 
                    v-model="showMajorOnly" 
                    class="rounded border-gray-300 text-primary-600 focus:ring-primary-500"
                  />
                </div>
              </div>
            </div>
          </div>

          <!-- Latest Update Highlight -->
          <div class="bg-gradient-to-r from-primary-50 to-primary-100 rounded-xl shadow-sm border border-primary-200 p-8 mb-8">
            <div class="flex items-start">
              <div class="h-12 w-12 bg-primary-500 text-white rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
                </svg>
              </div>
              <div>
                <div class="flex items-center gap-2 mb-2">
                  <span class="text-xs bg-primary-200 text-primary-800 px-2 py-1 rounded-full font-medium">LATEST</span>
                  <span class="text-sm text-primary-700 font-medium">August 9, 2025</span>
                </div>
                <h3 class="text-xl font-bold text-gray-900 mb-2">Enhanced Payment Analytics Dashboard</h3>
                <p class="text-gray-700 mb-4">We've completely redesigned the analytics dashboard with new visualizations, better performance, and more detailed insights into your payment patterns.</p>
                <div class="flex flex-wrap gap-2">
                  <span class="text-xs bg-accent-100 text-accent-800 px-2 py-1 rounded-full">New Feature</span>
                  <span class="text-xs bg-secondary-100 text-secondary-800 px-2 py-1 rounded-full">Dashboard</span>
                  <span class="text-xs bg-success-100 text-success-800 px-2 py-1 rounded-full">Analytics</span>
                </div>
              </div>
            </div>
          </div>

          <!-- Changelog Timeline -->
          <div class="space-y-8">
            <div v-for="(entry, index) in filteredChangelog" :key="index" class="relative">
              <!-- Timeline Line -->
              <div v-if="index < filteredChangelog.length - 1" class="absolute left-6 top-16 w-0.5 h-full bg-gray-200"></div>
              
              <!-- Changelog Entry -->
              <div class="flex items-start">
                <!-- Timeline Dot -->
                <div 
                  class="h-12 w-12 rounded-full flex items-center justify-center mr-6 flex-shrink-0 relative z-10"
                  :class="{
                    'bg-accent-100 text-accent-600': entry.type === 'feature',
                    'bg-primary-100 text-primary-600': entry.type === 'improvement',
                    'bg-success-100 text-success-600': entry.type === 'bugfix',
                    'bg-error-100 text-error-600': entry.type === 'security'
                  }"
                >
                  <svg v-if="entry.type === 'feature'" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
                  </svg>
                  <svg v-else-if="entry.type === 'improvement'" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6" />
                  </svg>
                  <svg v-else-if="entry.type === 'bugfix'" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                  <svg v-else-if="entry.type === 'security'" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
                  </svg>
                </div>
                
                <!-- Entry Content -->
                <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 flex-1">
                  <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-2 mb-4">
                    <div class="flex items-center gap-2">
                      <span 
                        class="text-xs px-2 py-1 rounded-full font-medium"
                        :class="{
                          'bg-accent-100 text-accent-800': entry.type === 'feature',
                          'bg-primary-100 text-primary-800': entry.type === 'improvement',
                          'bg-success-100 text-success-800': entry.type === 'bugfix',
                          'bg-error-100 text-error-800': entry.type === 'security'
                        }"
                      >
                        {{ getTypeLabel(entry.type) }}
                      </span>
                      <span v-if="entry.major" class="text-xs bg-warning-100 text-warning-800 px-2 py-1 rounded-full font-medium">
                        MAJOR
                      </span>
                    </div>
                    <span class="text-sm text-gray-500 font-medium">{{ entry.date }}</span>
                  </div>
                  
                  <h3 class="text-lg font-bold text-gray-900 mb-3">{{ entry.title }}</h3>
                  <p class="text-gray-600 mb-4">{{ entry.description }}</p>
                  
                  <div v-if="entry.changes && entry.changes.length > 0" class="space-y-2">
                    <h4 class="font-semibold text-gray-900 text-sm">Changes:</h4>
                    <ul class="text-sm text-gray-600 space-y-1">
                      <li v-for="(change, changeIndex) in entry.changes" :key="changeIndex" class="flex items-start">
                        <span class="mr-2 mt-1.5 h-1.5 w-1.5 bg-gray-400 rounded-full flex-shrink-0"></span>
                        {{ change }}
                      </li>
                    </ul>
                  </div>
                  
                  <div v-if="entry.tags && entry.tags.length > 0" class="flex flex-wrap gap-2 mt-4 pt-4 border-t border-gray-100">
                    <span 
                      v-for="tag in entry.tags" 
                      :key="tag" 
                      class="text-xs bg-gray-100 text-gray-600 px-2 py-1 rounded-full"
                    >
                      {{ tag }}
                    </span>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Load More Button -->
          <div v-if="hasMoreEntries" class="mt-12 text-center">
            <button 
              @click="loadMoreEntries"
              class="btn btn-outline-primary"
              :disabled="loading"
            >
              <span v-if="loading">Loading...</span>
              <span v-else>Load More Updates</span>
            </button>
          </div>

          <!-- Subscribe to Updates -->
          <div class="mt-12 bg-white rounded-xl shadow-sm border border-gray-100 p-8">
            <div class="text-center">
              <div class="h-16 w-16 bg-accent-100 text-accent-600 rounded-full flex items-center justify-center mx-auto mb-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
                </svg>
              </div>
              <h3 class="text-xl font-bold text-gray-900 mb-2">Stay Updated</h3>
              <p class="text-gray-600 mb-6">Get notified when we release new features and important updates.</p>
              
              <div class="max-w-md mx-auto">
                <div class="flex gap-3">
                  <input 
                    type="email" 
                    v-model="subscriptionEmail"
                    placeholder="Enter your email"
                    class="form-input flex-1"
                  />
                  <button 
                    @click="subscribeToUpdates"
                    class="btn btn-primary"
                    :disabled="!subscriptionEmail || subscribing"
                  >
                    <span v-if="subscribing">Subscribing...</span>
                    <span v-else>Subscribe</span>
                  </button>
                </div>
                <p class="text-xs text-gray-500 mt-2">We'll only send you important updates. No spam.</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Success Toast -->
    <div 
      v-if="showSubscriptionToast" 
      class="fixed bottom-4 right-4 bg-success-500 text-white px-6 py-3 rounded-lg shadow-lg z-50 transition-all duration-300"
    >
      <div class="flex items-center">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
        </svg>
        Successfully subscribed to updates!
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

definePageMeta({
  title: 'Changelog - What\'s New | CoverageX Payment Solutions',
  description: 'Stay up to date with the latest features, improvements, and updates to our payment platform.'
});

// Reactive state
const selectedCategory = ref('all');
const showMajorOnly = ref(false);
const subscriptionEmail = ref('');
const subscribing = ref(false);
const showSubscriptionToast = ref(false);
const loading = ref(false);
const hasMoreEntries = ref(true);
const displayedEntries = ref(10);

// Sample changelog data
const changelog = ref([
  {
    date: 'August 9, 2025',
    type: 'feature',
    major: true,
    title: 'Enhanced Payment Analytics Dashboard',
    description: 'We\'ve completely redesigned the analytics dashboard with new visualizations, better performance, and more detailed insights into your payment patterns.',
    changes: [
      'Added real-time payment tracking charts',
      'Introduced payment trend analysis',
      'New export functionality for reports',
      'Improved mobile responsiveness'
    ],
    tags: ['Dashboard', 'Analytics', 'Reporting']
  },
  {
    date: 'August 2, 2025',
    type: 'improvement',
    major: false,
    title: 'Faster Payment Processing',
    description: 'Optimized our payment processing engine to reduce transaction times by 40%.',
    changes: [
      'Streamlined API calls for payment verification',
      'Enhanced database query performance',
      'Reduced third-party service dependencies'
    ],
    tags: ['Performance', 'API', 'Backend']
  },
  {
    date: 'July 28, 2025',
    type: 'feature',
    major: true,
    title: 'Multi-Currency Support',
    description: 'You can now accept payments in over 150 currencies with automatic conversion rates.',
    changes: [
      'Added support for 150+ currencies',
      'Real-time exchange rate updates',
      'Currency conversion calculator',
      'Localized currency formatting'
    ],
    tags: ['Payments', 'International', 'Currency']
  },
  {
    date: 'July 21, 2025',
    type: 'security',
    major: true,
    title: 'Enhanced Security Measures',
    description: 'Implemented additional security layers including advanced fraud detection and two-factor authentication.',
    changes: [
      'Added two-factor authentication',
      'Enhanced fraud detection algorithms',
      'Improved SSL certificate management',
      'Regular security audits'
    ],
    tags: ['Security', 'Authentication', 'Fraud Prevention']
  },
  {
    date: 'July 15, 2025',
    type: 'bugfix',
    major: false,
    title: 'Payment History Export Fix',
    description: 'Fixed an issue where some payment history exports were incomplete.',
    changes: [
      'Resolved CSV export formatting issues',
      'Fixed date range filter problems',
      'Improved error handling for large exports'
    ],
    tags: ['Bug Fix', 'Export', 'History']
  },
  {
    date: 'July 8, 2025',
    type: 'improvement',
    major: false,
    title: 'Mobile App Performance',
    description: 'Significant performance improvements for the mobile application.',
    changes: [
      'Reduced app loading time by 50%',
      'Optimized image loading',
      'Improved offline functionality',
      'Enhanced push notification delivery'
    ],
    tags: ['Mobile', 'Performance', 'User Experience']
  },
  {
    date: 'June 30, 2025',
    type: 'feature',
    major: true,
    title: 'Automated Payment Reminders',
    description: 'Set up customizable payment reminders to help your customers stay on track.',
    changes: [
      'Configurable reminder schedules',
      'Email and SMS notification options',
      'Customizable message templates',
      'Reminder analytics and tracking'
    ],
    tags: ['Automation', 'Notifications', 'Customer Engagement']
  },
  {
    date: 'June 22, 2025',
    type: 'improvement',
    major: false,
    title: 'API Documentation Update',
    description: 'Comprehensive update to our API documentation with interactive examples.',
    changes: [
      'Added interactive API explorer',
      'Updated code examples for all endpoints',
      'Improved error response documentation',
      'Added postman collection'
    ],
    tags: ['API', 'Documentation', 'Developer Experience']
  },
  {
    date: 'June 15, 2025',
    type: 'feature',
    major: false,
    title: 'Dark Mode Support',
    description: 'Added dark mode theme option for better viewing experience.',
    changes: [
      'Dark theme for all pages',
      'Automatic system theme detection',
      'User preference saving',
      'Improved contrast ratios'
    ],
    tags: ['UI/UX', 'Accessibility', 'Theme']
  },
  {
    date: 'June 8, 2025',
    type: 'bugfix',
    major: false,
    title: 'Payment Schedule Display Fix',
    description: 'Fixed timezone-related issues in payment schedule display.',
    changes: [
      'Corrected timezone handling',
      'Fixed date format inconsistencies',
      'Improved calendar integration'
    ],
    tags: ['Bug Fix', 'Timezone', 'Calendar']
  }
]);

// Computed properties
const filteredChangelog = computed(() => {
  let filtered = changelog.value;
  
  if (selectedCategory.value !== 'all') {
    filtered = filtered.filter(entry => entry.type === selectedCategory.value);
  }
  
  if (showMajorOnly.value) {
    filtered = filtered.filter(entry => entry.major);
  }
  
  return filtered.slice(0, displayedEntries.value);
});

// Methods
function getTypeLabel(type) {
  const labels = {
    feature: 'New Feature',
    improvement: 'Improvement',
    bugfix: 'Bug Fix',
    security: 'Security'
  };
  return labels[type] || type;
}

function loadMoreEntries() {
  loading.value = true;
  
  setTimeout(() => {
    displayedEntries.value += 5;
    if (displayedEntries.value >= changelog.value.length) {
      hasMoreEntries.value = false;
    }
    loading.value = false;
  }, 500);
}

async function subscribeToUpdates() {
  if (!subscriptionEmail.value) return;
  
  subscribing.value = true;
  
  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    showSubscriptionToast.value = true;
    subscriptionEmail.value = '';
    
    // Hide toast after 3 seconds
    setTimeout(() => {
      showSubscriptionToast.value = false;
    }, 3000);
    
  } catch (error) {
    console.error('Error subscribing:', error);
  } finally {
    subscribing.value = false;
  }
}

onMounted(() => {
  // Any initialization logic
});
</script>

<style scoped>
.form-input {
  @apply w-full rounded-lg border-2 border-gray-200 bg-gray-50 shadow-sm focus:border-primary-500 focus:ring focus:ring-primary-500 focus:ring-opacity-50 transition-all duration-200 py-2 px-3;
}
</style>