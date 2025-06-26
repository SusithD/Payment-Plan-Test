<template>
  <div class="min-h-screen flex">
    <!-- Left side - Phone verification form -->
    <div class="w-full lg:w-1/2 bg-white flex flex-col justify-center px-6 sm:px-10 lg:px-16 xl:px-24 relative z-10">
      <div class="absolute top-8 left-8">
        <NuxtLink to="/" class="flex items-center">
          <span class="text-2xl font-bold gradient-text">PaymentPlan</span>
        </NuxtLink>
      </div>
      
      <div class="max-w-md mx-auto w-full py-20 lg:py-12">
        <div class="mb-8 text-center">
          <div class="mx-auto flex items-center justify-center h-16 w-16 rounded-full bg-primary-100 mb-4">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
            </svg>
          </div>
          <h2 class="text-3xl font-bold text-gray-900 mb-3">Verify your phone number</h2>
          <p class="text-gray-600">
            We need to verify your phone number to secure your account and enable payment notifications
          </p>
        </div>

        <form @submit.prevent="handleSubmit" class="space-y-6">
          <div class="form-group">
            <label for="mobile" class="form-label">Mobile number</label>
            <div class="mobile-input-container">
              <div class="relative">
                <svg xmlns="http://www.w3.org/2000/svg" class="input-icon h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                </svg>
                <select 
                  v-model="countryCode" 
                  class="auth-input country-select focus:ring-2 focus:ring-primary-500 transition-all duration-200"
                >
                  <option v-for="country in countries" :key="country.code" :value="country.code">
                    {{ country.code }} {{ country.flag }}
                  </option>
                </select>
              </div>
              <input 
                id="mobile" 
                v-model="mobile" 
                type="tel" 
                autocomplete="tel" 
                required 
                class="auth-input mobile-input focus:ring-2 focus:ring-primary-500 transition-all duration-200" 
                placeholder="Enter your mobile number"
                :class="{'border-red-300 focus:ring-red-500 error': mobileError}"
              />
            </div>
            <p class="mt-2 text-xs text-gray-500">We'll send a verification code to this number</p>
            <p v-if="mobileError" class="form-error">{{ mobileError }}</p>
          </div>

          <button 
            type="submit" 
            class="w-full btn-gradient py-3 rounded-xl text-lg font-medium relative overflow-hidden group transform transition hover:scale-[1.02] active:scale-[0.98]"
            :disabled="isLoading"
          >
            <div class="absolute top-0 left-0 w-full h-full bg-white opacity-0 group-hover:opacity-10 transition-opacity"></div>
            <span class="relative flex items-center justify-center">
              <span v-if="isLoading" class="mr-2">
                <svg class="animate-spin h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                  <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                  <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                </svg>
              </span>
              <span>
                {{ isLoading ? 'Sending code...' : 'Send verification code' }}
              </span>
              <svg v-if="!isLoading" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M10.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L12.586 11H5a1 1 0 110-2h7.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd" />
              </svg>
            </span>
          </button>
        </form>

        <!-- Security Notice -->
        <div class="mt-8 p-4 bg-gray-50 rounded-lg border border-gray-200">
          <div class="flex items-start">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400 mr-3 mt-0.5 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
            </svg>
            <div>
              <h4 class="text-sm font-medium text-gray-900 mb-1">Why do we need your phone number?</h4>
              <ul class="text-xs text-gray-600 space-y-1">
                <li>• Secure two-factor authentication</li>
                <li>• Payment reminders and notifications</li>
                <li>• Account recovery and security alerts</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
      
      <div class="absolute bottom-6 left-0 right-0 text-center text-xs text-gray-500">
        <p>© 2025 PaymentPlan. All rights reserved.</p>
      </div>
    </div>
    
    <!-- Right side - Image section -->
    <div class="hidden lg:block lg:w-1/2 relative overflow-hidden">
      <!-- Background Image with gradient overlay -->
      <div class="absolute inset-0 bg-cover bg-center" style="background-image: url('https://images.unsplash.com/photo-1556742049-0cfed4f6a45d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2340&q=80');">
        <div class="absolute inset-0 bg-gradient-to-br from-primary-900/90 via-primary-800/80 to-primary-700/70"></div>
      </div>
      
      <!-- Content overlay -->
      <div class="relative z-10 flex flex-col h-full p-12 justify-center">
        <div class="max-w-lg">
          <div class="inline-flex items-center px-4 py-2 rounded-full bg-white/10 backdrop-blur-md mb-6 border border-white/20">
            <span class="flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white mr-2" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M2.166 4.999A11.954 11.954 0 0010 1.944 11.954 11.954 0 0017.834 5c.11.65.166 1.32.166 2.001 0 5.225-3.34 9.67-8 11.317C5.34 16.67 2 12.225 2 7c0-.682.057-1.35.166-2.001zm11.541 3.708a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
              </svg>
              <span class="text-white font-medium">Secure verification</span>
            </span>
          </div>
          
          <h2 class="text-4xl font-bold text-white mb-6 leading-tight">
            Your security is our <span class="text-accent-300">priority</span>
          </h2>
          
          <p class="text-white/90 text-xl leading-relaxed mb-8">
            We use phone verification to ensure your account is protected and to send you important payment alerts.
          </p>
          
          <!-- Security features -->
          <div class="space-y-4">
            <div class="flex items-center space-x-3">
              <div class="flex-shrink-0 h-8 w-8 rounded-full bg-success-500/20 flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-success-300" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                </svg>
              </div>
              <span class="text-white">SMS codes expire in 5 minutes</span>
            </div>
            <div class="flex items-center space-x-3">
              <div class="flex-shrink-0 h-8 w-8 rounded-full bg-success-500/20 flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-success-300" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                </svg>
              </div>
              <span class="text-white">Your number is encrypted and secure</span>
            </div>
            <div class="flex items-center space-x-3">
              <div class="flex-shrink-0 h-8 w-8 rounded-full bg-success-500/20 flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-success-300" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                </svg>
              </div>
              <span class="text-white">No spam or marketing messages</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

