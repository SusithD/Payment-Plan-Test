<template>
  <div class="min-h-screen flex">
    <!-- Left side - Signup form -->
    <div class="w-full lg:w-1/2 bg-white flex flex-col justify-center px-6 sm:px-10 lg:px-16 xl:px-24 relative z-10">
      <div class="absolute top-8 left-8">
        <NuxtLink to="/" class="flex items-center">
          <span class="text-2xl font-bold gradient-text">PaymentPlan</span>
        </NuxtLink>
      </div>
      
      <div class="max-w-md mx-auto w-full py-20 lg:py-12">
        <div class="mb-8">
          <h2 class="text-3xl font-bold text-gray-900 mb-3">Create your account</h2>
          <p class="text-gray-600">
            Join thousands of users managing their payments with ease
          </p>
        </div>
        
        <!-- Step indicator -->
        <div class="flex items-center mb-10">
          <div class="flex flex-col items-center">
            <div :class="['rounded-full h-10 w-10 flex items-center justify-center text-white', currentStep >= 1 ? 'bg-primary-600' : 'bg-gray-200 text-gray-500']">
              1
            </div>
            <span class="text-sm mt-2 text-gray-600">Personal Info</span>
          </div>
          <div class="flex-1 h-1 mx-4 bg-gray-200">
            <div :class="['h-full bg-primary-600 transition-all duration-300', currentStep >= 2 ? 'w-full' : 'w-0']"></div>
          </div>
          <div class="flex flex-col items-center">
            <div :class="['rounded-full h-10 w-10 flex items-center justify-center', currentStep >= 2 ? 'bg-primary-600 text-white' : 'bg-gray-200 text-gray-500']">
              2
            </div>
            <span class="text-sm mt-2 text-gray-600">OTP Verify</span>
          </div>
          <div class="flex-1 h-1 mx-4 bg-gray-200">
            <div :class="['h-full bg-primary-600 transition-all duration-300', currentStep === 3 ? 'w-full' : 'w-0']"></div>
          </div>
          <div class="flex flex-col items-center">
            <div :class="['rounded-full h-10 w-10 flex items-center justify-center', currentStep === 3 ? 'bg-primary-600 text-white' : 'bg-gray-200 text-gray-500']">
              3
            </div>
            <span class="text-sm mt-2 text-gray-600">Account Setup</span>
          </div>
        </div>
        
        <form @submit.prevent="handleFormSubmit" class="space-y-6">
          <!-- Step 1: Personal Information -->
          <div v-if="currentStep === 1" class="space-y-5">
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-5">
              <div class="form-group">
                <label for="first-name" class="form-label inline-block mb-2 font-medium text-gray-700">First name</label>
                <div class="relative">
                  <svg xmlns="http://www.w3.org/2000/svg" class="input-icon h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z" clip-rule="evenodd" />
                  </svg>
                  <input 
                    id="first-name" 
                    v-model="firstName" 
                    type="text" 
                    autocomplete="given-name" 
                    required 
                    class="auth-input input-with-icon focus:ring-2 focus:ring-primary-500 transition-all duration-200" 
                    placeholder="Enter your first name"
                    :class="{'border-red-300 focus:ring-red-500 error': firstNameError}"
                  />
                </div>
                <p v-if="firstNameError" class="form-error">{{ firstNameError }}</p>
              </div>
              
              <div class="form-group">
                <label for="last-name" class="form-label inline-block mb-2 font-medium text-gray-700">Last name</label>
                <div class="relative">
                  <svg xmlns="http://www.w3.org/2000/svg" class="input-icon h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z" clip-rule="evenodd" />
                  </svg>
                  <input 
                    id="last-name" 
                    v-model="lastName" 
                    type="text" 
                    autocomplete="family-name" 
                    required 
                    class="auth-input input-with-icon focus:ring-2 focus:ring-primary-500 transition-all duration-200" 
                    placeholder="Enter your last name"
                    :class="{'border-red-300 focus:ring-red-500 error': lastNameError}"
                  />
                </div>
                <p v-if="lastNameError" class="form-error">{{ lastNameError }}</p>
              </div>
            </div>

            <div class="form-group">
              <label for="mobile" class="form-label inline-block mb-2 font-medium text-gray-700">Mobile number</label>
              <div class="mobile-input-container">
                <div class="relative">
                  <svg xmlns="http://www.w3.org/2000/svg" class="input-icon h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                  </svg>
                  <select 
                    v-model="countryCode" 
                    class="auth-input country-select focus:ring-2 focus:ring-primary-500 transition-all duration-200"
                  >
                    <option v-for="country in countries" :key="country.code" :value="country.code">
                      {{ country.code }} {{ country.flag }}
                    </option>
                  </select>
                </div>
                <input 
                  id="mobile" 
                  v-model="mobile" 
                  type="tel" 
                  autocomplete="tel" 
                  required 
                  class="auth-input mobile-input focus:ring-2 focus:ring-primary-500 transition-all duration-200" 
                  placeholder="Enter your mobile number"
                  :class="{'border-red-300 focus:ring-red-500 error': mobileError}"
                />
              </div>
              <p class="mt-2 text-xs text-gray-500">We'll send a verification code to this number</p>
              <p v-if="mobileError" class="form-error">{{ mobileError }}</p>
            </div>
          </div>

          <!-- Step 2: OTP Verification -->
          <div v-if="currentStep === 2" class="space-y-5">
            <div class="text-center mb-6">
              <div class="mx-auto flex items-center justify-center h-12 w-12 rounded-full bg-primary-100 mb-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 012 2zm10-10V7a4 4 0 00-8 0v4h8z" />
                </svg>
              </div>
              <h3 class="text-lg font-semibold text-gray-900 mb-2">Verify your phone number</h3>
              <p class="text-sm text-gray-600 mb-4">
                We've sent a 6-digit verification code to<br>
                <span class="font-medium text-gray-900">{{ countryCode }} {{ mobile }}</span>
              </p>
            </div>

            <div class="form-group">
              <label class="form-label inline-block mb-2 font-medium text-gray-700">Enter verification code</label>
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
                  :class="{'border-red-300 focus:border-red-500 focus:ring-red-500': otpError}"
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
                    Resend OTP in {{ resendTimer }}s
                  </span>
                  <span v-else>
                    Resend OTP
                  </span>
                </button>
              </div>
            </div>
          </div>

          <!-- Step 3: Account Setup -->
          <div v-if="currentStep === 3" class="space-y-5">
            <div class="form-group">
              <label for="password" class="form-label inline-block mb-2 font-medium text-gray-700">Password</label>
              <div class="relative">
                <svg xmlns="http://www.w3.org/2000/svg" class="input-icon h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M5 9V7a5 5 0 0110 0v2a2 2 0 012 2v5a2 2 0 01-2 2H5a2 2 0 01-2-2v-5a2 2 0 012-2zm8-2v2H7V7a3 3 0 016 0z" clip-rule="evenodd" />
                </svg>
                <input 
                  id="password" 
                  v-model="password" 
                  :type="showPassword ? 'text' : 'password'" 
                  autocomplete="new-password" 
                  required 
                  class="auth-input input-with-both-icons focus:ring-2 focus:ring-primary-500 transition-all duration-200" 
                  placeholder="••••••••"
                  :class="{'border-red-300 focus:ring-red-500 error': passwordError}"
                />
                <button 
                  type="button" 
                  class="password-toggle"
                  @click="togglePassword"
                >
                  <svg v-if="!showPassword" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path d="M10 12a2 2 0 100-4 2 2 0 000 4z" />
                    <path fill-rule="evenodd" d="M.458 10C1.732 5.943 5.522 3 10 3s8.268 2.943 9.542 7c-1.274 4.057-5.064 7-9.542 7S1.732 14.057.458 10zM14 10a4 4 0 11-8 0 4 4 0 018 0z" clip-rule="evenodd" />
                  </svg>
                  <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M3.707 2.293a1 1 0 00-1.414 1.414l14 14a1 1 0 001.414-1.414l-1.473-1.473A10.014 10.014 0 0019.542 10C18.268 5.943 14.478 3 10 3a9.958 9.958 0 00-4.512 1.074l-1.78-1.781zm4.261 4.26l1.514 1.515a2.003 2.003 0 012.45 2.45l1.514 1.514a4 4 0 00-5.478-5.478z" clip-rule="evenodd" />
                  </svg>
                </button>
              </div>
              <p class="mt-2 text-sm text-gray-500">
                Password must be at least 8 characters with numbers and special characters
              </p>
              <p v-if="passwordError" class="form-error">{{ passwordError }}</p>
            </div>
            
            <div class="form-group">
              <label for="confirm-password" class="form-label inline-block mb-2 font-medium text-gray-700">Confirm password</label>
              <div class="relative">
                <svg xmlns="http://www.w3.org/2000/svg" class="input-icon h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M5 9V7a5 5 0 0110 0v2a2 2 0 012 2v5a2 2 0 01-2 2H5a2 2 0 01-2-2v-5a2 2 0 012-2zm8-2v2H7V7a3 3 0 016 0z" clip-rule="evenodd" />
                </svg>
                <input 
                  id="confirm-password" 
                  v-model="confirmPassword" 
                  :type="showConfirmPassword ? 'text' : 'password'" 
                  autocomplete="new-password" 
                  required 
                  class="auth-input input-with-both-icons focus:ring-2 focus:ring-primary-500 transition-all duration-200" 
                  placeholder="••••••••"
                  :class="{'border-red-300 focus:ring-red-500 error': confirmPasswordError}"
                />
                <button 
                  type="button" 
                  class="password-toggle"
                  @click="toggleConfirmPassword"
                >
                  <svg v-if="!showConfirmPassword" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path d="M10 12a2 2 0 100-4 2 2 0 000 4z" />
                    <path fill-rule="evenodd" d="M.458 10C1.732 5.943 5.522 3 10 3s8.268 2.943 9.542 7c-1.274 4.057-5.064 7-9.542 7S1.732 14.057.458 10zM14 10a4 4 0 11-8 0 4 4 0 018 0z" clip-rule="evenodd" />
                  </svg>
                  <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M3.707 2.293a1 1 0 00-1.414 1.414l14 14a1 1 0 001.414-1.414l-1.473-1.473A10.014 10.014 0 0019.542 10C18.268 5.943 14.478 3 10 3a9.958 9.958 0 00-4.512 1.074l-1.78-1.781zm4.261 4.26l1.514 1.515a2.003 2.003 0 012.45 2.45l1.514 1.514a4 4 0 00-5.478-5.478z" clip-rule="evenodd" />
                  </svg>
                </button>
              </div>
              <p v-if="confirmPasswordError" class="form-error">{{ confirmPasswordError }}</p>
            </div>

            <div class="flex items-start">
              <input 
                id="terms" 
                v-model="acceptTerms"
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
          </div>

          <!-- Navigation buttons -->
          <div class="flex justify-between">
            <button 
              v-if="currentStep > 1"
              type="button" 
              class="px-8 py-3 border border-gray-300 rounded-xl text-gray-700 font-medium hover:bg-gray-50 transition-all focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-primary-500"
              @click="goToPreviousStep"
            >
              <span class="flex items-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M9.707 14.707a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 1.414L7.414 9H15a1 1 0 110 2H7.414l2.293 2.293a1 1 0 010 1.414z" clip-rule="evenodd" />
                </svg>
                Back
              </span>
            </button>
            <div v-else class="w-24"></div>

            <button 
              type="submit" 
              class="w-full sm:w-auto px-8 btn-gradient py-3 rounded-xl text-lg font-medium relative overflow-hidden group transform transition hover:scale-[1.02] active:scale-[0.98]"
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
                  {{ 
                    currentStep === 1 
                      ? 'Send OTP' 
                      : currentStep === 2 
                        ? 'Verify OTP'
                        : (isLoading ? 'Creating account...' : 'Create account')
                  }}
                </span>
                <svg v-if="currentStep < 3" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M10.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L12.586 11H5a1 1 0 110-2h7.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd" />
                </svg>
              </span>
            </button>
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

        <div class="text-center mt-6">
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
      </div>
      
      <div class="absolute bottom-6 left-0 right-0 text-center text-xs text-gray-500 mt-8">
        <p>© 2025 PaymentPlan. All rights reserved.</p>
      </div>
    </div>
    
    <!-- Right side - Image section -->
    <div class="hidden lg:block lg:w-1/2 relative overflow-hidden">
      <!-- Background Image with gradient overlay -->
      <div class="absolute inset-0 bg-cover bg-center" style="background-image: url('https://images.unsplash.com/photo-1520333789090-1afc82db536a?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2071&q=80');">
        <div class="absolute inset-0 bg-gradient-to-br from-primary-900/90 via-primary-800/80 to-primary-700/70"></div>
      </div>
      
      <!-- Content overlay with modern design -->
      <div class="relative z-10 flex flex-col h-full p-12 justify-between">
        <!-- Top Section -->
        <div class="mt-12">
          <div class="inline-flex items-center px-4 py-2 rounded-full bg-white/10 backdrop-blur-md mb-6 border border-white/20">
            <span class="flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
              <span class="text-white font-medium">Trusted by 20,000+ users</span>
            </span>
          </div>
          <h2 class="text-4xl font-bold text-white mb-6 max-w-md leading-tight">Take control of your finances with <span class="text-accent-300">PaymentPlan</span></h2>
          <p class="text-white/90 text-xl max-w-lg leading-relaxed mb-8">Our platform simplifies payment management and provides powerful insights to help you make better financial decisions.</p>
        </div>
        
        <!-- Feature cards with modern design -->
        <div class="space-y-6">
          <!-- Feature Card 1 -->
          <div class="bg-white/10 backdrop-blur-md rounded-xl p-6 border border-white/20 transform transition-all duration-300 hover:translate-x-2">
            <div class="flex items-start space-x-4">
              <div class="flex-shrink-0">
                <div class="h-12 w-12 rounded-xl bg-accent-500/20 flex items-center justify-center">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-accent-300" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                </div>
              </div>
              <div>
                <h3 class="text-white text-lg font-semibold mb-2">Smart Payment Tracking</h3>
                <p class="text-white/80">Set up automated payment reminders and never miss a due date again. Track all your payments in one place.</p>
              </div>
            </div>
          </div>
          
          <!-- Feature Card 2 -->
          <div class="bg-white/10 backdrop-blur-md rounded-xl p-6 border border-white/20 transform transition-all duration-300 hover:translate-x-2">
            <div class="flex items-start space-x-4">
              <div class="flex-shrink-0">
                <div class="h-12 w-12 rounded-xl bg-success-500/20 flex items-center justify-center">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-success-300" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
                  </svg>
                </div>
              </div>
              <div>
                <h3 class="text-white text-lg font-semibold mb-2">Visual Analytics</h3>
                <p class="text-white/80">Get insightful reports and visualizations of your spending habits to optimize your budget.</p>
              </div>
            </div>
          </div>
          
          <!-- Feature Card 3 -->
          <div class="bg-white/10 backdrop-blur-md rounded-xl p-6 border border-white/20 transform transition-all duration-300 hover:translate-x-2">
            <div class="flex items-start space-x-4">
              <div class="flex-shrink-0">
                <div class="h-12 w-12 rounded-xl bg-primary-300/20 flex items-center justify-center">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-300" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z" />
                  </svg>
                </div>
              </div>
              <div>
                <h3 class="text-white text-lg font-semibold mb-2">Secure Transactions</h3>
                <p class="text-white/80">End-to-end encryption and bank-level security protocols to protect all your financial information.</p>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Bottom stats section -->
        <div class="mt-12 grid grid-cols-3 gap-4">
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
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { useRouter } from 'vue-router';

