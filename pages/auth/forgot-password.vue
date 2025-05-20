<template>
  <div class="min-h-screen flex">
    <!-- Left side - Forgot Password form -->
    <div class="w-full lg:w-1/2 bg-white flex flex-col justify-center px-6 sm:px-10 lg:px-16 xl:px-24 relative z-10">
      <div class="absolute top-8 left-8">
        <NuxtLink to="/" class="flex items-center">
          <span class="text-2xl font-bold gradient-text">PaymentPlan</span>
        </NuxtLink>
      </div>
      
      <div class="max-w-md mx-auto w-full py-20 lg:py-12">
        <div class="mb-10 text-center">
          <div class="inline-flex items-center justify-center w-16 h-16 rounded-full bg-primary-100 text-primary-600 mb-4">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 7a2 2 0 012 2m4 0a6 6 0 01-7.743 5.743L11 17H9v2H7v2H4a1 1 0 01-1-1v-2.586a1 1 0 01.293-.707l5.964-5.964A6 6 0 1121 9z" />
            </svg>
          </div>
          <h1 class="text-3xl font-bold text-gray-900">Forgot your password?</h1>
          <p class="mt-2 text-gray-600">
            No worries, we'll send you a reset link to your email address.
          </p>
        </div>
        
        <form class="mt-8 space-y-6" @submit.prevent="handleForgotPassword">
          <div class="form-group">
            <label for="email" class="form-label inline-block mb-2 font-medium text-gray-700">Email address</label>
            <div class="relative">
              <span class="absolute inset-y-0 left-3 flex items-center text-gray-400">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                  <path d="M2.003 5.884L10 9.882l7.997-3.998A2 2 0 0016 4H4a2 2 0 00-1.997 1.884z" />
                  <path d="M18 8.118l-8 4-8-4V14a2 2 0 002 2h12a2 2 0 002-2V8.118z" />
                </svg>
              </span>
              <input 
                id="email" 
                v-model="email" 
                name="email" 
                type="email" 
                autocomplete="email" 
                required 
                class="auth-input pl-10 focus:ring-2 focus:ring-primary-500 transition-all duration-200"
                placeholder="your.email@example.com" 
              />
            </div>
          </div>

          <div>
            <button 
              type="submit" 
              class="w-full btn-gradient py-4 rounded-xl text-lg font-medium relative overflow-hidden group transform transition hover:scale-[1.02] active:scale-[0.98]"
              :disabled="isSubmitting"
            >
              <div class="absolute top-0 left-0 w-full h-full bg-white opacity-0 group-hover:opacity-10 transition-opacity"></div>
              <span class="relative flex items-center justify-center">
                <span v-if="isSubmitting" class="mr-2">
                  <svg class="animate-spin h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                    <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                    <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                  </svg>
                </span>
                <span>{{ isSubmitting ? 'Sending reset link...' : 'Send reset link' }}</span>
              </span>
            </button>
          </div>
          
          <div class="text-center">
            <p class="text-sm text-gray-600">
              Remember your password?
              <NuxtLink 
                to="/auth/login" 
                class="font-medium text-primary-600 hover:text-primary-500 transition-colors"
              >
                Back to login
              </NuxtLink>
            </p>
          </div>
        </form>

        <!-- Success message -->
        <div v-if="submitted" class="mt-8 p-4 rounded-xl bg-success-50 text-success-700 border border-success-200 fade-in">
          <div class="flex">
            <div class="shrink-0">
              <svg class="h-5 w-5 text-success-400" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
              </svg>
            </div>
            <div class="ml-3">
              <p class="text-sm font-medium">
                Reset link sent! Check your email for instructions.
              </p>
            </div>
          </div>
        </div>
      </div>
      
      <div class="absolute bottom-6 left-0 right-0 text-center text-xs text-gray-500 mt-8">
        <p>© 2025 PaymentPlan. All rights reserved.</p>
      </div>
    </div>
    
    <!-- Right side - Image section with help information -->
    <div class="hidden lg:block lg:w-1/2 relative overflow-hidden">
      <!-- Background Image with gradient overlay -->
      <div class="absolute inset-0 bg-cover bg-center" style="background-image: url('https://images.unsplash.com/photo-1518458028785-8fbcd101ebb9?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2070&q=80');">
        <div class="absolute inset-0 bg-gradient-to-br from-primary-900/90 via-primary-800/75 to-primary-700/60"></div>
      </div>
      
      <!-- Content overlay with modern design -->
      <div class="relative z-10 flex flex-col h-full p-12 justify-center">
        <div class="space-y-8 max-w-lg">
          <div class="inline-flex items-center px-4 py-2 rounded-full bg-white/10 backdrop-blur-md mb-2 border border-white/20">
            <span class="flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
              <span class="text-white font-medium">Password Recovery Help</span>
            </span>
          </div>
          
          <h2 class="text-4xl font-bold text-white mb-6 leading-tight">Need help with your <span class="text-accent-300">account access</span>?</h2>
          
          <div class="space-y-6">
            <!-- Help Card 1 -->
            <div class="bg-white/10 backdrop-blur-md rounded-xl p-6 border border-white/20">
              <div class="flex items-start">
                <div class="flex-shrink-0 mr-4">
                  <div class="h-10 w-10 rounded-full bg-accent-500/20 flex items-center justify-center">
                    <span class="text-accent-300 font-bold text-lg">1</span>
                  </div>
                </div>
                <div>
                  <h3 class="text-white text-lg font-semibold mb-2">Check Your Email</h3>
                  <p class="text-white/80">After submitting, check your email inbox for a password reset link. Be sure to check your spam folder if you don't see it.</p>
                </div>
              </div>
            </div>
            
            <!-- Help Card 2 -->
            <div class="bg-white/10 backdrop-blur-md rounded-xl p-6 border border-white/20">
              <div class="flex items-start">
                <div class="flex-shrink-0 mr-4">
                  <div class="h-10 w-10 rounded-full bg-accent-500/20 flex items-center justify-center">
                    <span class="text-accent-300 font-bold text-lg">2</span>
                  </div>
                </div>
                <div>
                  <h3 class="text-white text-lg font-semibold mb-2">Click the Reset Link</h3>
                  <p class="text-white/80">The link in your email will direct you to a secure page where you can create a new password for your account.</p>
                </div>
              </div>
            </div>
            
            <!-- Help Card 3 -->
            <div class="bg-white/10 backdrop-blur-md rounded-xl p-6 border border-white/20">
              <div class="flex items-start">
                <div class="flex-shrink-0 mr-4">
                  <div class="h-10 w-10 rounded-full bg-accent-500/20 flex items-center justify-center">
                    <span class="text-accent-300 font-bold text-lg">3</span>
                  </div>
                </div>
                <div>
                  <h3 class="text-white text-lg font-semibold mb-2">Create New Password</h3>
                  <p class="text-white/80">Choose a strong, unique password with a mix of letters, numbers, and special characters for better security.</p>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Contact support -->
          <div class="mt-8 bg-white/10 backdrop-blur-md rounded-xl p-6 border border-white/20">
            <div class="flex items-center">
              <div class="mr-4">
                <div class="h-12 w-12 rounded-full bg-primary-300/20 flex items-center justify-center">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-300" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18 9v3m0 0v3m0-3h3m-3 0h-3m-2-5a4 4 0 11-8 0 4 4 0 018 0zM3 20a6 6 0 0112 0v1H3v-1z" />
                  </svg>
                </div>
              </div>
              <div>
                <h3 class="text-white text-lg font-semibold mb-1">Still need help?</h3>
                <p class="text-white/80">Contact our support team at <span class="text-accent-300">support@paymentplan.com</span></p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

definePageMeta({
  layout: false,
});

const email = ref('');
const isSubmitting = ref(false);
const submitted = ref(false);

const handleForgotPassword = () => {
  isSubmitting.value = true;
  
  // Simulate API call
  setTimeout(() => {
    isSubmitting.value = false;
    submitted.value = true;
  }, 1500);
};
</script>

<style scoped>
.auth-input {
  width: 100%;
  padding: 0.75rem 1rem;
  border-radius: 0.5rem;
  border: 1px solid #d1d5db;
  transition-property: all;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 200ms;
}

.btn-gradient {
  background-image: linear-gradient(to right, var(--tw-gradient-stops));
  --tw-gradient-from: #2C4880;
  --tw-gradient-to: #4476b0;
  --tw-gradient-stops: var(--tw-gradient-from), var(--tw-gradient-to);
  color: white;
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

.form-label {
  display: block;
  font-size: 0.875rem;
  font-weight: 500;
  color: #374151;
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

.form-group {
  animation: fadeIn 0.5s ease-out forwards;
}

.fade-in {
  animation: fadeIn 0.5s ease-out forwards;
}
</style>