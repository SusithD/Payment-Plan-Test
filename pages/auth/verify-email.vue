<template>
  <div class="w-full max-w-md p-8 space-y-8 bg-white rounded-xl shadow-card">
    <div class="text-center">
      <div class="inline-flex items-center justify-center w-16 h-16 rounded-full bg-primary-100 text-primary-600 mb-4">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
        </svg>
      </div>
      <h1 class="text-3xl font-bold text-gray-900">Verify your email</h1>
      <p class="mt-2 text-gray-600">
        We've sent a verification code to your email address. 
        Please enter the code below to verify your account.
      </p>
    </div>
    
    <form class="mt-8 space-y-6" @submit.prevent="handleVerification">
      <div>
        <label for="verification-code" class="form-label">Verification code</label>
        <input 
          id="verification-code" 
          v-model="verificationCode" 
          name="verification-code" 
          type="text" 
          required 
          class="form-input text-center text-xl tracking-widest" 
          placeholder="Enter code"
        />
      </div>

      <div>
        <button 
          type="submit" 
          class="w-full btn-primary py-3"
        >
          Verify email
        </button>
      </div>
      
      <div class="text-center">
        <p class="text-gray-600 text-sm">
          Didn't receive the code?
          <button @click="resendCode" class="font-medium text-primary-600 hover:text-primary-500 ml-1">
            Resend code
          </button>
        </p>
      </div>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

definePageMeta({
  layout: 'auth',
});

const router = useRouter();
const verificationCode = ref('');
const isResending = ref(false);

const handleVerification = () => {
  // In a real app, this would verify the code with the backend
  // For now, just redirect to dashboard
  router.push('/dashboard');
};

const resendCode = () => {
  isResending.value = true;
  
  // Simulate API call to resend code
  setTimeout(() => {
    isResending.value = false;
    // Show success message
    alert('Verification code has been resent to your email');
  }, 1000);
};
</script>