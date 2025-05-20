<template>
  <div class="min-h-screen flex">
    <!-- Left side - Login form -->
    <div class="w-full lg:w-1/2 bg-white flex flex-col justify-center px-6 sm:px-10 lg:px-16 xl:px-24 relative z-10">
      <div class="absolute top-8 left-8">
        <NuxtLink to="/" class="flex items-center">
          <span class="text-2xl font-bold gradient-text">PaymentPlan</span>
        </NuxtLink>
      </div>
      
      <div class="max-w-md mx-auto w-full py-20 lg:py-12">
        <div class="mb-10">
          <h2 class="text-3xl font-bold text-gray-900 mb-3">Welcome back</h2>
          <p class="text-gray-600">
            We're happy to see you again. Access your account below.
          </p>
        </div>
        
        <form @submit.prevent="handleLogin" class="space-y-6">
          <div class="space-y-5">
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
                  type="email" 
                  autocomplete="email" 
                  required 
                  class="auth-input pl-10 focus:ring-2 focus:ring-primary-500 transition-all duration-200" 
                  placeholder="your.email@example.com"
                  :class="{'border-red-300 focus:ring-red-500': emailError}"
                />
              </div>
              <p v-if="emailError" class="mt-1 text-sm text-red-500">{{ emailError }}</p>
            </div>
            
            <div class="form-group">
              <div class="flex items-center justify-between mb-2">
                <label for="password" class="form-label font-medium text-gray-700">Password</label>
                <NuxtLink 
                  to="/auth/forgot-password" 
                  class="text-sm font-medium text-primary-600 hover:text-primary-500 transition-colors"
                >
                  Forgot password?
                </NuxtLink>
              </div>
              <div class="relative">
                <span class="absolute inset-y-0 left-3 flex items-center text-gray-400">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M5 9V7a5 5 0 0110 0v2a2 2 0 012 2v5a2 2 0 01-2 2H5a2 2 0 01-2-2v-5a2 2 0 012-2zm8-2v2H7V7a3 3 0 016 0z" clip-rule="evenodd" />
                  </svg>
                </span>
                <input 
                  id="password" 
                  v-model="password" 
                  :type="showPassword ? 'text' : 'password'" 
                  autocomplete="current-password" 
                  required 
                  class="auth-input pl-10 pr-10 focus:ring-2 focus:ring-primary-500 transition-all duration-200" 
                  placeholder="••••••••"
                  :class="{'border-red-300 focus:ring-red-500': passwordError}"
                />
                <button 
                  type="button" 
                  class="absolute inset-y-0 right-3 flex items-center text-gray-400 hover:text-gray-600"
                  @click="togglePassword"
                >
                  <svg v-if="!showPassword" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path d="M10 12a2 2 0 100-4 2 2 0 000 4z" />
                    <path fill-rule="evenodd" d="M.458 10C1.732 5.943 5.522 3 10 3s8.268 2.943 9.542 7c-1.274 4.057-5.064 7-9.542 7S1.732 14.057.458 10zM14 10a4 4 0 11-8 0 4 4 0 018 0z" clip-rule="evenodd" />
                  </svg>
                  <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M3.707 2.293a1 1 0 00-1.414 1.414l14 14a1 1 0 001.414-1.414l-1.473-1.473A10.014 10.014 0 0019.542 10C18.268 5.943 14.478 3 10 3a9.958 9.958 0 00-4.512 1.074l-1.78-1.781zm4.261 4.26l1.514 1.515a2.003 2.003 0 012.45 2.45l1.514 1.514a4 4 0 00-5.478-5.478z" clip-rule="evenodd" />
                    <path d="M12.454 16.697L9.75 13.992a4 4 0 01-3.742-3.741L2.335 6.578A9.98 9.98 0 00.458 10c1.274 4.057 5.065 7 9.542 7 .847 0 1.669-.105 2.454-.303z" />
                  </svg>
                </button>
              </div>
              <p v-if="passwordError" class="mt-1 text-sm text-red-500">{{ passwordError }}</p>
            </div>
          </div>

          <div class="flex items-center">
            <input 
              id="remember-me" 
              v-model="rememberMe"
              type="checkbox" 
              class="h-4 w-4 text-primary-600 border-gray-300 rounded focus:ring-primary-500" 
            />
            <label for="remember-me" class="ml-2 block text-sm text-gray-700">
              Keep me signed in
            </label>
          </div>

          <button 
            type="submit" 
            class="w-full btn-gradient py-4 rounded-xl text-lg font-medium relative overflow-hidden group transform transition hover:scale-[1.02] active:scale-[0.98]"
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
              <span>{{ isLoading ? 'Signing in...' : 'Sign in to account' }}</span>
            </span>
          </button>

          <div class="text-center">
            <p class="text-sm text-gray-600">
              Don't have an account?
              <NuxtLink 
                to="/auth/signup" 
                class="font-medium text-primary-600 hover:text-primary-500 transition-colors"
              >
                Create one now
              </NuxtLink>
            </p>
          </div>
        </form>

        <div class="mt-10">
          <div class="relative">
            <div class="absolute inset-0 flex items-center">
              <div class="w-full border-t border-gray-200"></div>
            </div>
            <div class="relative flex justify-center text-sm">
              <span class="px-4 bg-white text-gray-500">Or continue with</span>
            </div>
          </div>

          <div class="mt-6 grid grid-cols-2 gap-3">
            <button class="social-btn">
              <img src="https://www.google.com/favicon.ico" alt="Google" class="w-5 h-5" />
              <span>Google</span>
            </button>
            <button class="social-btn">
              <img src="https://www.apple.com/favicon.ico" alt="Apple" class="w-5 h-5" />
              <span>Apple</span>
            </button>
          </div>
        </div>
      </div>
      
      <div class="absolute bottom-6 left-0 right-0 text-center text-xs text-gray-500 mt-8">
        <p>© 2025 PaymentPlan. All rights reserved.</p>
      </div>
    </div>
    
    <!-- Right side - Image section -->
    <div class="hidden lg:block lg:w-1/2 relative overflow-hidden">
      <!-- Background Image with gradient overlay -->
      <div class="absolute inset-0 bg-cover bg-center" style="background-image: url('https://images.unsplash.com/photo-1579621970588-a35d0e7ab9b6?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2070&q=80');">
        <div class="absolute inset-0 bg-gradient-to-br from-primary-900/90 via-primary-800/75 to-primary-700/60"></div>
      </div>
      
      <!-- Content overlay with modern design -->
      <div class="relative z-10 flex flex-col h-full p-12 justify-between">
        <!-- Top Section -->
        <div class="mt-16">
          <div class="inline-flex items-center px-4 py-2 rounded-full bg-white/10 backdrop-blur-md mb-6 border border-white/20">
            <span class="flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white mr-2" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M6.267 3.455a3.066 3.066 0 001.745-.723 3.066 3.066 0 013.976 0 3.066 3.066 0 001.745.723 3.066 3.066 0 012.812 2.812c.051.643.304 1.254.723 1.745a3.066 3.066 0 010 3.976 3.066 3.066 0 00-.723 1.745 3.066 3.066 0 01-2.812 2.812 3.066 3.066 0 00-1.745.723 3.066 3.066 0 01-3.976 0 3.066 3.066 0 00-1.745-.723 3.066 3.066 0 01-2.812-2.812 3.066 3.066 0 00-.723-1.745 3.066 3.066 0 010-3.976 3.066 3.066 0 00.723-1.745 3.066 3.066 0 012.812-2.812zm7.44 5.252a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
              </svg>
              <span class="text-white font-medium">Trusted by 20,000+ users</span>
            </span>
          </div>
          <h2 class="text-4xl font-bold text-white mb-6 max-w-md leading-tight">Manage your payments <span class="text-accent-300">smarter</span> with PaymentPlan</h2>
          <p class="text-white/90 text-xl max-w-lg leading-relaxed mb-8">Access your dashboard to track, plan and manage all your payments in one secure place.</p>
        </div>
        
        <!-- Feature highlight section -->
        <div class="space-y-6">
          <!-- Stats cards -->
          <div class="grid grid-cols-2 gap-6">
            <!-- Analytics Card -->
            <div class="bg-white/10 backdrop-blur-md rounded-xl p-6 border border-white/20 transform transition-all duration-300 hover:translate-y-[-5px]">
              <div class="flex flex-col items-center text-center">
                <div class="h-16 w-16 rounded-2xl bg-accent-500/20 flex items-center justify-center mb-4">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 text-accent-300" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
                  </svg>
                </div>
                <h3 class="text-white text-lg font-semibold mb-2">Advanced Analytics</h3>
                <p class="text-white/80">Get detailed insights on your spending patterns</p>
              </div>
            </div>

            <!-- Security Card -->
            <div class="bg-white/10 backdrop-blur-md rounded-xl p-6 border border-white/20 transform transition-all duration-300 hover:translate-y-[-5px]">
              <div class="flex flex-col items-center text-center">
                <div class="h-16 w-16 rounded-2xl bg-success-500/20 flex items-center justify-center mb-4">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 text-success-300" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
                  </svg>
                </div>
                <h3 class="text-white text-lg font-semibold mb-2">Bank-Level Security</h3>
                <p class="text-white/80">Your financial data is protected with end-to-end encryption</p>
              </div>
            </div>
          </div>

          <!-- Feature Banner -->
          <div class="bg-white/10 backdrop-blur-md rounded-xl p-6 border border-white/20 relative overflow-hidden">
            <div class="flex items-start">
              <div class="mr-4">
                <div class="h-12 w-12 rounded-xl bg-primary-300/20 flex items-center justify-center">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-300" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                </div>
              </div>
              <div>
                <h3 class="text-white text-lg font-semibold mb-2">Never Miss a Payment</h3>
                <p class="text-white/80">Smart reminders and scheduling help you stay on top of all your payments.</p>
                <div class="mt-4">
                  <span class="inline-flex items-center px-3 py-1 rounded-full bg-accent-500/20 text-accent-300 text-sm font-medium">
                    <span class="mr-1">●</span> Premium Feature
                  </span>
                </div>
              </div>
            </div>
            
            <!-- Decorative elements -->
            <div class="absolute -bottom-6 -right-6 h-24 w-24 rounded-full bg-gradient-to-r from-accent-500/20 to-primary-500/10 blur-xl"></div>
            <div class="absolute -top-10 -right-10 h-16 w-16 rounded-full bg-gradient-to-r from-success-500/20 to-accent-500/10 blur-lg"></div>
          </div>
        </div>
        
        <!-- Bottom section with stats -->
        <div class="mt-12">
          <div class="flex items-center justify-between mb-6">
            <h3 class="text-white font-medium">Trusted by financial experts</h3>
            <div class="flex space-x-2">
              <span class="flex h-2.5 w-2.5 rounded-full bg-accent-400"></span>
              <span class="flex h-2.5 w-2.5 rounded-full bg-white/30"></span>
              <span class="flex h-2.5 w-2.5 rounded-full bg-white/30"></span>
            </div>
          </div>
          <div class="grid grid-cols-3 gap-6">
            <div class="text-center">
              <div class="text-3xl font-bold text-white">98%</div>
              <div class="text-white/70 text-sm mt-1">Customer satisfaction</div>
            </div>
            <div class="text-center">
              <div class="text-3xl font-bold text-white">$2.5M</div>
              <div class="text-white/70 text-sm mt-1">Late fees saved</div>
            </div>
            <div class="text-center">
              <div class="text-3xl font-bold text-white">15min</div>
              <div class="text-white/70 text-sm mt-1">Setup time</div>
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
const email = ref('');
const password = ref('');
const rememberMe = ref(false);
const showPassword = ref(false);
const isLoading = ref(false);
const emailError = ref('');
const passwordError = ref('');

