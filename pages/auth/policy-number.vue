<template>
  <div class="min-h-screen flex">
    <!-- Left side - Policy number form -->
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
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
            </svg>
          </div>
          <h2 class="text-3xl font-bold text-gray-900 mb-3">Enter your policy number</h2>
          <p class="text-gray-600">
            Please provide your insurance policy number to complete your account setup
          </p>
        </div>

        <form @submit.prevent="handleSubmit" class="space-y-6">
          <div class="form-group">
            <label for="policy-number" class="form-label">Policy Number</label>
            <div class="relative">
              <svg xmlns="http://www.w3.org/2000/svg" class="input-icon h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
              </svg>
              <input 
                id="policy-number" 
                v-model="policyNumber" 
                type="text" 
                required 
                class="auth-input input-with-icon focus:ring-2 focus:ring-primary-500 transition-all duration-200" 
                placeholder="Enter your policy number (e.g., POL123456789)"
                :class="{'border-red-300 focus:ring-red-500 error': policyError}"
                @input="formatPolicyNumber"
              />
            </div>
            <p class="mt-2 text-xs text-gray-500">
              This can be found on your insurance documents or policy certificate
            </p>
            <p v-if="policyError" class="form-error">{{ policyError }}</p>
          </div>

          <div class="form-group">
            <label for="policy-type" class="form-label">Policy Type</label>
            <div class="relative">
              <svg xmlns="http://www.w3.org/2000/svg" class="input-icon h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4" />
              </svg>
              <select 
                id="policy-type" 
                v-model="policyType" 
                required 
                class="auth-input input-with-icon focus:ring-2 focus:ring-primary-500 transition-all duration-200 appearance-none"
                :class="{'border-red-300 focus:ring-red-500 error': policyTypeError}"
              >
                <option value="">Select your policy type</option>
                <option value="health">Health Insurance</option>
                <option value="auto">Auto Insurance</option>
                <option value="home">Home Insurance</option>
                <option value="life">Life Insurance</option>
                <option value="business">Business Insurance</option>
                <option value="travel">Travel Insurance</option>
                <option value="other">Other</option>
              </select>
              <div class="absolute inset-y-0 right-3 flex items-center pointer-events-none">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" />
                </svg>
              </div>
            </div>
            <p v-if="policyTypeError" class="form-error">{{ policyTypeError }}</p>
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
                {{ isLoading ? 'Setting up account...' : 'Complete setup' }}
              </span>
              <svg v-if="!isLoading" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M10.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L12.586 11H5a1 1 0 110-2h7.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd" />
              </svg>
            </span>
          </button>
        </form>

        <!-- Help section -->
        <div class="mt-8 p-4 bg-blue-50 rounded-lg border border-blue-200">
          <div class="flex items-start">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-blue-600 mr-3 mt-0.5 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
            <div>
              <h4 class="text-sm font-medium text-blue-900 mb-1">Need help finding your policy number?</h4>
              <ul class="text-xs text-blue-800 space-y-1">
                <li>• Check your insurance policy documents</li>
                <li>• Look at your insurance ID card</li>
                <li>• Check recent premium payment receipts</li>
                <li>• Contact your insurance provider</li>
              </ul>
            </div>
          </div>
        </div>

        <!-- Privacy notice -->
        <div class="mt-6 p-4 bg-gray-50 rounded-lg border border-gray-200">
          <div class="flex items-start">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400 mr-3 mt-0.5 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
            </svg>
            <div>
              <h4 class="text-sm font-medium text-gray-900 mb-1">Your information is secure</h4>
              <p class="text-xs text-gray-600">We use bank-level encryption to protect your policy information and never share it with third parties.</p>
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
      <div class="absolute inset-0 bg-cover bg-center" style="background-image: url('https://images.unsplash.com/photo-1450101499163-c8848c66ca85?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2340&q=80');">
        <div class="absolute inset-0 bg-gradient-to-br from-primary-900/90 via-primary-800/80 to-primary-700/70"></div>
      </div>
      
      <!-- Content overlay -->
      <div class="relative z-10 flex flex-col h-full p-12 justify-center">
        <div class="max-w-lg">
          <div class="inline-flex items-center px-4 py-2 rounded-full bg-white/10 backdrop-blur-md mb-6 border border-white/20">
            <span class="flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white mr-2" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M6.267 3.455a3.066 3.066 0 001.745-.723 3.066 3.066 0 013.976 0 3.066 3.066 0 001.745.723 3.066 3.066 0 012.812 2.812c.051.643.304 1.254.723 1.745a3.066 3.066 0 010 3.976 3.066 3.066 0 00-.723 1.745 3.066 3.066 0 01-2.812 2.812 3.066 3.066 0 00-1.745.723 3.066 3.066 0 01-3.976 0 3.066 3.066 0 00-1.745-.723 3.066 3.066 0 01-2.812-2.812 3.066 3.066 0 00-.723-1.745 3.066 3.066 0 010-3.976 3.066 3.066 0 00.723-1.745 3.066 3.066 0 012.812-2.812zm7.44 5.252a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
              </svg>
              <span class="text-white font-medium">Final step!</span>
            </span>
          </div>
          
          <h2 class="text-4xl font-bold text-white mb-6 leading-tight">
            You're almost <span class="text-accent-300">ready</span>
          </h2>
          
          <p class="text-white/90 text-xl leading-relaxed mb-8">
            Link your insurance policy to enable smart payment tracking and automated premium reminders.
          </p>
          
          <!-- Progress indicator -->
          <div class="mb-8">
            <div class="flex items-center justify-between mb-2">
              <span class="text-white/70 text-sm">Progress</span>
              <span class="text-white/70 text-sm">90%</span>
            </div>
            <div class="w-full bg-white/20 rounded-full h-2">
              <div class="bg-accent-400 h-2 rounded-full" style="width: 90%"></div>
            </div>
          </div>
          
          <!-- Benefits of linking policy -->
          <div class="space-y-4">
            <div class="flex items-start space-x-3">
              <div class="flex-shrink-0 h-8 w-8 rounded-full bg-accent-500/20 flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-accent-300" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                </svg>
              </div>
              <div>
                <h3 class="text-white font-medium">Automated Premium Tracking</h3>
                <p class="text-white/80 text-sm">Never miss a premium payment with smart reminders</p>
              </div>
            </div>
            
            <div class="flex items-start space-x-3">
              <div class="flex-shrink-0 h-8 w-8 rounded-full bg-success-500/20 flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-success-300" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                </svg>
              </div>
              <div>
                <h3 class="text-white font-medium">Policy Insights</h3>
                <p class="text-white/80 text-sm">Get detailed analytics on your insurance spending</p>
              </div>
            </div>
            
            <div class="flex items-start space-x-3">
              <div class="flex-shrink-0 h-8 w-8 rounded-full bg-primary-300/20 flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-primary-300" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                </svg>
              </div>
              <div>
                <h3 class="text-white font-medium">Renewal Alerts</h3>
                <p class="text-white/80 text-sm">Get notified before your policy expires</p>
              </div>
            </div>
          </div>
          
          <!-- Steps completed -->
          <div class="mt-8 pt-6 border-t border-white/20">
            <div class="flex items-center justify-between text-sm">
              <span class="text-white/70">Steps completed:</span>
              <span class="text-white font-medium">3 of 4</span>
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
const policyNumber = ref('');
const policyType = ref('');
const isLoading = ref(false);
const policyError = ref('');
const policyTypeError = ref('');