definePageMeta({
  layout: false,
});

const router = useRouter();
const mobile = ref('');
const countryCode = ref('+1');
const isLoading = ref(false);
const mobileError = ref('');

const countries = ref([
  { code: '+1', name: 'United States/Canada', flag: '🇺🇸' },
  { code: '+44', name: 'United Kingdom', flag: '🇬🇧' },
  { code: '+91', name: 'India', flag: '🇮🇳' },
  { code: '+61', name: 'Australia', flag: '🇦🇺' },
  { code: '+64', name: 'New Zealand', flag: '🇳🇿' },
  { code: '+49', name: 'Germany', flag: '🇩🇪' },
  { code: '+33', name: 'France', flag: '🇫🇷' },
  { code: '+81', name: 'Japan', flag: '🇯🇵' },
  { code: '+86', name: 'China', flag: '🇨🇳' },
  { code: '+65', name: 'Singapore', flag: '🇸🇬' },
]);

const validatePhone = () => {
  mobileError.value = '';
  
  if (!mobile.value) {
    mobileError.value = 'Mobile number is required';
    return false;
  }
  
  if (!/^\d{10,15}$/.test(mobile.value.replace(/\s+/g, ''))) {
    mobileError.value = 'Please enter a valid mobile number';
    return false;
  }
  
  return true;
};

const handleSubmit = async () => {
  if (!validatePhone()) return;
  
  try {
    isLoading.value = true;
    
    // Simulate sending OTP
    await new Promise(resolve => setTimeout(resolve, 1500));
    
    // Store phone details in session/localStorage for OTP verification
    sessionStorage.setItem('phone-verification', JSON.stringify({
      mobile: mobile.value,
      countryCode: countryCode.value
    }));
    
    // Redirect to OTP verification
    router.push('/auth/verify-otp');
  } catch (error) {
    console.error('Failed to send OTP:', error);
    mobileError.value = 'Failed to send verification code. Please try again.';
  } finally {
    isLoading.value = false;
  }
};
</script>

<style scoped>
.form-group {
  animation: fadeIn 0.5s ease-out forwards;
  opacity: 0;
}

.form-group:nth-child(1) {
  animation-delay: 0.1s;
}

button[type="submit"] {
  animation: fadeIn 0.5s ease-out forwards;
  animation-delay: 0.2s;
  opacity: 0;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.gradient-text {
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
  background-image: linear-gradient(to right, var(--tw-gradient-stops));
  --tw-gradient-from: #2C4880;
  --tw-gradient-to: #4476b0;
  --tw-gradient-stops: var(--tw-gradient-from), var(--tw-gradient-to);
}

.btn-gradient {
  background-image: linear-gradient(to right, var(--tw-gradient-stops));
  --tw-gradient-from: #2C4880;
  --tw-gradient-to: #4476b0;
  --tw-gradient-stops: var(--tw-gradient-from), var(--tw-gradient-to);
  color: white;
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
}

.btn-gradient:hover {
  --tw-gradient-from: #253a6c;
  --tw-gradient-to: #355b8f;
  transform: translateY(-1px);
  box-shadow: 0 10px 15px -3px rgba(44, 72, 128, 0.3);
}

.btn-gradient:disabled {
  opacity: 0.6;
  cursor: not-allowed;
  transform: none;
  box-shadow: none;
}
</style>