const togglePassword = () => {
  showPassword.value = !showPassword.value;
};

const validateForm = () => {
  let isValid = true;
  
  // Reset errors
  emailError.value = '';
  passwordError.value = '';
  
  // Email validation
  if (!email.value) {
    emailError.value = 'Email is required';
    isValid = false;
  } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email.value)) {
    emailError.value = 'Please enter a valid email address';
    isValid = false;
  }
  
  // Password validation
  if (!password.value) {
    passwordError.value = 'Password is required';
    isValid = false;
  } else if (password.value.length < 6) {
    passwordError.value = 'Password must be at least 6 characters';
    isValid = false;
  }
  
  return isValid;
};

const handleLogin = async () => {
  if (!validateForm()) return;
  
  try {
    isLoading.value = true;
    
    // Simulate API call with timeout
    await new Promise(resolve => setTimeout(resolve, 1500));
    
    // Login successful
    router.push('/dashboard');
  } catch (error) {
    console.error('Login failed:', error);
  } finally {
    isLoading.value = false;
  }
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

.social-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.75rem 1rem;
  border: 1px solid #d1d5db;
  border-radius: 0.5rem;
  color: #4b5563;
  background-color: white;
  font-weight: 500;
  transition-property: all;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 200ms;
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
}

.social-btn:hover {
  background-color: #f9fafb;
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
}

.social-btn:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(44, 72, 128, 0.2);
}

.social-btn span {
  margin-left: 0.75rem;
}

.form-label {
  display: block;
  font-size: 0.875rem;
  font-weight: 500;
  color: #374151;
}

/* Animation for page elements */
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
</style>