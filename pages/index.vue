<template>
  <div>
    <!-- Enhanced Hero Section (keeping as is since it's already well-designed) -->
    <section class="bg-gradient-to-r from-primary-600 to-primary-800 text-white relative overflow-hidden">
      <!-- Background pattern -->
      <div class="absolute inset-0 opacity-10">
        <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg">
          <defs>
            <pattern id="smallGrid" width="20" height="20" patternUnits="userSpaceOnUse">
              <path d="M 20 0 L 0 0 0 20" fill="none" stroke="currentColor" stroke-width="0.5" />
            </pattern>
          </defs>
          <rect width="100%" height="100%" fill="url(#smallGrid)" />
        </svg>
      </div>
      
      <div class="container-custom py-16 md:py-28 relative z-10">
        <div class="grid md:grid-cols-2 gap-12 items-center">
          <div class="max-w-xl">
            <span class="bg-primary-800 text-primary-100 text-sm font-medium py-1 px-3 rounded-full mb-4 inline-block">
              Financial Freedom Starts Here
            </span>
            <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold mb-6 text-white leading-tight">
              Simplify Your <span class="text-yellow-300">Payment Plans</span>
            </h1>
            <p class="text-xl text-primary-100 mb-8 leading-relaxed">
              Manage your instalments, make payments, and stay on top of your financial commitments with our secure and easy-to-use payment portal. Join thousands of satisfied customers who trust us with their payment management.
            </p>
            
            <div class="space-y-6">
              <div class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-4">
                <NuxtLink to="/auth/signup" class="btn bg-white text-primary-700 hover:bg-primary-50 focus:ring-white flex items-center justify-center group">
                  <span>Create Account</span>
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2 transform group-hover:translate-x-1 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                  </svg>
                </NuxtLink>
                <NuxtLink to="/auth/login" class="btn bg-primary-700 border border-white text-white hover:bg-primary-800 focus:ring-white flex items-center justify-center">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 16l-4-4m0 0l4-4m-4 4h14m-5 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h7a3 3 0 013 3v1" />
                  </svg>
                  <span>Sign In</span>
                </NuxtLink>
              </div>
              
              <!-- Trust indicators -->
              <div class="flex flex-wrap items-center gap-6 pt-4 border-t border-primary-500/30">
                <div class="flex items-center text-primary-100">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
                  </svg>
                  <span>Bank-level Security</span>
                </div>
                <div class="flex items-center text-primary-100">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                  <span>24/7 Support</span>
                </div>
                <div class="flex items-center text-primary-100">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 10h4.764a2 2 0 011.789 2.894l-3.5 7A2 2 0 0115.263 21h-4.017c-.163 0-.326-.02-.485-.06L7 20m7-10V5a2 2 0 00-2-2h-.095c-.5 0-.905.405-.905.905 0 .714-.211 1.412-.608 2.006L7 11v9m7-10h-2M7 20H5a2 2 0 01-2-2v-6a2 2 0 012-2h2.5" />
                  </svg>
                  <span>4.9/5 User Rating</span>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Interactive illustration or preview -->
          <div class="hidden md:block relative">
            <div class="bg-white/10 backdrop-blur-sm rounded-lg p-6 shadow-xl border border-white/20 transform hover:-translate-y-2 transition-transform duration-300">
              <div class="bg-primary-700/50 rounded-t-md py-3 px-4 flex items-center">
                <div class="flex space-x-2">
                  <div class="w-3 h-3 bg-red-400 rounded-full"></div>
                  <div class="w-3 h-3 bg-yellow-400 rounded-full"></div>
                  <div class="w-3 h-3 bg-green-400 rounded-full"></div>
                </div>
                <div class="ml-4 h-5 w-40 bg-primary-600/50 rounded"></div>
              </div>
              <div class="bg-primary-800/30 p-4 space-y-3">
                <div class="flex items-center justify-between pb-2 border-b border-white/10">
                  <div class="h-4 w-32 bg-primary-600/40 rounded"></div>
                  <div class="h-4 w-16 bg-green-500/40 rounded"></div>
                </div>
                <div class="flex items-center justify-between pb-2 border-b border-white/10">
                  <div class="h-4 w-36 bg-primary-600/40 rounded"></div>
                  <div class="h-4 w-20 bg-yellow-500/40 rounded"></div>
                </div>
                <div class="flex items-center justify-between pb-2 border-b border-white/10">
                  <div class="h-4 w-28 bg-primary-600/40 rounded"></div>
                  <div class="h-4 w-24 bg-blue-500/40 rounded"></div>
                </div>
                <div class="pt-2 flex justify-end">
                  <div class="h-8 w-24 bg-primary-500/50 rounded-md"></div>
                </div>
              </div>
            </div>
            
            <!-- Decorative elements -->
            <div class="absolute -top-6 -right-6 w-12 h-12 bg-yellow-300 rounded-full opacity-70 animate-pulse"></div>
            <div class="absolute -bottom-4 -left-4 w-8 h-8 bg-blue-400 rounded-full opacity-70"></div>
          </div>
        </div>
      </div>
      
      <!-- Wave effect at the bottom -->
      <div class="absolute bottom-0 left-0 right-0">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320" class="text-white fill-current">
          <path fill-opacity="1" d="M0,288L48,272C96,256,192,224,288,197.3C384,171,480,149,576,165.3C672,181,768,235,864,250.7C960,267,1056,245,1152,224C1248,203,1344,181,1392,170.7L1440,160L1440,320L1392,320C1344,320,1248,320,1152,320C1056,320,960,320,864,320C768,320,672,320,576,320C480,320,384,320,288,320C192,320,96,320,48,320L0,320Z"></path>
        </svg>
      </div>
    </section>

    <!-- Features Section - Enhanced with icons and animations -->
    <section class="py-20 bg-white">
      <div class="container-custom">
        <div class="text-center max-w-3xl mx-auto mb-16">
          <span class="text-primary-600 font-medium block mb-2">POWERFUL FEATURES</span>
          <h2 class="text-3xl md:text-4xl font-bold mb-6">Everything You Need to Manage Your Payments</h2>
          <p class="text-lg text-gray-600">
            Our platform offers a comprehensive suite of tools to help you manage your payment plans efficiently.
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div class="rounded-xl bg-white p-8 border border-gray-100 shadow-lg hover:shadow-xl hover:-translate-y-1 transition-all duration-300">
            <div class="h-14 w-14 bg-primary-100 text-primary-600 rounded-xl flex items-center justify-center mb-6">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-7 w-7" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-3 7h3m-3 4h3m-6-4h.01M9 16h.01" />
              </svg>
            </div>
            <h3 class="text-xl font-semibold mb-3">View Instalments</h3>
            <p class="text-gray-600 mb-4">
              Easily view all your pending instalments, including due dates, amounts, and descriptions in one place.
            </p>
            <NuxtLink to="/dashboard" class="text-primary-600 font-medium flex items-center group">
              Learn more
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1 group-hover:ml-2 transition-all" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
            </NuxtLink>
          </div>

          <div class="rounded-xl bg-white p-8 border border-gray-100 shadow-lg hover:shadow-xl hover:-translate-y-1 transition-all duration-300">
            <div class="h-14 w-14 bg-secondary-100 text-secondary-600 rounded-xl flex items-center justify-center mb-6">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-7 w-7" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
              </svg>
            </div>
            <h3 class="text-xl font-semibold mb-3">Secure Payments</h3>
            <p class="text-gray-600 mb-4">
              Make secure payments using our integrated payment gateway with multiple payment methods.
            </p>
            <NuxtLink to="/payments" class="text-secondary-600 font-medium flex items-center group">
              Learn more
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1 group-hover:ml-2 transition-all" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
            </NuxtLink>
          </div>

          <div class="rounded-xl bg-white p-8 border border-gray-100 shadow-lg hover:shadow-xl hover:-translate-y-1 transition-all duration-300">
            <div class="h-14 w-14 bg-accent-100 text-accent-600 rounded-xl flex items-center justify-center mb-6">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-7 w-7" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
              </svg>
            </div>
            <h3 class="text-xl font-semibold mb-3">Payment History</h3>
            <p class="text-gray-600 mb-4">
              Access your complete payment history with detailed transaction records and receipts.
            </p>
            <NuxtLink to="/history" class="text-accent-600 font-medium flex items-center group">
              Learn more
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1 group-hover:ml-2 transition-all" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
            </NuxtLink>
          </div>
        </div>
      </div>
    </section>

    <!-- How It Works - Enhanced with animated elements -->
    <section class="py-24 bg-gray-50 relative overflow-hidden">
      <!-- Background decorative elements -->
      <div class="absolute -top-12 -right-12 w-64 h-64 bg-primary-300/20 rounded-full blur-3xl"></div>
      <div class="absolute -bottom-20 -left-20 w-80 h-80 bg-secondary-300/20 rounded-full blur-3xl"></div>
      
      <div class="container-custom relative z-10">
        <div class="text-center max-w-3xl mx-auto mb-16">
          <span class="text-primary-600 font-medium block mb-2">SIMPLE PROCESS</span>
          <h2 class="text-3xl md:text-4xl font-bold mb-6">How It Works</h2>
          <p class="text-lg text-gray-600">
            Our intuitive platform makes managing your payments effortless in just a few simple steps
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
          <!-- Step 1 -->
          <div class="text-center relative">
            <div class="h-20 w-20 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mb-6 mx-auto border-4 border-white shadow-lg">
              <span class="text-2xl font-bold">1</span>
            </div>
            <!-- Connector line -->
            <div class="hidden md:block absolute top-10 left-1/2 w-full h-1 bg-primary-100"></div>
            <h3 class="text-xl font-semibold mb-3">Create an Account</h3>
            <p class="text-gray-600">
              Sign up with your email and set a secure password to get started.
            </p>
          </div>

          <!-- Step 2 -->
          <div class="text-center relative">
            <div class="h-20 w-20 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mb-6 mx-auto border-4 border-white shadow-lg">
              <span class="text-2xl font-bold">2</span>
            </div>
            <!-- Connector line -->
            <div class="hidden md:block absolute top-10 left-1/2 w-full h-1 bg-primary-100"></div>
            <h3 class="text-xl font-semibold mb-3">View Your Instalments</h3>
            <p class="text-gray-600">
              See all your pending instalments with details like due dates and amounts.
            </p>
          </div>

          <!-- Step 3 -->
          <div class="text-center relative">
            <div class="h-20 w-20 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mb-6 mx-auto border-4 border-white shadow-lg">
              <span class="text-2xl font-bold">3</span>
            </div>
            <!-- Connector line -->
            <div class="hidden md:block absolute top-10 left-1/2 w-full h-1 bg-primary-100"></div>
            <h3 class="text-xl font-semibold mb-3">Select Payments</h3>
            <p class="text-gray-600">
              Choose which instalments you want to pay and proceed to checkout.
            </p>
          </div>

          <!-- Step 4 -->
          <div class="text-center">
            <div class="h-20 w-20 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mb-6 mx-auto border-4 border-white shadow-lg">
              <span class="text-2xl font-bold">4</span>
            </div>
            <h3 class="text-xl font-semibold mb-3">Complete Payment</h3>
            <p class="text-gray-600">
              Pay securely using your preferred payment method and get instant confirmation.
            </p>
          </div>
        </div>
        
        <!-- Call to action button -->
        <div class="text-center mt-14">
          <NuxtLink to="/auth/signup" class="btn bg-primary-600 text-white hover:bg-primary-700">
            Get Started Now
          </NuxtLink>
        </div>
      </div>
    </section>
    
    <!-- Testimonials Section - New Section -->
    <section class="py-24 bg-white">
      <div class="container-custom">
        <div class="text-center max-w-3xl mx-auto mb-16">
          <span class="text-primary-600 font-medium block mb-2">TESTIMONIALS</span>
          <h2 class="text-3xl md:text-4xl font-bold mb-6">What Our Users Say</h2>
          <p class="text-lg text-gray-600">
            Discover why thousands of customers trust our platform for their payment management needs
          </p>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <!-- Testimonial 1 -->
          <div class="bg-gray-50 rounded-xl p-8 shadow-sm hover:shadow-md transition-shadow">
            <div class="flex items-center space-x-1 mb-4 text-yellow-400">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
            </div>
            <p class="text-gray-700 mb-6 italic">
              "This platform has completely transformed how I manage my payments. The interface is intuitive, and I love getting notifications before my payments are due."
            </p>
            <div class="flex items-center">
              <div class="w-12 h-12 bg-primary-200 rounded-full flex items-center justify-center text-primary-700 font-bold mr-4">JD</div>
              <div>
                <h4 class="font-semibold">John Doe</h4>
                <p class="text-sm text-gray-500">Customer since 2023</p>
              </div>
            </div>
          </div>
          
          <!-- Testimonial 2 -->
          <div class="bg-gray-50 rounded-xl p-8 shadow-sm hover:shadow-md transition-shadow">
            <div class="flex items-center space-x-1 mb-4 text-yellow-400">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
            </div>
            <p class="text-gray-700 mb-6 italic">
              "The security features are impressive. I feel confident making payments through this platform knowing my financial information is secure and protected."
            </p>
            <div class="flex items-center">
              <div class="w-12 h-12 bg-secondary-200 rounded-full flex items-center justify-center text-secondary-700 font-bold mr-4">JS</div>
              <div>
                <h4 class="font-semibold">Jane Smith</h4>
                <p class="text-sm text-gray-500">Customer since 2024</p>
              </div>
            </div>
          </div>
          
          <!-- Testimonial 3 -->
          <div class="bg-gray-50 rounded-xl p-8 shadow-sm hover:shadow-md transition-shadow">
            <div class="flex items-center space-x-1 mb-4 text-yellow-400">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
            </div>
            <p class="text-gray-700 mb-6 italic">
              "Customer service is outstanding. When I had questions about a payment, they responded quickly and resolved my issue within minutes. Highly recommend!"
            </p>
            <div class="flex items-center">
              <div class="w-12 h-12 bg-accent-200 rounded-full flex items-center justify-center text-accent-700 font-bold mr-4">RJ</div>
              <div>
                <h4 class="font-semibold">Robert Johnson</h4>
                <p class="text-sm text-gray-500">Customer since 2022</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- FAQ Section - New Section -->
    <section class="py-24 bg-gray-50">
      <div class="container-custom">
        <div class="text-center max-w-3xl mx-auto mb-16">
          <span class="text-primary-600 font-medium block mb-2">FAQs</span>
          <h2 class="text-3xl md:text-4xl font-bold mb-6">Frequently Asked Questions</h2>
          <p class="text-lg text-gray-600">
            Find answers to common questions about our payment management platform
          </p>
        </div>
        
        <div class="max-w-3xl mx-auto divide-y divide-gray-200">
          <!-- FAQ Item 1 -->
          <details class="group py-4">
            <summary class="flex justify-between items-center font-semibold cursor-pointer list-none">
              <span>How secure is the payment platform?</span>
              <span class="transition group-open:rotate-180">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                </svg>
              </span>
            </summary>
            <p class="text-gray-600 mt-4 ml-4">
              Our platform utilizes bank-level security protocols including SSL encryption, 
              two-factor authentication, and regular security audits to ensure your financial 
              information is always protected. We comply with PCI DSS standards and never 
              store your full credit card details on our servers.
            </p>
          </details>
          
          <!-- FAQ Item 2 -->
          <details class="group py-4">
            <summary class="flex justify-between items-center font-semibold cursor-pointer list-none">
              <span>What payment methods are accepted?</span>
              <span class="transition group-open:rotate-180">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                </svg>
              </span>
            </summary>
            <p class="text-gray-600 mt-4 ml-4">
              We accept all major credit and debit cards (Visa, Mastercard, American Express), 
              PayPal, bank transfers, and select digital wallets. Our goal is to provide you 
              with flexible payment options that suit your preferences.
            </p>
          </details>
          
          <!-- FAQ Item 3 -->
          <details class="group py-4">
            <summary class="flex justify-between items-center font-semibold cursor-pointer list-none">
              <span>How do I know my payment was successful?</span>
              <span class="transition group-open:rotate-180">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                </svg>
              </span>
            </summary>
            <p class="text-gray-600 mt-4 ml-4">
              After completing a payment, you'll receive an instant confirmation on the screen and 
              an email receipt with all transaction details. You can also view all your payments 
              in the history section of your account dashboard at any time.
            </p>
          </details>
          
          <!-- FAQ Item 4 -->
          <details class="group py-4">
            <summary class="flex justify-between items-center font-semibold cursor-pointer list-none">
              <span>Can I schedule automatic payments?</span>
              <span class="transition group-open:rotate-180">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                </svg>
              </span>
            </summary>
            <p class="text-gray-600 mt-4 ml-4">
              Yes, our platform allows you to set up automatic payments for recurring instalments. 
              You can easily configure payment dates, frequency, and maximum amounts in your account settings. 
              You'll always receive a notification before an automatic payment is processed.
            </p>
          </details>
        </div>
        
        <div class="mt-12 text-center">
          <p class="mb-4 text-gray-700">Still have questions?</p>
          <button class="btn bg-gray-100 hover:bg-gray-200 text-gray-800">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
            </svg>
            Contact Support
          </button>
        </div>
      </div>
    </section>
    
    <!-- Stats Section - New Section -->
    <section class="py-16 bg-primary-900 text-white">
      <div class="container-custom">
        <div class="grid grid-cols-2 md:grid-cols-4 gap-8 text-center">
          <div>
            <div class="text-4xl md:text-5xl font-bold mb-2 text-primary-100">25k+</div>
            <p class="text-primary-200">Active Users</p>
          </div>
          <div>
            <div class="text-4xl md:text-5xl font-bold mb-2 text-primary-100">$5M+</div>
            <p class="text-primary-200">Payments Processed</p>
          </div>
          <div>
            <div class="text-4xl md:text-5xl font-bold mb-2 text-primary-100">99.9%</div>
            <p class="text-primary-200">Uptime</p>
          </div>
          <div>
            <div class="text-4xl md:text-5xl font-bold mb-2 text-primary-100">4.9/5</div>
            <p class="text-primary-200">Customer Satisfaction</p>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Enhanced CTA Section -->
    <section class="py-24 bg-gradient-to-r from-secondary-600 to-secondary-800 text-white relative overflow-hidden">
      <!-- Background decorative elements -->
      <div class="absolute top-0 left-0 w-full h-full opacity-10">
        <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg">
          <defs>
            <pattern id="smallDots" width="20" height="20" patternUnits="userSpaceOnUse">
              <circle cx="3" cy="3" r="1.5" fill="white" />
            </pattern>
          </defs>
          <rect width="100%" height="100%" fill="url(#smallDots)" />
        </svg>
      </div>
      
      <div class="container-custom relative z-10">
        <div class="max-w-3xl mx-auto text-center">
          <h2 class="text-3xl md:text-4xl lg:text-5xl font-bold mb-6">Ready to Take Control of Your Payments?</h2>
          <p class="text-xl mb-10 text-white/85">
            Join thousands of satisfied users who are already simplifying their payment management.
            Get started today and experience the difference!
          </p>
          <div class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-4 justify-center">
            <NuxtLink to="/auth/signup" class="btn bg-white text-secondary-700 hover:bg-secondary-50 focus:ring-white flex items-center justify-center group">
              <span>Create Free Account</span>
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2 transform group-hover:translate-x-1 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
              </svg>
            </NuxtLink>
            <NuxtLink to="/auth/login" class="btn bg-secondary-700 border border-white text-white hover:bg-secondary-800 focus:ring-white flex items-center justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 16l-4-4m0 0l4-4m-4 4h14m-5 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h7a3 3 0 013 3v1" />
              </svg>
              <span>Sign In</span>
            </NuxtLink>
          </div>
          
          <!-- Trust badges -->
          <div class="mt-12 flex flex-wrap justify-center gap-8">
            <div class="flex items-center bg-white/10 px-4 py-2 rounded-lg">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
              </svg>
              <span>SSL Secured</span>
            </div>
            <div class="flex items-center bg-white/10 px-4 py-2 rounded-lg">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
              </svg>
              <span>PCI Compliant</span>
            </div>
            <div class="flex items-center bg-white/10 px-4 py-2 rounded-lg">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
              </svg>
              <span>GDPR Ready</span>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
definePageMeta({
  layout: 'default',
});
</script>

<style scoped>
/* Modern styling for details/summary FAQ elements */
details {
  transition: all 0.3s ease;
}

details:hover {
  @apply bg-gray-50 rounded-lg px-4;
}

details[open] summary {
  @apply text-primary-600 mb-2;
}

/* Additional hover effects */
.btn {
  @apply py-3 px-6 rounded-lg font-medium transition-all duration-300 focus:outline-none focus:ring-2 focus:ring-offset-2;
}

.card {
  @apply bg-white rounded-xl p-8 shadow-md;
}

.shadow-raised {
  box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
}

.container-custom {
  @apply max-w-7xl mx-auto px-4 sm:px-6 lg:px-8;
}
</style>