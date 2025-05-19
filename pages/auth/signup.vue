<template>
  <div class="min-h-screen flex flex-col lg:flex-row">
    <!-- Left side - Signup form -->
    <div class="w-full lg:w-1/2 bg-white flex flex-col justify-center px-4 sm:px-6 lg:px-8 xl:px-12 relative">
      <div class="absolute top-4 left-4 sm:top-6 sm:left-6">
        <NuxtLink to="/" class="flex items-center">
          <span class="text-2xl font-bold bg-gradient-to-r from-indigo-600 to-purple-600 bg-clip-text text-transparent">PaymentPlan</span>
        </NuxtLink>
      </div>

      <div class="max-w-md mx-auto w-full py-8 sm:py-12 lg:py-16">
        <div class="mb-8">
          <h2 class="text-2xl sm:text-3xl font-bold text-gray-900 mb-3">Create your account</h2>
          <p class="text-gray-600 text-sm sm:text-base">Join thousands of users managing their payments with ease</p>
        </div>

        <form @submit.prevent="handleSignup" class="space-y-5">
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div class="form-group">
              <label for="first-name" class="block text-sm font-medium text-gray-700">First name</label>
              <div class="relative mt-1">
                <span class="absolute inset-y-0 left-3 flex items-center text-gray-400">
                  <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z" clip-rule="evenodd" />
                  </svg>
                </span>
                <input
                  id="first-name"
                  v-model="firstName"
                  type="text"
                  autocomplete="given-name"
                  required
                  class="block w-full pl-10 pr-3 py-2 border rounded-lg focus:ring-2 focus:ring-indigo-500 transition-all duration-200"
                  :class="{ 'border-red-300 focus:ring-red-500': firstNameError }"
                  placeholder="Enter your first name"
                />
              </div>
              <p v-if="firstNameError" class="mt-1 text-sm text-red-500">{{ firstNameError }}</p>
            </div>

            <div class="form-group">
              <label for="last-name" class="block text-sm font-medium text-gray-700">Last name</label>
              <div class="relative mt-1">
                <span class="absolute inset-y-0 left-3 flex items-center text-gray-400">
                  <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z" clip-rule="evenodd" />
                  </svg>
                </span>
                <input
                  id="last-name"
                  v-model="lastName"
                  type="text"
                  autocomplete="family-name"
                  required
                  class="block w-full pl-10 pr-3 py-2 border rounded-lg focus:ring-2 focus:ring-indigo-500 transition-all duration-200"
                  :class="{ 'border-red-300 focus:ring-red-500': lastNameError }"
                  placeholder="Enter your last name"
                />
              </div>
              <p v-if="lastNameError" class="mt-1 text-sm text-red-500">{{ lastNameError }}</p>
            </div>
          </div>

          <div class="form-group">
            <label for="email" class="block text-sm font-medium text-gray-700">Email address</label>
            <div class="relative mt-1">
              <span class="absolute inset-y-0 left-3 flex items-center text-gray-400">
                <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
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
                class="block w-full pl-10 pr-3 py-2 border rounded-lg focus:ring-2 focus:ring-indigo-500 transition-all duration-200"
                :class="{ 'border-red-300 focus:ring-red-500': emailError }"
                placeholder="your.email@example.com"
              />
            </div>
            <p v-if="emailError" class="mt-1 text-sm text-red-500">{{ emailError }}</p>
          </div>

          <div class="form-group">
            <label for="mobile" class="block text-sm font-medium text-gray-700">Mobile number</label>
            <div class="relative mt-1">
              <span class="absolute inset-y-0 left-3 flex items-center text-gray-400">
                <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                  <path d="M2 3a1 1 0 011-1h2.153a1 1 0 01.986.836l.74 4.435a1 1 0 01-.54 1.06l-1.548.773a11.037 11.037 0 006.105 6.105l.774-1.548a1 1 0 011.059-.54l4.435.74a1 1 0 01.836.986V17a1 1 0 01-1 1h-2C7.82 18 2 12.18 2 5V3z" />
                </svg>
              </span>
              <input
                id="mobile"
                v-model="mobile"
                type="tel"
                autocomplete="tel"
                required
                class="block w-full pl-10 pr-3 py-2 border rounded-lg focus:ring-2 focus:ring-indigo-500 transition-all duration-200"
                :class="{ 'border-red-300 focus:ring-red-500': mobileError }"
                placeholder="Enter your mobile number"
              />
            </div>
            <p v-if="mobileError" class="mt-1 text-sm text-red-500">{{ mobileError }}</p>
          </div>

          <div class="form-group">
            <label for="password" class="block text-sm font-medium text-gray-700">Password</label>
            <div class="relative mt-1">
              <span class="absolute inset-y-0 left-3 flex items-center text-gray-400">
                <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M5 9V7a5 5 0 0110 0v2a2 2 0 012 2v5a2 2 0 01-2 2H5a2 2 0 01-2-2v-5a2 2 0 012-2zm8-2v2H7V7a3 3 0 016 0z" clip-rule="evenodd" />
                </svg>
              </span>
              <input
                id="password"
                v-model="password"
                :type="showPassword ? 'text' : 'password'"
                autocomplete="new-password"
                required
                class="block w-full pl-10 pr-10 py-2 border rounded-lg focus:ring-2 focus:ring-indigo-500 transition-all duration-200"
                :class="{ 'border-red-300 focus:ring-red-500': passwordError }"
                placeholder="••••••••"
              />
              <button
                type="button"
                class="absolute inset-y-0 right-3 flex items-center text-gray-400 hover:text-gray-600"
                @click="togglePassword"
              >
                <svg v-if="!showPassword" class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                  <path d="M10 12a2 2 0 100-4 2 2 0 000 4z" />
                  <path fill-rule="evenodd" d="M.458 10C1.732 5.943 5.522 3 10 3s8.268 2.943 9.542 7c-1.274 4.057-5.064 7-9.542 7S1.732 14.057.458 10zM14 10a4 4 0 11-8 0 4 4 0 018 0z" clip-rule="evenodd" />
                </svg>
                <svg v-else class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M3.707 2.293a1 1 0 00-1.414 1.414l14 14a1 1 0 001.414-1.414l-1.473-1.473A10.014 10.014 0 0019.542 10C18.268 5.943 14.478 3 10 3a9.958 9.958 0 00-4.512 1.074l-1.78-1.781zm4.261 4.26l1.514 1.515a2.003 2.003 0 012.45 2.45l1.514 1.514a4 4 0 00-5.478-5.478z" clip-rule="evenodd" />
                  <path d="M12.454 16.697L9.75 13.992a4 4 0 01-3.742-3.741L2.335 6.578A9.98 9.98 0 00.458 10c1.274 4.057 5.065 7 9.542 7 .847 0 1.669-.105 2.454-.303z" />
                </svg>
              </button>
            </div>
            <p class="mt-2 text-sm text-gray-500">Password must be at least 8 characters with numbers and special characters</p>
            <p v-if="passwordError" class="mt-1 text-sm text-red-500">{{ passwordError }}</p>
          </div>

          <div class="form-group">
            <label for="confirm-password" class="block text-sm font-medium text-gray-700">Confirm password</label>
            <div class="relative mt-1">
              <span class="absolute inset-y-0 left-3 flex items-center text-gray-400">
                <svg class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M5 9V7a5 5 0 0110 0v2a2 2 0 012 2v5a2 2 0 01-2 2H5a2 2 0 01-2-2v-5a2 2 0 012-2zm8-2v2H7V7a3 3 0 016 0z" clip-rule="evenodd" />
                </svg>
              </span>
              <input
                id="confirm-password"
                v-model="confirmPassword"
                :type="showConfirmPassword ? 'text' : 'password'"
                autocomplete="new-password"
                required
                class="block w-full pl-10 pr-10 py-2 border rounded-lg focus:ring-2 focus:ring-indigo-500 transition-all duration-200"
                :class="{ 'border-red-300 focus:ring-red-500': confirmPasswordError }"
                placeholder="••••••••"
              />
              <button
                type="button"
                class="absolute inset-y-0 right-3 flex items-center text-gray-400 hover:text-gray-600"
                @click="toggleConfirmPassword"
              >
                <svg v-if="!showConfirmPassword" class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                  <path d="M10 12a2 2 0 100-4 2 2 0 000 4z" />
                  <path fill-rule="evenodd" d="M.458 10C1.732 5.943 5.522 3 10 3s8.268 2.943 9.542 7c-1.274 4.057-5.064 7-9.542 7S1.732 14.057.458 10zM14 10a4 4 0 11-8 0 4 4 0 018 0z" clip-rule="evenodd" />
                </svg>
                <svg v-else class="h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M3.707 2.293a1 1 0 00-1.414 1.414l14 14a1 1 0 001.414-1.414l-1.473-1.473A10.014 10.014 0 0019.542 10C18.268 5.943 14.478 3 10 3a9.958 9.958 0 00-4.512 1.074l-1.78-1.781zm4.261 4.26l1.514 1.515a2.003 2.003 0 012.45 2.45l1.514 1.514a4 4 0 00-5.478-5.478z" clip-rule="evenodd" />
                  <path d="M12.454 16.697L9.75 13.992a4 4 0 01-3.742-3.741L2.335 6.578A9.98 9.98 0 00.458 10c1.274 4.057 5.065 7 9.542 7 .847 0 1.669-.105 2.454-.303z" />
                </svg>
              </button>
            </div>
            <p v-if="confirmPasswordError" class="mt-1 text-sm text-red-500">{{ confirmPasswordError }}</p>
          </div>

          <div class="flex items-start">
            <input
              id="terms"
              v-model="acceptTerms"
              type="checkbox"
              required
              class="h-4 w-4 mt-1 text-indigo-600 border-gray-300 rounded focus:ring-indigo-500"
            />
            <label for="terms" class="ml-2 block text-sm text-gray-700">
              I agree to the
              <a href="#" class="font-medium text-indigo-600 hover:text-indigo-500">Terms of Service</a>
              and
              <a href="#" class="font-medium text-indigo-600 hover:text-indigo-500">Privacy Policy</a>
            </label>
          </div>

          <button
            type="submit"
            class="w-full bg-gradient-to-r from-indigo-600 to-purple-600 text-white py-3 rounded-lg font-medium relative overflow-hidden group hover:scale-[1.02] transition-transform duration-200"
            :disabled="isLoading"
          >
            <span class="relative flex items-center justify-center">
              <span v-if="isLoading" class="mr-2">
                <svg class="animate-spin h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                  <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                  <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                </svg>
              </span>
              <span>{{ isLoading ? 'Creating account...' : 'Create account' }}</span>
            </span>
          </button>

          <div class="text-center text-sm">
            <p class="text-gray-600">
              Already have an account?
              <NuxtLink to="/auth/login" class="font-medium text-indigo-600 hover:text-indigo-500">Sign in instead</NuxtLink>
            </p>
          </div>
        </form>

        <div class="mt-8">
          <div class="relative">
            <div class="absolute inset-0 flex items-center">
              <div class="w-full border-t border-gray-200"></div>
            </div>
            <div class="relative flex justify-center text-sm">
              <span class="px-4 bg-white text-gray-500">Or continue with</span>
            </div>
          </div>

          <div class="mt-6 grid grid-cols-2 gap-3">
            <button class="flex items-center justify-center py-2 px-4 border border-gray-300 rounded-lg hover:bg-gray-50 transition-all duration-200">
              <img src="https://www.google.com/favicon.ico" alt="Google" class="w-5 h-5 mr-2" />
              <span>Google</span>
            </button>
            <button class="flex items-center justify-center py-2 px-4 border border-gray-300 rounded-lg hover:bg-gray-50 transition-all duration-200">
              <img src="https://www.apple.com/favicon.ico" alt="Apple" class="w-5 h-5 mr-2" />
              <span>Apple</span>
            </button>
          </div>
        </div>
      </div>

      <div class="absolute bottom-4 left-0 right-0 text-center text-xs text-gray-500">
        <p>© 2025 PaymentPlan. All rights reserved.</p>
      </div>
    </div>

    <!-- Right side - Image section -->
    <div class="hidden lg:block lg:w-1/2 relative overflow-hidden">
      <div class="absolute inset-0 bg-cover bg-center" style="background-image: url('https://images.unsplash.com/photo-1520333789090-1afc82db536a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2071&q=80');">
        <div class="absolute inset-0 bg-gradient-to-t from-indigo-900/70 via-indigo-800/50 to-indigo-800/30"></div>
      </div>

      <div class="relative z-10 flex flex-col h-full p-8 sm:p-12 justify-between">
        <div class="mt-12">
          <div class="inline-block px-4 py-2 rounded-full bg-white/10 backdrop-blur-sm mb-6">
            <span class="text-white font-medium">Smart Financial Management</span>
          </div>
          <h2 class="text-3xl sm:text-4xl font-bold text-white mb-4 max-w-md">Simplify your payments and track expenses effortlessly</h2>
          <p class="text-white/80 text-base sm:text-lg max-w-md">Our platform helps you manage payment schedules, track spending patterns, and achieve your financial goals.</p>
        </div>

        <div class="mt-auto">
          <div class="bg-white/10 backdrop-blur-md rounded-xl p-6">
            <div class="flex items-start space-x-4">
              <div class="flex-shrink-0">
                <div class="h-12 w-12 rounded-full bg-gradient-to-br from-indigo-300 to-purple-300 flex items-center justify-center text-white font-bold">
                  SW
                </div>
              </div>
              <div>
                <div class="flex mb-1">
                  <svg class="h-5 w-5 text-yellow-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                    <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                  </svg>
                  <svg class="h-5 w-5 text-yellow-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                    <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                  </svg>
                  <svg class="h-5 w-5 text-yellow-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                    <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                  </svg>
                  <svg class="h-5 w-5 text-yellow-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                    <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                  </svg>
                </div>
                <p class="text-white text-lg font-medium mb-2">Sarah Wilson</p>
                <p class="text-white/80 italic text-sm sm:text-base">"Since joining PaymentPlan, I've been able to organize all my payments in one place. The alerts help me stay on top of due dates and I've saved money by avoiding late fees!"</p>
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
const acceptTerms = ref(false);
const showPassword = ref(false);
const showConfirmPassword = ref(false);
const isLoading = ref(false);
const firstNameError = ref('');
const lastNameError = ref('');
const emailError = ref('');
const mobileError = ref('');
const passwordError = ref('');
const confirmPasswordError = ref('');

