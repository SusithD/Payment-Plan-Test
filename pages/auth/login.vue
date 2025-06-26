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
        <div class="mb-10 text-center">
          <h2 class="text-3xl font-bold text-gray-900 mb-3">Welcome back</h2>
          <p class="text-gray-600 text-lg">
            Sign in with your preferred account to access your payment dashboard
          </p>
        </div>

        <!-- Social Login Options -->
        <div class="space-y-4">
          <!-- Google Login -->
          <button 
            @click="handleGoogleLogin" 
            class="w-full flex items-center justify-center px-6 py-4 border-2 border-gray-200 rounded-xl text-gray-700 bg-white hover:bg-gray-50 hover:border-gray-300 focus:outline-none focus:ring-4 focus:ring-blue-500/20 transition-all duration-200 transform hover:scale-[1.02] active:scale-[0.98] shadow-sm hover:shadow-md"
            :disabled="isLoading"
          >
            <div class="flex items-center">
              <svg class="w-6 h-6 mr-4" viewBox="0 0 24 24">
                <path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/>
                <path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/>
                <path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z"/>
                <path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z"/>
              </svg>
              <div class="text-left">
                <div class="font-semibold text-base">Continue with Google</div>
                <div class="text-sm text-gray-500">Use your Google account to sign in securely</div>
              </div>
            </div>
            <svg v-if="isLoading && loadingProvider === 'google'" class="animate-spin ml-3 h-5 w-5 text-gray-500" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
              <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
              <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
            </svg>
          </button>

          <!-- Apple Login -->
          <button 
            @click="handleAppleLogin" 
            class="w-full flex items-center justify-center px-6 py-4 border-2 border-gray-900 bg-gray-900 rounded-xl text-white hover:bg-gray-800 hover:border-gray-800 focus:outline-none focus:ring-4 focus:ring-gray-500/20 transition-all duration-200 transform hover:scale-[1.02] active:scale-[0.98] shadow-sm hover:shadow-md"
            :disabled="isLoading"
          >
            <div class="flex items-center">
              <svg class="w-6 h-6 mr-4 text-white" viewBox="0 0 24 24" fill="currentColor">
                <path d="M12.152 6.896c-.948 0-2.415-1.078-3.96-1.04-2.04.027-3.91 1.183-4.961 3.014-2.117 3.675-.546 9.103 1.519 12.09 1.013 1.454 2.208 3.09 3.792 3.039 1.52-.065 2.09-.987 3.935-.987 1.831 0 2.35.987 3.96.948 1.637-.026 2.676-1.48 3.676-2.948 1.156-1.688 1.636-3.325 1.662-3.415-.039-.013-3.182-1.221-3.22-4.857-.026-3.04 2.48-4.494 2.597-4.559-1.429-2.09-3.623-2.324-4.39-2.376-2-.156-3.675 1.09-4.61 1.09zM15.53 3.83c.843-1.012 1.4-2.427 1.245-3.83-1.207.052-2.662.805-3.532 1.818-.78.896-1.454 2.338-1.273 3.714 1.338.104 2.715-.688 3.559-1.701"/>
              </svg>
              <div class="text-left">
                <div class="font-semibold text-base">Continue with Apple</div>
                <div class="text-sm text-gray-300">Sign in using your Apple ID with Touch ID or Face ID</div>
              </div>
            </div>
            <svg v-if="isLoading && loadingProvider === 'apple'" class="animate-spin ml-3 h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
              <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
              <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
            </svg>
          </button>
        </div>

        <!-- Benefits Section -->
        <div class="mt-8 p-6 bg-gradient-to-r from-blue-50 to-indigo-50 rounded-xl border border-blue-100">
          <h3 class="font-semibold text-gray-900 mb-3 flex items-center">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-blue-600 mr-2" viewBox="0 0 20 20" fill="currentColor">
              <path fill-rule="evenodd" d="M2.166 4.999A11.954 11.954 0 0010 1.944 11.954 11.954 0 0017.834 5c.11.65.166 1.32.166 2.001 0 5.225-3.34 9.67-8 11.317C5.34 16.67 2 12.225 2 7c0-.682.057-1.35.166-2.001zm11.541 3.708a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
            </svg>
            Why use social login?
          </h3>
          <ul class="space-y-2 text-sm text-gray-600">
            <li class="flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-green-500 mr-2 flex-shrink-0" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
              </svg>
              Enhanced security with two-factor authentication
            </li>
            <li class="flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-green-500 mr-2 flex-shrink-0" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
              </svg>
              Quick and seamless access to your account
            </li>
            <li class="flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-green-500 mr-2 flex-shrink-0" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
              </svg>
              No need to remember another password
            </li>
          </ul>
        </div>

        <!-- Security Notice -->
        <div class="mt-6 p-4 bg-gray-50 rounded-lg border border-gray-200">
          <div class="flex items-start">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400 mr-3 mt-0.5 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
            </svg>
            <div>
              <h4 class="text-sm font-medium text-gray-900 mb-1">Your data is protected</h4>
              <p class="text-xs text-gray-600">We use industry-standard encryption and never store your login credentials. Your financial information is secured with bank-level security.</p>
            </div>
          </div>
        </div>

        <div class="text-center mt-8">
          <p class="text-sm text-gray-600">
            Don't have an account?
            <NuxtLink 
              to="/auth/signup" 
              class="font-medium text-primary-600 hover:text-primary-500 transition-colors"
            >
              Create one now
            </NuxtLink>
          </p>
          <p class="text-xs text-gray-500 mt-4">
            By signing in, you agree to our 
            <a href="#" class="text-primary-600 hover:text-primary-500">Terms of Service</a> and 
            <a href="#" class="text-primary-600 hover:text-primary-500">Privacy Policy</a>
          </p>
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
const isLoading = ref(false);
const loadingProvider = ref('');

