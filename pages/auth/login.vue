<template>
  <div class="min-h-screen bg-gradient-to-br from-primary-50 via-white to-secondary-50 flex items-center justify-center p-4">
    <div class="auth-card fade-in-up">
      <div class="text-center mb-8">
        <NuxtLink to="/" class="inline-block mb-8">
          <h1 class="text-3xl font-bold gradient-text">PaymentPlan</h1>
        </NuxtLink>
        <h2 class="text-2xl font-bold text-gray-900 mb-2">Welcome back</h2>
        <p class="text-gray-600">
          Enter your credentials to access your account
        </p>
      </div>
      
      <form @submit.prevent="handleLogin" class="space-y-6">
        <div class="space-y-4">
          <div>
            <label for="email" class="form-label">Email address</label>
            <input 
              id="email" 
              v-model="email" 
              type="email" 
              autocomplete="email" 
              required 
              class="auth-input" 
              placeholder="Enter your email"
            />
          </div>
          
          <div>
            <div class="flex items-center justify-between mb-2">
              <label for="password" class="form-label">Password</label>
              <NuxtLink 
                to="/auth/forgot-password" 
                class="text-sm font-medium text-primary-600 hover:text-primary-500 transition-colors"
              >
                Forgot password?
              </NuxtLink>
            </div>
            <input 
              id="password" 
              v-model="password" 
              type="password" 
              autocomplete="current-password" 
              required 
              class="auth-input" 
              placeholder="Enter your password"
            />
          </div>
        </div>

        <div class="flex items-center">
          <input 
            id="remember-me" 
            type="checkbox" 
            class="h-4 w-4 text-primary-600 border-gray-300 rounded focus:ring-primary-500" 
          />
          <label for="remember-me" class="ml-2 block text-sm text-gray-700">
            Keep me signed in
          </label>
        </div>

        <button 
          type="submit" 
          class="w-full btn-primary py-4 text-lg"
        >
          Sign in
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

      <div class="mt-8 pt-8 border-t border-gray-200">
        <div class="flex flex-col space-y-4">
          <button class="btn-outline flex items-center justify-center space-x-3">
            <img src="https://www.google.com/favicon.ico" alt="Google" class="w-5 h-5" />
            <span>Continue with Google</span>
          </button>
          <button class="btn-outline flex items-center justify-center space-x-3">
            <img src="https://www.apple.com/favicon.ico" alt="Apple" class="w-5 h-5" />
            <span>Continue with Apple</span>
          </button>
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

const handleLogin = () => {
  router.push('/dashboard');
};
</script>