definePageMeta({
  layout: false,
});

const router = useRouter();
const currentStep = ref(1);
const firstName = ref('');
const lastName = ref('');
const mobile = ref('');
const password = ref('');
const confirmPassword = ref('');
const acceptTerms = ref(false);
const showPassword = ref(false);
const showConfirmPassword = ref(false);
const isLoading = ref(false);
const isResending = ref(false);
const firstNameError = ref('');
const lastNameError = ref('');
const mobileError = ref('');
const passwordError = ref('');
const confirmPasswordError = ref('');
const otpError = ref('');
const countryCode = ref('+1');
const otpDigits = ref(['', '', '', '', '', '']);
const otpInputs = ref([]);
const resendTimer = ref(0);
let resendInterval = null;

const countries = ref([
  { code: '+1', name: 'United States/Canada', flag: '🇺🇸' },
  { code: '+44', name: 'United Kingdom', flag: '🇬🇧' },
  { code: '+91', name: 'India', flag: '🇮🇳' },
  { code: '+61', name: 'Australia', flag: '🇦🇺' },
  { code: '+64', name: 'New Zealand', flag: '🇳🇿' },
  { code: '+49', name: 'Germany', flag: '🇩🇪' },
  { code: '+33', name: 'France', flag: '🇫🇷' },
  { code: '+81', name: 'Japan', flag: '🇯🇵' },
  { code: '+86', name: 'China', flag: '🇨🇳' },
  { code: '+65', name: 'Singapore', flag: '🇸🇬' },
]);

