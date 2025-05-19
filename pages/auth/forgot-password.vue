<template>
  <div class="w-full max-w-md p-8 space-y-8 bg-white rounded-xl shadow-card">
    <div class="text-center">
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
      <div>
        <label for="email" class="form-label">Email address</label>
        <input 
          id="email" 
          v-model="email" 
          name="email" 
          type="email" 
          autocomplete="email" 
          required 
          class="form-input" 
        />
      </div>

      <div>
        <button 
          type="submit" 
          class="w-full btn-primary py-3"
          :disabled="isSubmitting"
        >
          {{ isSubmitting ? 'Sending reset link...' : 'Send reset link' }}
        </button>
      </div>
      
      <div class="text-center">
        <NuxtLink to="/auth/login" class="font-medium text-primary-600 hover:text-primary-500">
          Back to login
        </NuxtLink>
      </div>
    </form>

    <!-- Success message -->
    <div v-if="submitted" class="mt-4 p-4 rounded-md bg-success-50 text-success-700 fade-in">
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
</template>

<script setup>
import { ref } from 'vue';

definePageMeta({
  layout: 'auth',
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