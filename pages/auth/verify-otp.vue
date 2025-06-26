<template>
  <div class="min-h-screen flex">
    <!-- Left side - OTP verification form -->
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
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
            </svg>
          </div>
          <h2 class="text-3xl font-bold text-gray-900 mb-3">Enter verification code</h2>
          <p class="text-gray-600 mb-4">
            We've sent a 6-digit verification code to<br>
            <span class="font-medium text-gray-900">{{ phoneDisplay }}</span>
          </p>
        </div>

        <form @submit.prevent="handleSubmit" class="space-y-6">
          <div class="form-group">
            <label class="form-label text-center block">Enter verification code</label>
            <div class="flex justify-center space-x-3 mb-4">
              <input 
                v-for="(digit, index) in otpDigits" 
                :key="index"
                v-model="otpDigits[index]"
                @input="handleOtpInput(index, $event)"
                @keydown="handleOtpKeydown(index, $event)"
                :ref="el => otpInputs[index] = el"
                type="text" 
                maxlength="1"
                class="otp-input text-center text-lg font-semibold border-2 border-gray-300 rounded-lg focus:border-primary-500 focus:ring-2 focus:ring-primary-500 focus:outline-none transition-all duration-200"
                :class="{'border-red-300 focus:border-red-500 focus:ring-red-500 error': otpError}"
              />
            </div>
            <p v-if="otpError" class="text-sm text-red-500 text-center mb-4">{{ otpError }}</p>
            
            <div class="text-center">
              <p class="text-sm text-gray-600 mb-4">
                Didn't receive the code?
              </p>
              <button 
                type="button" 
                @click="resendOtp"
                :disabled="resendTimer > 0 || isResending"
                class="text-primary-600 text-sm font-medium hover:text-primary-700 disabled:text-gray-400 disabled:cursor-not-allowed transition-colors"
              >
                <span v-if="isResending" class="flex items-center justify-center">
                  <svg class="animate-spin h-4 w-4 mr-2" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                    <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                    <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                  </svg>
                  Resending...
                </span>
                <span v-else-if="resendTimer > 0">
                  Resend code in {{ resendTimer }}s
                </span>
                <span v-else>
                  Resend verification code
                </span>
              </button>
            </div>
          </div>

          <button 
            type="submit" 
            class="w-full btn-gradient py-3 rounded-xl text-lg font-medium relative overflow-hidden group transform transition hover:scale-[1.02] active:scale-[0.98]"
            :disabled="isLoading || !isOtpComplete"
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
                {{ isLoading ? 'Verifying...' : 'Verify code' }}
              </span>
              <svg v-if="!isLoading" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M10.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L12.586 11H5a1 1 0 110-2h7.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd" />
              </svg>
            </span>
          </button>
        </form>

        <!-- Back button -->
        <div class="mt-6 text-center">
          <button 
            @click="goBack"
            class="text-sm text-gray-500 hover:text-gray-700 font-medium transition-colors"
          >
            ← Back to phone number
          </button>
        </div>

        <!-- Security Notice -->
        <div class="mt-8 p-4 bg-gray-50 rounded-lg border border-gray-200">
          <div class="flex items-start">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400 mr-3 mt-0.5 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
            </svg>
            <div>
              <h4 class="text-sm font-medium text-gray-900 mb-1">Security tip</h4>
              <p class="text-xs text-gray-600">This code will expire in 5 minutes. Never share your verification code with anyone.</p>
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
      <div class="absolute inset-0 bg-cover bg-center" style="background-image: url('https://images.unsplash.com/photo-1563013544-824ae1b704d3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2340&q=80');">
        <div class="absolute inset-0 bg-gradient-to-br from-primary-900/90 via-primary-800/80 to-primary-700/70"></div>
      </div>
      
      <!-- Content overlay -->
      <div class="relative z-10 flex flex-col h-full p-12 justify-center">
        <div class="max-w-lg">
          <div class="inline-flex items-center px-4 py-2 rounded-full bg-white/10 backdrop-blur-md mb-6 border border-white/20">
            <span class="flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white mr-2" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" clip-rule="evenodd" />
              </svg>
              <span class="text-white font-medium">Almost there!</span>
            </span>
          </div>
          
          <h2 class="text-4xl font-bold text-white mb-6 leading-tight">
            Just one step <span class="text-accent-300">away</span>
          </h2>
          
          <p class="text-white/90 text-xl leading-relaxed mb-8">
            Enter the 6-digit code we sent to your phone to complete the verification process.
          </p>
          
          <!-- Progress indicator -->
          <div class="mb-8">
            <div class="flex items-center justify-between mb-2">
              <span class="text-white/70 text-sm">Progress</span>
              <span class="text-white/70 text-sm">66%</span>
            </div>
            <div class="w-full bg-white/20 rounded-full h-2">
              <div class="bg-accent-400 h-2 rounded-full" style="width: 66%"></div>
            </div>
          </div>
          
          <!-- Steps remaining -->
          <div class="space-y-3">
            <div class="flex items-center space-x-3">
              <div class="flex-shrink-0 h-6 w-6 rounded-full bg-success-500 flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-3 w-3 text-white" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                </svg>
              </div>
              <span class="text-white">Social login completed</span>
            </div>
            <div class="flex items-center space-x-3">
              <div class="flex-shrink-0 h-6 w-6 rounded-full bg-success-500 flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-3 w-3 text-white" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                </svg>
              </div>
              <span class="text-white">Phone number added</span>
            </div>
            <div class="flex items-center space-x-3">
              <div class="flex-shrink-0 h-6 w-6 rounded-full bg-accent-400 flex items-center justify-center animate-pulse">
                <span class="text-white text-xs font-bold">3</span>
              </div>
              <span class="text-white font-medium">Verify phone number</span>
            </div>
            <div class="flex items-center space-x-3">
              <div class="flex-shrink-0 h-6 w-6 rounded-full bg-white/20 flex items-center justify-center">
                <span class="text-white/70 text-xs">4</span>
              </div>
              <span class="text-white/70">Add policy number</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue';