const togglePassword = () => {
  showPassword.value = !showPassword.value;
};

const toggleConfirmPassword = () => {
  showConfirmPassword.value = !showConfirmPassword.value;
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

const startResendTimer = () => {
  resendTimer.value = 60;
  resendInterval = setInterval(() => {
    resendTimer.value--;
    if (resendTimer.value <= 0) {
      clearInterval(resendInterval);
    }
  }, 1000);
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

const validateStep1 = () => {
  let isValid = true;
  
  firstNameError.value = '';
  lastNameError.value = '';
  mobileError.value = '';
  
  if (!firstName.value.trim()) {
    firstNameError.value = 'First name is required';
    isValid = false;
  }
  
  if (!lastName.value.trim()) {
    lastNameError.value = 'Last name is required';
    isValid = false;
  }
  
  if (!mobile.value) {
    mobileError.value = 'Mobile number is required';
    isValid = false;
  } else if (!/^\d{10,15}$/.test(mobile.value.replace(/\s+/g, ''))) {
    mobileError.value = 'Please enter a valid mobile number';
    isValid = false;
  }
  
  return isValid;
};

const validateStep2 = () => {
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

const validateStep3 = () => {
  let isValid = true;
  
  passwordError.value = '';
  confirmPasswordError.value = '';
  
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
  
  if (password.value !== confirmPassword.value) {
    confirmPasswordError.value = 'Passwords do not match';
    isValid = false;
  }
  
  return isValid;
};

const goToPreviousStep = () => {
  currentStep.value--;
  window.scrollTo({ top: 0, behavior: 'smooth' });
};

const handleFormSubmit = async () => {
  if (currentStep.value === 1) {
    if (validateStep1()) {
      isLoading.value = true;
      
      // Simulate sending OTP
      await new Promise(resolve => setTimeout(resolve, 1500));
      
      currentStep.value = 2;
      startResendTimer();
      
      // Focus first OTP input
      setTimeout(() => {
        otpInputs.value[0]?.focus();
      }, 100);
      
      isLoading.value = false;
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }
  } else if (currentStep.value === 2) {
    if (validateStep2()) {
      isLoading.value = true;
      
      // Simulate OTP verification
      await new Promise(resolve => setTimeout(resolve, 1000));
      
      currentStep.value = 3;
      isLoading.value = false;
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }
  } else if (currentStep.value === 3) {
    if (validateStep3()) {
      isLoading.value = true;
      
      // Simulate account creation
      await new Promise(resolve => setTimeout(resolve, 2000));
      
      // Redirect to dashboard
      router.push('/dashboard');
    }
  }
};

onUnmounted(() => {
  if (resendInterval) {
    clearInterval(resendInterval);
  }
});
</script>

<style scoped>
.auth-input {
  width: 100%;
  padding: 0.75rem 1rem;
  border-radius: 0.75rem;
  border: 2px solid #e5e7eb;
  background-color: #f9fafb;
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
  font-size: 0.875rem;
  line-height: 1.25rem;
}

.auth-input:focus {
  outline: none;
  border-color: #2C4880;
  background-color: white;
  box-shadow: 0 0 0 3px rgba(44, 72, 128, 0.1);
}

.auth-input::placeholder {
  color: #9ca3af;
}

.auth-input.error {
  border-color: #ef4444;
  background-color: #fef2f2;
}

.auth-input.error:focus {
  border-color: #ef4444;
  box-shadow: 0 0 0 3px rgba(239, 68, 68, 0.1);
}

.auth-select {
  width: 100%;
  padding: 0.75rem 1rem;
  border-radius: 0.75rem;
  border: 2px solid #e5e7eb;
  background-color: #f9fafb;
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
  font-size: 0.875rem;
  line-height: 1.25rem;
  appearance: none;
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' fill='none' viewBox='0 0 20 20'%3e%3cpath stroke='%236b7280' stroke-linecap='round' stroke-linejoin='round' stroke-width='1.5' d='m6 8 4 4 4-4'/%3e%3c/svg%3e");
  background-position: right 0.5rem center;
  background-repeat: no-repeat;
  background-size: 1.5em 1.5em;
}

.auth-select:focus {
  outline: none;
  border-color: #2C4880;
  background-color: white;
  box-shadow: 0 0 0 3px rgba(44, 72, 128, 0.1);
}

.otp-input {
  width: 3rem;
  height: 3rem;
  text-align: center;
  font-size: 1.125rem;
  font-weight: 600;
  border: 2px solid #e5e7eb;
  border-radius: 0.75rem;
  background-color: #f9fafb;
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
}

.otp-input:focus {
  outline: none;
  border-color: #2C4880;
  background-color: white;
  box-shadow: 0 0 0 3px rgba(44, 72, 128, 0.1);
}

.otp-input.error {
  border-color: #ef4444;
  background-color: #fef2f2;
}

.otp-input.error:focus {
  border-color: #ef4444;
  box-shadow: 0 0 0 3px rgba(239, 68, 68, 0.1);
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

.btn-gradient:active {
  transform: translateY(0);
}

.btn-gradient:disabled {
  opacity: 0.6;
  cursor: not-allowed;
  transform: none;
  box-shadow: none;
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
  border: 2px solid #e5e7eb;
  border-radius: 0.75rem;
  color: #4b5563;
  background-color: #f9fafb;
  font-weight: 500;
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
  gap: 0.5rem;
}

.social-btn:hover {
  background-color: white;
  border-color: #d1d5db;
  transform: translateY(-1px);
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
}

.social-btn:focus {
  outline: none;
  border-color: #2C4880;
  box-shadow: 0 0 0 3px rgba(44, 72, 128, 0.1);
}

.form-label {
  display: block;
  font-size: 0.875rem;
  font-weight: 600;
  color: #374151;
  margin-bottom: 0.5rem;
}

.form-error {
  color: #ef4444;
  font-size: 0.875rem;
  margin-top: 0.25rem;
  display: flex;
  align-items: center;
  gap: 0.25rem;
}

.input-icon {
  position: absolute;
  left: 0.75rem;
  top: 50%;
  transform: translateY(-50%);
  color: #9ca3af;
  pointer-events: none;
}

.input-with-icon {
  padding-left: 2.5rem;
}

.toggle-password-btn {
  position: absolute;
  right: 0.75rem;
  top: 50%;
  transform: translateY(-50%);
  color: #9ca3af;
  transition: color 0.2s;
  background: none;
  border: none;
  padding: 0.25rem;
  border-radius: 0.25rem;
}

.toggle-password-btn:hover {
  color: #6b7280;
}

.toggle-password-btn:focus {
  outline: none;
  color: #2C4880;
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

/* Mobile responsive adjustments */
@media (max-width: 640px) {
  .auth-input {
    font-size: 1rem; /* Prevent zoom on iOS */
  }
  
  .otp-input {
    width: 2.5rem;
    height: 2.5rem;
    font-size: 1rem;
  }
  
  .social-btn {
    font-size: 0.875rem;
    padding: 0.625rem 0.75rem;
  }
}
</style>