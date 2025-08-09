<template>
  <div class="fade-in bg-gray-50 min-h-screen">
    <!-- Header Section -->
    <section class="bg-gradient-to-r from-primary-600 to-primary-800 text-white">
      <div class="container-custom py-16">
        <div class="max-w-3xl mx-auto text-center">
          <div class="inline-block mb-4">
            <span class="bg-primary-800 text-primary-100 text-sm font-medium py-1 px-3 rounded-full">
              Cookie Management
            </span>
          </div>
          <h1 class="text-4xl md:text-5xl font-bold mb-4 text-white">Cookie Preferences</h1>
          <p class="text-xl text-primary-100 leading-relaxed">
            Manage your cookie settings and control how we use cookies on our platform.
          </p>
        </div>
      </div>
    </section>

    <!-- Content Section -->
    <section class="py-16">
      <div class="container-custom">
        <div class="max-w-4xl mx-auto">
          <!-- Current Settings Status -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 mb-8">
            <div class="flex items-center justify-between mb-4">
              <h2 class="text-xl font-bold text-gray-900">Current Cookie Settings</h2>
              <div class="flex items-center">
                <div class="h-3 w-3 bg-success-500 rounded-full mr-2"></div>
                <span class="text-sm text-gray-600">Last updated: {{ lastUpdated }}</span>
              </div>
            </div>
            
            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
              <div class="text-center p-4 bg-error-50 rounded-lg">
                <div class="text-2xl font-bold text-error-600">Required</div>
                <div class="text-sm text-gray-600">Essential</div>
              </div>
              <div class="text-center p-4" :class="preferences.functional ? 'bg-success-50' : 'bg-gray-50'">
                <div class="text-2xl font-bold" :class="preferences.functional ? 'text-success-600' : 'text-gray-400'">
                  {{ preferences.functional ? 'Enabled' : 'Disabled' }}
                </div>
                <div class="text-sm text-gray-600">Functional</div>
              </div>
              <div class="text-center p-4" :class="preferences.analytics ? 'bg-success-50' : 'bg-gray-50'">
                <div class="text-2xl font-bold" :class="preferences.analytics ? 'text-success-600' : 'text-gray-400'">
                  {{ preferences.analytics ? 'Enabled' : 'Disabled' }}
                </div>
                <div class="text-sm text-gray-600">Analytics</div>
              </div>
              <div class="text-center p-4" :class="preferences.marketing ? 'bg-success-50' : 'bg-gray-50'">
                <div class="text-2xl font-bold" :class="preferences.marketing ? 'text-success-600' : 'text-gray-400'">
                  {{ preferences.marketing ? 'Enabled' : 'Disabled' }}
                </div>
                <div class="text-sm text-gray-600">Marketing</div>
              </div>
            </div>
          </div>

          <!-- Cookie Categories -->
          <div class="space-y-6">
            <!-- Essential Cookies -->
            <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-8">
              <div class="flex items-start justify-between mb-6">
                <div class="flex items-start">
                  <div class="h-12 w-12 bg-error-100 text-error-600 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
                    </svg>
                  </div>
                  <div>
                    <h3 class="text-xl font-bold text-gray-900 mb-2">Essential Cookies</h3>
                    <p class="text-gray-600 mb-4">These cookies are necessary for the website to function and cannot be switched off in our systems.</p>
                    <div class="text-sm text-gray-500">
                      <strong>Purpose:</strong> Authentication, security, load balancing, session management
                    </div>
                  </div>
                </div>
                <div class="flex items-center">
                  <span class="text-sm font-medium text-error-600 mr-3">Always Active</span>
                  <div class="relative">
                    <input type="checkbox" checked disabled class="sr-only" />
                    <div class="w-12 h-6 bg-error-500 rounded-full shadow-inner"></div>
                    <div class="absolute inset-y-0 right-0 w-6 h-6 bg-white rounded-full shadow transform translate-x-0"></div>
                  </div>
                </div>
              </div>
              
              <div class="bg-gray-50 rounded-lg p-4">
                <h4 class="font-semibold text-gray-900 mb-2">What these cookies do:</h4>
                <ul class="text-sm text-gray-600 space-y-1">
                  <li>• Keep you logged in during your session</li>
                  <li>• Remember your security preferences</li>
                  <li>• Ensure the website loads properly</li>
                  <li>• Protect against security threats</li>
                </ul>
              </div>
            </div>

            <!-- Functional Cookies -->
            <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-8">
              <div class="flex items-start justify-between mb-6">
                <div class="flex items-start">
                  <div class="h-12 w-12 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                    </svg>
                  </div>
                  <div>
                    <h3 class="text-xl font-bold text-gray-900 mb-2">Functional Cookies</h3>
                    <p class="text-gray-600 mb-4">These cookies enable enhanced functionality and personalization.</p>
                    <div class="text-sm text-gray-500">
                      <strong>Purpose:</strong> Remember preferences, settings, and user choices
                    </div>
                  </div>
                </div>
                <div class="flex items-center">
                  <span class="text-sm font-medium text-gray-600 mr-3">{{ preferences.functional ? 'Enabled' : 'Disabled' }}</span>
                  <div class="relative">
                    <input 
                      type="checkbox" 
                      v-model="preferences.functional"
                      @change="updatePreference('functional', preferences.functional)"
                      class="sr-only" 
                    />
                    <div 
                      class="w-12 h-6 rounded-full shadow-inner cursor-pointer transition-colors duration-200"
                      :class="preferences.functional ? 'bg-primary-500' : 'bg-gray-300'"
                      @click="togglePreference('functional')"
                    ></div>
                    <div 
                      class="absolute inset-y-0 w-6 h-6 bg-white rounded-full shadow transform transition-transform duration-200 cursor-pointer"
                      :class="preferences.functional ? 'translate-x-6' : 'translate-x-0'"
                      @click="togglePreference('functional')"
                    ></div>
                  </div>
                </div>
              </div>
              
              <div class="bg-gray-50 rounded-lg p-4">
                <h4 class="font-semibold text-gray-900 mb-2">What these cookies do:</h4>
                <ul class="text-sm text-gray-600 space-y-1">
                  <li>• Remember your language and region preferences</li>
                  <li>• Save your display settings (theme, font size)</li>
                  <li>• Remember form data you've previously entered</li>
                  <li>• Customize your experience based on your choices</li>
                </ul>
              </div>
            </div>

            <!-- Analytics Cookies -->
            <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-8">
              <div class="flex items-start justify-between mb-6">
                <div class="flex items-start">
                  <div class="h-12 w-12 bg-secondary-100 text-secondary-600 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
                    </svg>
                  </div>
                  <div>
                    <h3 class="text-xl font-bold text-gray-900 mb-2">Analytics Cookies</h3>
                    <p class="text-gray-600 mb-4">These cookies help us understand how visitors interact with our website.</p>
                    <div class="text-sm text-gray-500">
                      <strong>Purpose:</strong> Website analytics, performance monitoring, user behavior analysis
                    </div>
                  </div>
                </div>
                <div class="flex items-center">
                  <span class="text-sm font-medium text-gray-600 mr-3">{{ preferences.analytics ? 'Enabled' : 'Disabled' }}</span>
                  <div class="relative">
                    <input 
                      type="checkbox" 
                      v-model="preferences.analytics"
                      @change="updatePreference('analytics', preferences.analytics)"
                      class="sr-only" 
                    />
                    <div 
                      class="w-12 h-6 rounded-full shadow-inner cursor-pointer transition-colors duration-200"
                      :class="preferences.analytics ? 'bg-secondary-500' : 'bg-gray-300'"
                      @click="togglePreference('analytics')"
                    ></div>
                    <div 
                      class="absolute inset-y-0 w-6 h-6 bg-white rounded-full shadow transform transition-transform duration-200 cursor-pointer"
                      :class="preferences.analytics ? 'translate-x-6' : 'translate-x-0'"
                      @click="togglePreference('analytics')"
                    ></div>
                  </div>
                </div>
              </div>
              
              <div class="bg-gray-50 rounded-lg p-4">
                <h4 class="font-semibold text-gray-900 mb-2">What these cookies do:</h4>
                <ul class="text-sm text-gray-600 space-y-1">
                  <li>• Track page views and user journeys (anonymized)</li>
                  <li>• Monitor website performance and errors</li>
                  <li>• Help us understand popular features and content</li>
                  <li>• Improve our website based on usage patterns</li>
                </ul>
                <div class="mt-3 text-xs text-gray-500">
                  <strong>Providers:</strong> Google Analytics, Hotjar
                </div>
              </div>
            </div>

            <!-- Marketing Cookies -->
            <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-8">
              <div class="flex items-start justify-between mb-6">
                <div class="flex items-start">
                  <div class="h-12 w-12 bg-accent-100 text-accent-600 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z" />
                    </svg>
                  </div>
                  <div>
                    <h3 class="text-xl font-bold text-gray-900 mb-2">Marketing Cookies</h3>
                    <p class="text-gray-600 mb-4">These cookies are used to deliver relevant advertisements and track their effectiveness.</p>
                    <div class="text-sm text-gray-500">
                      <strong>Purpose:</strong> Advertising, retargeting, conversion tracking, social media integration
                    </div>
                  </div>
                </div>
                <div class="flex items-center">
                  <span class="text-sm font-medium text-gray-600 mr-3">{{ preferences.marketing ? 'Enabled' : 'Disabled' }}</span>
                  <div class="relative">
                    <input 
                      type="checkbox" 
                      v-model="preferences.marketing"
                      @change="updatePreference('marketing', preferences.marketing)"
                      class="sr-only" 
                    />
                    <div 
                      class="w-12 h-6 rounded-full shadow-inner cursor-pointer transition-colors duration-200"
                      :class="preferences.marketing ? 'bg-accent-500' : 'bg-gray-300'"
                      @click="togglePreference('marketing')"
                    ></div>
                    <div 
                      class="absolute inset-y-0 w-6 h-6 bg-white rounded-full shadow transform transition-transform duration-200 cursor-pointer"
                      :class="preferences.marketing ? 'translate-x-6' : 'translate-x-0'"
                      @click="togglePreference('marketing')"
                    ></div>
                  </div>
                </div>
              </div>
              
              <div class="bg-gray-50 rounded-lg p-4">
                <h4 class="font-semibold text-gray-900 mb-2">What these cookies do:</h4>
                <ul class="text-sm text-gray-600 space-y-1">
                  <li>• Show you relevant advertisements based on your interests</li>
                  <li>• Track conversion from ads to measure effectiveness</li>
                  <li>• Enable retargeting and remarketing campaigns</li>
                  <li>• Integrate with social media platforms</li>
                </ul>
                <div class="mt-3 text-xs text-gray-500">
                  <strong>Providers:</strong> Google Ads, Facebook Pixel, LinkedIn Insight Tag
                </div>
              </div>
            </div>
          </div>

          <!-- Action Buttons -->
          <div class="mt-8 bg-white rounded-xl shadow-sm border border-gray-100 p-8">
            <div class="flex flex-col sm:flex-row gap-4 justify-between items-center">
              <div>
                <h3 class="text-lg font-bold text-gray-900 mb-2">Save Your Preferences</h3>
                <p class="text-sm text-gray-600">Your choices will be saved and applied across our website.</p>
              </div>
              
              <div class="flex flex-col sm:flex-row gap-3">
                <button
                  @click="acceptAll"
                  class="btn bg-success-500 text-white hover:bg-success-600 focus:ring-success-500"
                >
                  Accept All Cookies
                </button>
                <button
                  @click="rejectOptional"
                  class="btn bg-gray-500 text-white hover:bg-gray-600 focus:ring-gray-500"
                >
                  Reject Optional
                </button>
                <button
                  @click="savePreferences"
                  class="btn btn-primary"
                  :disabled="saving"
                >
                  <span v-if="saving">Saving...</span>
                  <span v-else>Save Preferences</span>
                </button>
              </div>
            </div>
          </div>

          <!-- Additional Information -->
          <div class="mt-8 bg-white rounded-xl shadow-sm border border-gray-100 p-8">
            <h3 class="text-lg font-bold text-gray-900 mb-4">Additional Information</h3>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div>
                <h4 class="font-semibold text-gray-900 mb-2">Browser Settings</h4>
                <p class="text-sm text-gray-600 mb-3">You can also manage cookies through your browser settings. Note that disabling cookies may affect website functionality.</p>
                <NuxtLink to="/legal/cookies#browser-settings" class="text-primary-600 hover:text-primary-700 text-sm font-medium">
                  Learn about browser settings →
                </NuxtLink>
              </div>
              
              <div>
                <h4 class="font-semibold text-gray-900 mb-2">Questions?</h4>
                <p class="text-sm text-gray-600 mb-3">If you have questions about our cookie practices, please don't hesitate to contact us.</p>
                <div class="space-y-1">
                  <p class="text-sm"><strong>Email:</strong> <a href="mailto:privacy@coveragex.com" class="text-primary-600 hover:text-primary-700">privacy@coveragex.com</a></p>
                  <p class="text-sm"><strong>Support:</strong> <NuxtLink to="/support" class="text-primary-600 hover:text-primary-700">Visit Support Center</NuxtLink></p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Success Toast -->
    <div 
      v-if="showSuccessToast" 
      class="fixed bottom-4 right-4 bg-success-500 text-white px-6 py-3 rounded-lg shadow-lg z-50 transition-all duration-300"
    >
      <div class="flex items-center">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
        </svg>
        Cookie preferences saved successfully!
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted } from 'vue';