const handleGoogleLogin = async () => {
  try {
    isLoading.value = true;
    loadingProvider.value = 'google';
    
    // Simulate OAuth flow
    await new Promise(resolve => setTimeout(resolve, 2000));
    
    // In a real app, you would integrate with Google OAuth
    // Example: window.location.href = 'https://accounts.google.com/oauth/authorize?...'
    
    // Redirect to phone verification instead of dashboard
    router.push('/auth/phone-verification');
  } catch (error) {
    console.error('Google login failed:', error);
    // Handle error (show toast notification, etc.)
  } finally {
    isLoading.value = false;
    loadingProvider.value = '';
  }
};

const handleAppleLogin = async () => {
  try {
    isLoading.value = true;
    loadingProvider.value = 'apple';
    
    // Simulate OAuth flow
    await new Promise(resolve => setTimeout(resolve, 2000));
    
    // In a real app, you would integrate with Apple Sign In
    // Example: Use Apple's Sign In JS SDK
    
    // Redirect to phone verification instead of dashboard
    router.push('/auth/phone-verification');
  } catch (error) {
    console.error('Apple login failed:', error);
    // Handle error (show toast notification, etc.)
  } finally {
    isLoading.value = false;
    loadingProvider.value = '';
  }
};
</script>

<style scoped>
.gradient-text {
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
  background-image: linear-gradient(to right, var(--tw-gradient-stops));
  --tw-gradient-from: #2C4880;
  --tw-gradient-to: #4476b0;
  --tw-gradient-stops: var(--tw-gradient-from), var(--tw-gradient-to);
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

.space-y-4 > * {
  animation: fadeIn 0.5s ease-out forwards;
  opacity: 0;
}

.space-y-4 > *:nth-child(1) {
  animation-delay: 0.1s;
}

.space-y-4 > *:nth-child(2) {
  animation-delay: 0.2s;
}
</style>