const formatPolicyNumber = (event) => {
  // Remove any non-alphanumeric characters and convert to uppercase
  const value = event.target.value.replace(/[^a-zA-Z0-9]/g, '').toUpperCase();
  policyNumber.value = value;
  policyError.value = '';
};

const validatePolicy = () => {
  let isValid = true;
  
  policyError.value = '';
  policyTypeError.value = '';
  
  if (!policyNumber.value) {
    policyError.value = 'Policy number is required';
    isValid = false;
  } else if (policyNumber.value.length < 6) {
    policyError.value = 'Policy number must be at least 6 characters';
    isValid = false;
  }
  
  if (!policyType.value) {
    policyTypeError.value = 'Please select your policy type';
    isValid = false;
  }
  
  return isValid;
};

const handleSubmit = async () => {
  if (!validatePolicy()) return;
  
  try {
    isLoading.value = true;
    
    // Simulate policy verification
    await new Promise(resolve => setTimeout(resolve, 2000));
    
    // Store policy information (in real app, this would be sent to backend)
    const policyData = {
      policyNumber: policyNumber.value,
      policyType: policyType.value,
      timestamp: new Date().toISOString()
    };
    
    sessionStorage.setItem('policy-data', JSON.stringify(policyData));
    
    // Redirect to dashboard
    router.push('/dashboard');
  } catch (error) {
    console.error('Policy verification failed:', error);
    policyError.value = 'Policy verification failed. Please try again.';
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

.form-group:nth-child(2) {
  animation-delay: 0.2s;
}

button[type="submit"] {
  animation: fadeIn 0.5s ease-out forwards;
  animation-delay: 0.3s;
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

/* Custom select dropdown styling */
select.auth-input {
  background-image: none;
}
</style>