definePageMeta({
  title: 'Cookie Preferences - CoverageX Payment Solutions',
  description: 'Manage your cookie preferences and control how we use cookies on our platform.'
});

// Reactive state
const preferences = reactive({
  functional: true,
  analytics: true,
  marketing: false
});

const saving = ref(false);
const showSuccessToast = ref(false);
const lastUpdated = ref('');

// Load preferences from localStorage on mount
onMounted(() => {
  loadPreferences();
  updateLastUpdatedTime();
});

function loadPreferences() {
  if (process.client) {
    const saved = localStorage.getItem('cookiePreferences');
    if (saved) {
      const parsed = JSON.parse(saved);
      Object.assign(preferences, parsed);
    }
  }
}

function updateLastUpdatedTime() {
  const now = new Date();
  lastUpdated.value = now.toLocaleDateString('en-US', { 
    year: 'numeric', 
    month: 'short', 
    day: 'numeric',
    hour: '2-digit',
    minute: '2-digit'
  });
}

function togglePreference(type) {
  preferences[type] = !preferences[type];
  updatePreference(type, preferences[type]);
}

function updatePreference(type, value) {
  // Immediately save to localStorage
  if (process.client) {
    const currentPrefs = JSON.parse(localStorage.getItem('cookiePreferences') || '{}');
    currentPrefs[type] = value;
    localStorage.setItem('cookiePreferences', JSON.stringify(currentPrefs));
  }
}

async function savePreferences() {
  saving.value = true;
  
  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    // Save to localStorage
    if (process.client) {
      localStorage.setItem('cookiePreferences', JSON.stringify(preferences));
    }
    
    updateLastUpdatedTime();
    showSuccessToast.value = true;
    
    // Hide toast after 3 seconds
    setTimeout(() => {
      showSuccessToast.value = false;
    }, 3000);
    
  } catch (error) {
    console.error('Error saving preferences:', error);
  } finally {
    saving.value = false;
  }
}

function acceptAll() {
  preferences.functional = true;
  preferences.analytics = true;
  preferences.marketing = true;
  savePreferences();
}

function rejectOptional() {
  preferences.functional = false;
  preferences.analytics = false;
  preferences.marketing = false;
  savePreferences();
}
</script>

<style scoped>
.transition-transform {
  transition-property: transform;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 200ms;
}

.transition-colors {
  transition-property: color, background-color, border-color, text-decoration-color, fill, stroke;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 200ms;
}
</style>