const togglePassword = () => {
  showPassword.value = !showPassword.value;
};

const toggleConfirmPassword = () => {
  showConfirmPassword.value = !showConfirmPassword.value;
};

const validateForm = () => {
  let isValid = true;

  // Reset errors
  firstNameError.value = '';
  lastNameError.value = '';
  emailError.value = '';
  mobileError.value = '';
  passwordError.value = '';
  confirmPasswordError.value = '';

  // First name validation
  if (!firstName.value.trim()) {
    firstNameError.value = 'First name is required';
    isValid = false;
  }

  // Last name validation
  if (!lastName.value.trim()) {
    lastNameError.value = 'Last name is required';
    isValid = false;
  }

  // Email validation
  if (!email.value) {
    emailError.value = 'Email is required';
    isValid = false;
  } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email.value)) {
    emailError.value = 'Please enter a valid email address';
    isValid = false;
  }

  // Mobile validation
  if (!mobile.value) {
    mobileError.value = 'Mobile number is required';
    isValid = false;
  }

  // Password validation
  if (!password.value) {
    passwordError.value = 'Password is required';
    isValid = false;
  } else if (password.value.length < 8) {
    passwordError.value = 'Password must be at least 8 characters';
    isValid = false;
  } else if (!/(?=.*[0-9])(?=.*[!@#$%^&*])/.test(password.value)) {
    passwordError.value = 'Password must include numbers and special characters';
    isValid = false;
  }

  // Confirm password validation
  if (password.value !== confirmPassword.value) {
    confirmPasswordError.value = 'Passwords do not match';
    isValid = false;
  }

  return isValid;
};

const handleSignup = async () => {
  if (!validateForm()) return;

  try {
    isLoading.value = true;
    await new Promise(resolve => setTimeout(resolve, 1500));
    router.push('/auth/verify-email');
  } catch (error) {
    console.error('Signup failed:', error);
  } finally {
    isLoading.value = false;
  }
};
</script>

<style scoped>
/* Animation for form elements */
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

.form-group:nth-child(3) {
  animation-delay: 0.3s;
}

.form-group:nth-child(4) {
  animation-delay: 0.4s;
}

.form-group:nth-child(5) {
  animation-delay: 0.5s;
}

.form-group:nth-child(6) {
  animation-delay: 0.6s;
}

button[type="submit"] {
  animation: fadeIn 0.5s ease-out forwards;
  animation-delay: 0.7s;
  opacity: 0;
}
</style>