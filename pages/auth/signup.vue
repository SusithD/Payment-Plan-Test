<template>
  <div class="min-h-screen bg-gradient-to-br from-primary-50 via-white to-secondary-50 flex items-center justify-center p-4">
    <div class="auth-card fade-in-up">
      <div class="text-center mb-8">
        <NuxtLink to="/" class="inline-block mb-8">
          <h1 class="text-3xl font-bold gradient-text">PaymentPlan</h1>
        </NuxtLink>
        <h2 class="text-2xl font-bold text-gray-900 mb-2">Create your account</h2>
        <p class="text-gray-600">
          Join thousands of users managing their payments with ease
        </p>
      </div>
      
      <form @submit.prevent="handleSignup" class="space-y-6">
        <div class="space-y-4">
          <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <div>
              <label for="first-name" class="form-label">First name</label>
              <input 
                id="first-name" 
                v-model="firstName" 
                type="text" 
                autocomplete="given-name" 
                required 
                class="auth-input" 
                placeholder="Enter your first name"
              />
            </div>
            <div>
              <label for="last-name" class="form-label">Last name</label>
              <input 
                id="last-name" 
                v-model="lastName" 
                type="text" 
                autocomplete="family-name" 
                required 
                class="auth-input" 
                placeholder="Enter your last name"
              />
            </div>
          </div>
          
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
            <label for="mobile" class="form-label">Mobile number</label>
            <input 
              id="mobile" 
              v-model="mobile" 
              type="tel" 
              autocomplete="tel" 
              required 
              class="auth-input" 
              placeholder="Enter your mobile number"
            />
          </div>
          
          <div>
            <label for="password" class="form-label">Password</label>
            <input 
              id="password" 
              v-model="password" 
              type="password" 
              autocomplete="new-password" 
              required 
              class="auth-input" 
              placeholder="Create a password"
            />
            <p class="mt-2 text-sm text-gray-500">
              Password must be at least 8 characters with numbers and special characters
            </p>
          </div>
          
          <div>
            <label for="confirm-password" class="form-label">Confirm password</label>
            <input 
              id="confirm-password" 
              v-model="confirmPassword" 
              type="password" 
              autocomplete="new-password" 
              required 
              class="auth-input" 
              placeholder="Confirm your password"
            />
          </div>
        </div>

        <div class="flex items-start">
          <input 
            id="terms" 
            type="checkbox" 
            required
            class="h-4 w-4 mt-1 text-primary-600 border-gray-300 rounded focus:ring-primary-500" 
          />
          <label for="terms" class="ml-2 block text-sm text-gray-700">
            I agree to the 
            <a href="#" class="font-medium text-primary-600 hover:text-primary-500">Terms of Service</a>
            and
            <a href="#" class="font-medium text-primary-600 hover:text-primary-500">Privacy Policy</a>
          </label>
        </div>

        <button 
          type="submit" 
          class="w-full btn-primary py-4 text-lg"
        >
          Create account
        </button>

        <div class="text-center">
          <p class="text-sm text-gray-600">
            Already have an account?
            <NuxtLink 
              to="/auth/login" 
              class="font-medium text-primary-600 hover:text-primary-500 transition-colors"
            >
              Sign in instead
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
const firstName = ref('');
const lastName = ref('');
const email = ref('');
const mobile = ref('');
const password = ref('');
const confirmPassword = ref('');

const handleSignup = () => {
  router.push('/auth/verify-email');
};
</script>