import { useRouter } from 'vue-router';

definePageMeta({
  layout: false,
});

const router = useRouter();
const otpDigits = ref(['', '', '', '', '', '']);
const otpInputs = ref([]);
const isLoading = ref(false);
const otpError = ref('');
const isResending = ref(false);
const resendTimer = ref(60);
const phoneData = ref(null);

let resendInterval = null;

const phoneDisplay = computed(() => {
  if (!phoneData.value) return '';
  return `${phoneData.value.countryCode} ${phoneData.value.mobile}`;
});

const isOtpComplete = computed(() => {
  return otpDigits.value.every(digit => digit !== '');
});

onMounted(() => {
  // Get phone data from session storage
  const storedData = sessionStorage.getItem('phone-verification');
  if (!storedData) {
    router.push('/auth/phone-verification');
    return;
  }
  
  phoneData.value = JSON.parse(storedData);
  
  // Start resend timer
  startResendTimer();
  
  // Focus first input
  setTimeout(() => {
    otpInputs.value[0]?.focus();
  }, 100);
});

onUnmounted(() => {
  if (resendInterval) {
    clearInterval(resendInterval);
  }
});

const startResendTimer = () => {
  resendTimer.value = 60;
  resendInterval = setInterval(() => {
    resendTimer.value--;
    if (resendTimer.value <= 0) {
      clearInterval(resendInterval);
    }
  }, 1000);
};

const handleOtpInput = (index, event) => {
  const value = event.target.value;
  if (!/^\d*$/.test(value)) {
    event.target.value = otpDigits.value[index];
    return;
  }
  
  otpDigits.value[index] = value;
  
  if (value && index < 5) {
    otpInputs.value[index + 1]?.focus();
  }
  
  otpError.value = '';
};

const handleOtpKeydown = (index, event) => {
  if (event.key === 'Backspace' && !otpDigits.value[index] && index > 0) {
    otpInputs.value[index - 1]?.focus();
  }
};

const validateOtp = () => {
  const otp = otpDigits.value.join('');
  if (otp.length !== 6) {
    otpError.value = 'Please enter the complete 6-digit code';
    return false;
  }
  
  // For demo purposes, accept any 6-digit code
  // In real app, verify with backend
  if (otp !== '123456' && otp !== '000000') {
    // Auto-accept for demo, but you can uncomment below for testing
    // otpError.value = 'Invalid verification code. Please try again.';
    // return false;
  }
  
  return true;
};

const resendOtp = async () => {
  try {
    isResending.value = true;
    
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    // Clear OTP inputs
    otpDigits.value = ['', '', '', '', '', ''];
    otpInputs.value[0]?.focus();
    
    // Start timer
    startResendTimer();
    
  } catch (error) {
    console.error('Failed to resend OTP:', error);
  } finally {
    isResending.value = false;
  }
};

const handleSubmit = async () => {
  if (!validateOtp()) return;
  
  try {
    isLoading.value = true;
    
    // Simulate OTP verification
    await new Promise(resolve => setTimeout(resolve, 1500));
    
    // Clear phone verification data
    sessionStorage.removeItem('phone-verification');
    
    // Redirect to policy number page
    router.push('/auth/policy-number');
  } catch (error) {
    console.error('OTP verification failed:', error);
    otpError.value = 'Verification failed. Please try again.';
  } finally {
    isLoading.value = false;
  }
};

const goBack = () => {
  router.push('/auth/phone-verification');
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