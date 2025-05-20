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

    <!-- Features Section - Enhanced with interactive elements and modern design -->
    <section class="py-24 bg-gradient-to-br from-white to-gray-50 relative">
      <!-- Decorative background elements -->
      <div class="absolute top-0 left-0 w-full h-64 bg-gradient-to-r from-primary-50 to-transparent opacity-70"></div>
      <div class="absolute -top-10 right-10 w-40 h-40 bg-yellow-200 rounded-full opacity-20 blur-3xl"></div>
      <div class="absolute bottom-10 left-10 w-60 h-60 bg-primary-200 rounded-full opacity-20 blur-3xl"></div>
      
      <div class="container-custom relative z-10">
        <div class="text-center max-w-3xl mx-auto mb-16">
          <div class="inline-block mb-3">
            <span class="bg-primary-50 text-primary-700 font-semibold py-1.5 px-4 rounded-full relative overflow-hidden group">
              <span class="relative z-10 uppercase tracking-wider text-sm">POWERFUL FEATURES</span>
              <span class="absolute inset-0 bg-primary-100 transform scale-x-0 group-hover:scale-x-100 transition-transform origin-left duration-300"></span>
            </span>
          </div>
          <h2 class="text-3xl md:text-4xl font-bold mb-6 bg-clip-text text-transparent bg-gradient-to-r from-primary-700 to-primary-500">
            Everything You Need to Manage Your Payments
          </h2>
          <p class="text-lg text-gray-600 max-w-2xl mx-auto">
            Our platform offers a comprehensive suite of tools to help you manage your payment plans effectively and efficiently.
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-x-8 gap-y-12">
          <!-- Feature 1 - Hover interactive card -->
          <div class="bg-white rounded-2xl p-8 shadow-lg group hover:shadow-xl transition-all duration-300 relative overflow-hidden border border-gray-100">
            <div class="absolute w-full h-full bg-gradient-to-br from-primary-50 to-transparent -top-40 -right-40 rounded-full opacity-0 group-hover:opacity-100 transition-opacity duration-500"></div>
            
            <div class="h-16 w-16 rounded-2xl bg-gradient-to-br from-primary-500 to-primary-600 text-white flex items-center justify-center mb-6 transform group-hover:scale-110 group-hover:rotate-3 transition-transform relative z-10">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-3 7h3m-3 4h3m-6-4h.01M9 16h.01" />
              </svg>
            </div>
            
            <h3 class="text-2xl font-bold mb-4 relative z-10">View Instalments</h3>
            <p class="text-gray-600 mb-6 relative z-10">
              Easily view all your pending instalments, including due dates, amounts, and descriptions in one centralized dashboard.
            </p>
            
            <div class="relative z-10">
              <NuxtLink to="/dashboard" class="inline-flex items-center text-primary-600 font-semibold group/link">
                <span class="relative">
                  Explore Dashboard
                  <span class="absolute bottom-0 left-0 w-full h-0.5 bg-primary-600 transform scale-x-0 group-hover/link:scale-x-100 transition-transform origin-left"></span>
                </span>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2 transform group-hover/link:translate-x-1 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                </svg>
              </NuxtLink>
            </div>
          </div>

          <!-- Feature 2 - Hover interactive card -->
          <div class="bg-white rounded-2xl p-8 shadow-lg group hover:shadow-xl transition-all duration-300 relative overflow-hidden border border-gray-100">
            <div class="absolute w-full h-full bg-gradient-to-br from-secondary-50 to-transparent -top-40 -right-40 rounded-full opacity-0 group-hover:opacity-100 transition-opacity duration-500"></div>
            
            <div class="h-16 w-16 rounded-2xl bg-gradient-to-br from-secondary-500 to-secondary-600 text-white flex items-center justify-center mb-6 transform group-hover:scale-110 group-hover:rotate-3 transition-transform relative z-10">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z" />
              </svg>
            </div>
            
            <h3 class="text-2xl font-bold mb-4 relative z-10">Secure Payments</h3>
            <p class="text-gray-600 mb-6 relative z-10">
              Make secure payments using our bank-level encrypted gateway with multiple payment methods and instant verification.
            </p>
            
            <div class="relative z-10">
              <NuxtLink to="/payments" class="inline-flex items-center text-secondary-600 font-semibold group/link">
                <span class="relative">
                  Payment Options
                  <span class="absolute bottom-0 left-0 w-full h-0.5 bg-secondary-600 transform scale-x-0 group-hover/link:scale-x-100 transition-transform origin-left"></span>
                </span>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2 transform group-hover/link:translate-x-1 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                </svg>
              </NuxtLink>
            </div>
          </div>

          <!-- Feature 3 - Hover interactive card -->
          <div class="bg-white rounded-2xl p-8 shadow-lg group hover:shadow-xl transition-all duration-300 relative overflow-hidden border border-gray-100">
            <div class="absolute w-full h-full bg-gradient-to-br from-accent-50 to-transparent -top-40 -right-40 rounded-full opacity-0 group-hover:opacity-100 transition-opacity duration-500"></div>
            
            <div class="h-16 w-16 rounded-2xl bg-gradient-to-br from-accent-500 to-accent-600 text-white flex items-center justify-center mb-6 transform group-hover:scale-110 group-hover:rotate-3 transition-transform relative z-10">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
              </svg>
            </div>
            
            <h3 class="text-2xl font-bold mb-4 relative z-10">Payment History</h3>
            <p class="text-gray-600 mb-6 relative z-10">
              Access your complete payment history with detailed transaction records, downloadable receipts, and analytics.
            </p>
            
            <div class="relative z-10">
              <NuxtLink to="/history" class="inline-flex items-center text-accent-600 font-semibold group/link">
                <span class="relative">
                  View History
                  <span class="absolute bottom-0 left-0 w-full h-0.5 bg-accent-600 transform scale-x-0 group-hover/link:scale-x-100 transition-transform origin-left"></span>
                </span>
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2 transform group-hover/link:translate-x-1 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                </svg>
              </NuxtLink>
            </div>
          </div>
        </div>
        
        <!-- Additional Features Grid - Modern Interactive Elements -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mt-16">
          <div class="bg-gradient-to-br from-white to-primary-50 p-6 rounded-xl shadow-sm hover:shadow-md transition-all duration-300 flex items-start space-x-4">
            <div class="h-12 w-12 rounded-xl bg-primary-100 text-primary-700 flex items-center justify-center flex-shrink-0">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
              </svg>
            </div>
            <div>
              <h4 class="text-lg font-semibold mb-2">Payment Reminders</h4>
              <p class="text-gray-600">Get customized notifications and reminders before your payments are due.</p>
            </div>
          </div>
          
          <div class="bg-gradient-to-br from-white to-secondary-50 p-6 rounded-xl shadow-sm hover:shadow-md transition-all duration-300 flex items-start space-x-4">
            <div class="h-12 w-12 rounded-xl bg-secondary-100 text-secondary-700 flex items-center justify-center flex-shrink-0">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
              </svg>
            </div>
            <div>
              <h4 class="text-lg font-semibold mb-2">Bank-Level Security</h4>
              <p class="text-gray-600">Your financial data is encrypted with enterprise-grade security protocols.</p>
            </div>
          </div>
          
          <div class="bg-gradient-to-br from-white to-accent-50 p-6 rounded-xl shadow-sm hover:shadow-md transition-all duration-300 flex items-start space-x-4">
            <div class="h-12 w-12 rounded-xl bg-accent-100 text-accent-700 flex items-center justify-center flex-shrink-0">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
              </svg>
            </div>
            <div>
              <h4 class="text-lg font-semibold mb-2">Flexible Payment Options</h4>
              <p class="text-gray-600">Choose from multiple payment methods including credit/debit cards and digital wallets.</p>
            </div>
          </div>
          
          <div class="bg-gradient-to-br from-white to-gray-50 p-6 rounded-xl shadow-sm hover:shadow-md transition-all duration-300 flex items-start space-x-4">
            <div class="h-12 w-12 rounded-xl bg-gray-100 text-gray-700 flex items-center justify-center flex-shrink-0">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
            <div>
              <h4 class="text-lg font-semibold mb-2">24/7 Support</h4>
              <p class="text-gray-600">Access our dedicated customer support team anytime you need assistance.</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- How It Works Section - Enhanced with modern design and interactivity -->
    <section class="py-24 bg-white relative overflow-hidden">
      <!-- Decorative elements -->
      <div class="absolute top-0 right-0 w-1/3 h-1/3 bg-gradient-to-br from-primary-50 to-accent-50 opacity-50 rounded-bl-full animate-pulse"></div>
      <div class="absolute bottom-0 left-0 w-1/4 h-1/4 bg-gradient-to-tr from-secondary-50 to-primary-50 opacity-50 rounded-tr-full"></div>
      
      <!-- Enhanced decorative dots pattern -->
      <div class="absolute top-20 left-10 grid grid-cols-5 gap-4 opacity-20">
        <div v-for="i in 25" :key="i" class="h-2 w-2 rounded-full bg-primary-500"></div>
      </div>
      <div class="absolute bottom-20 right-10 grid grid-cols-5 gap-4 opacity-20">
        <div v-for="i in 25" :key="i" class="h-2 w-2 rounded-full bg-secondary-500"></div>
      </div>
      
      <div class="container-custom relative z-10">
        <div class="text-center max-w-3xl mx-auto mb-16">
          <div class="inline-block mb-3">
            <span class="bg-secondary-50 text-secondary-700 font-semibold py-1.5 px-4 rounded-full relative overflow-hidden group cursor-pointer transform hover:scale-105 transition-all">
              <span class="relative z-10 uppercase tracking-wider text-sm">HOW IT WORKS</span>
              <span class="absolute inset-0 bg-secondary-100 transform scale-x-0 group-hover:scale-x-100 transition-transform origin-left duration-300"></span>
            </span>
          </div>
          <h2 class="text-3xl md:text-4xl font-bold mb-6 bg-clip-text text-transparent bg-gradient-to-r from-secondary-700 to-secondary-500">
            Simple Process, Powerful Results
          </h2>
          <p class="text-lg text-gray-600 max-w-2xl mx-auto">
            Our streamlined payment process is designed to be intuitive and efficient, helping you manage your instalments with ease in just three simple steps.
          </p>
        </div>

        <!-- Enhanced Process Timeline with Animation -->
        <div class="relative">
          <!-- Enhanced connection line with animation -->
          <div class="hidden md:block absolute top-1/2 left-0 right-0 h-2 bg-gradient-to-r from-primary-500 via-secondary-500 to-accent-500 transform -translate-y-1/2 rounded-full shadow-md"></div>
          
          <div class="grid grid-cols-1 md:grid-cols-3 gap-16 md:gap-8">
            <!-- Step 1 - Enhanced -->
            <div class="relative group">
              <div class="hidden md:flex absolute top-0 left-1/2 transform -translate-x-1/2 -translate-y-1/2 z-10">
                <div class="h-14 w-14 rounded-full bg-white shadow-lg flex items-center justify-center border-4 border-primary-500 group-hover:scale-125 transition-transform duration-300">
                  <span class="text-xl font-bold text-primary-700">1</span>
                </div>
              </div>
              
              <div class="bg-white rounded-2xl p-8 shadow-lg group-hover:shadow-xl transition-all duration-300 relative overflow-hidden md:mt-10 border border-gray-100 hover:border-primary-200 transform group-hover:-translate-y-2">
                <div class="absolute -bottom-20 -right-20 h-40 w-40 rounded-full bg-primary-50 opacity-0 group-hover:opacity-70 transition-opacity duration-500"></div>
                
                <div class="md:hidden flex justify-center mb-4">
                  <div class="h-12 w-12 rounded-full bg-white shadow-md flex items-center justify-center border-4 border-primary-500">
                    <span class="text-lg font-bold text-primary-700">1</span>
                  </div>
                </div>
                
                <div class="h-20 w-20 rounded-full bg-primary-50 text-primary-700 flex items-center justify-center mb-6 mx-auto group-hover:bg-primary-100 transition-colors duration-300 relative z-10">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                  </svg>
                </div>
                
                <h3 class="text-2xl font-bold mb-4 text-center relative z-10">Create Your Account</h3>
                <p class="text-gray-600 text-center mb-6 relative z-10">
                  Sign up in minutes with your email or social media account. Verify your identity securely to access your personalized payment dashboard.
                </p>
                
                <div class="flex justify-center relative z-10">
                  <NuxtLink to="/auth/signup" class="inline-flex items-center bg-primary-50 text-primary-700 py-3 px-6 rounded-lg font-medium hover:bg-primary-100 transition-all hover:shadow-md group/btn">
                    <span>Get Started</span>
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2 transform group-hover/btn:translate-x-1 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                    </svg>
                  </NuxtLink>
                </div>
              </div>
            </div>
            
            <!-- Step 2 - Enhanced -->
            <div class="relative group">
              <div class="hidden md:flex absolute top-0 left-1/2 transform -translate-x-1/2 -translate-y-1/2 z-10">
                <div class="h-14 w-14 rounded-full bg-white shadow-lg flex items-center justify-center border-4 border-secondary-500 group-hover:scale-125 transition-transform duration-300">
                  <span class="text-xl font-bold text-secondary-700">2</span>
                </div>
              </div>
              
              <div class="bg-white rounded-2xl p-8 shadow-lg group-hover:shadow-xl transition-all duration-300 relative overflow-hidden md:mt-10 border border-gray-100 hover:border-secondary-200 transform group-hover:-translate-y-2">
                <div class="absolute -bottom-20 -right-20 h-40 w-40 rounded-full bg-secondary-50 opacity-0 group-hover:opacity-70 transition-opacity duration-500"></div>
                
                <div class="md:hidden flex justify-center mb-4">
                  <div class="h-12 w-12 rounded-full bg-white shadow-md flex items-center justify-center border-4 border-secondary-500">
                    <span class="text-lg font-bold text-secondary-700">2</span>
                  </div>
                </div>
                
                <div class="h-20 w-20 rounded-full bg-secondary-50 text-secondary-700 flex items-center justify-center mb-6 mx-auto group-hover:bg-secondary-100 transition-colors duration-300 relative z-10">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10" />
                  </svg>
                </div>
                
                <h3 class="text-2xl font-bold mb-4 text-center relative z-10">Manage Your Instalments</h3>
                <p class="text-gray-600 text-center mb-6 relative z-10">
                  Access your comprehensive dashboard showing all upcoming payments, due dates, and balances. Set up custom notifications to never miss a payment.
                </p>
                
                <div class="flex justify-center relative z-10">
                  <NuxtLink to="/dashboard" class="inline-flex items-center bg-secondary-50 text-secondary-700 py-3 px-6 rounded-lg font-medium hover:bg-secondary-100 transition-all hover:shadow-md group/btn">
                    <span>View Dashboard Demo</span>
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2 transform group-hover/btn:translate-x-1 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                    </svg>
                  </NuxtLink>
                </div>
              </div>
            </div>
            
            <!-- Step 3 - Enhanced -->
            <div class="relative group">
              <div class="hidden md:flex absolute top-0 left-1/2 transform -translate-x-1/2 -translate-y-1/2 z-10">
                <div class="h-14 w-14 rounded-full bg-white shadow-lg flex items-center justify-center border-4 border-accent-500 group-hover:scale-125 transition-transform duration-300">
                  <span class="text-xl font-bold text-accent-700">3</span>
                </div>
              </div>
              
              <div class="bg-white rounded-2xl p-8 shadow-lg group-hover:shadow-xl transition-all duration-300 relative overflow-hidden md:mt-10 border border-gray-100 hover:border-accent-200 transform group-hover:-translate-y-2">
                <div class="absolute -bottom-20 -right-20 h-40 w-40 rounded-full bg-accent-50 opacity-0 group-hover:opacity-70 transition-opacity duration-500"></div>
                
                <div class="md:hidden flex justify-center mb-4">
                  <div class="h-12 w-12 rounded-full bg-white shadow-md flex items-center justify-center border-4 border-accent-500">
                    <span class="text-lg font-bold text-accent-700">3</span>
                  </div>
                </div>
                
                <div class="h-20 w-20 rounded-full bg-accent-50 text-accent-700 flex items-center justify-center mb-6 mx-auto group-hover:bg-accent-100 transition-colors duration-300 relative z-10">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                </div>
                
                <h3 class="text-2xl font-bold mb-4 text-center relative z-10">Make Secure Payments</h3>
                <p class="text-gray-600 text-center mb-6 relative z-10">
                  Choose your preferred payment method and make secure transactions with our bank-level encryption. Get instant receipts and track your payment history.
                </p>
                
                <div class="flex justify-center relative z-10">
                  <NuxtLink to="/payments" class="inline-flex items-center bg-accent-50 text-accent-700 py-3 px-6 rounded-lg font-medium hover:bg-accent-100 transition-all hover:shadow-md group/btn">
                    <span>Explore Payment Options</span>
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 ml-2 transform group-hover/btn:translate-x-1 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                    </svg>
                  </NuxtLink>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Added testimonial/stats section -->
        <div class="mt-24 bg-gradient-to-br from-gray-50 to-white rounded-2xl p-8 shadow-lg border border-gray-100">
          <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
            <div class="text-center p-6 hover:bg-white hover:shadow-md rounded-xl transition-all duration-300">
              <div class="text-4xl font-bold text-primary-600 mb-2">98%</div>
              <p class="text-gray-600">Customer Satisfaction</p>
            </div>
            <div class="text-center p-6 hover:bg-white hover:shadow-md rounded-xl transition-all duration-300">
              <div class="text-4xl font-bold text-secondary-600 mb-2">24/7</div>
              <p class="text-gray-600">Customer Support</p>
            </div>
            <div class="text-center p-6 hover:bg-white hover:shadow-md rounded-xl transition-all duration-300">
              <div class="text-4xl font-bold text-accent-600 mb-2">100%</div>
              <p class="text-gray-600">Secure Transactions</p>
            </div>
          </div>
          
          <div class="mt-8 text-center">
            <NuxtLink to="/auth/signup" class="btn bg-gradient-to-r from-primary-600 to-secondary-600 text-white hover:from-primary-700 hover:to-secondary-700 shadow-md hover:shadow-lg transition-all duration-300 transform hover:scale-105">
              Get Started Today
            </NuxtLink>
          </div>
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
              "Managing my instalments has never been easier. The dashboard gives me a clear overview of my payments, and the security features give me peace of mind."
            </p>
            <div class="flex items-center">
              <div class="w-12 h-12 bg-secondary-200 rounded-full flex items-center justify-center text-secondary-700 font-bold mr-4">JS</div>
              <div>
                <h4 class="font-semibold">Jane Smith</h4>
                <p class="text-sm text-gray-500">Customer since 2022</p>
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
              "The customer service is exceptional. Any time I've had a question, they've been quick to respond and incredibly helpful."
            </p>
            <div class="flex items-center">
              <div class="w-12 h-12 bg-accent-200 rounded-full flex items-center justify-center text-accent-700 font-bold mr-4">RJ</div>
              <div>
                <h4 class="font-semibold">Robert Johnson</h4>
                <p class="text-sm text-gray-500">Customer since 2024</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- FAQ Section -->
    <section class="py-16 bg-gray-50">
      <div class="container mx-auto px-4">
        <div class="text-center mb-12">
          <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">Frequently Asked Questions</h2>
          <p class="text-lg text-gray-600 max-w-2xl mx-auto">
            Get answers to common questions about our payment services and platform.
          </p>
        </div>
        
        <div class="max-w-3xl mx-auto">
          <div class="space-y-4">
            <div v-for="(faq, index) in faqs" :key="index" class="bg-white rounded-lg shadow-md overflow-hidden">
              <button 
                @click="toggleFaq(index)"
                class="flex items-center justify-between w-full p-5 text-left"
                :class="{'border-b border-gray-200': activeFaq === index}"
              >
                <span class="text-lg font-medium text-gray-900">{{ faq.question }}</span>
                <span class="ml-6 flex-shrink-0">
                  <svg 
                    class="w-6 h-6 text-indigo-600 transform transition-transform duration-200"
                    :class="{'rotate-180': activeFaq === index}"
                    xmlns="http://www.w3.org/2000/svg" 
                    viewBox="0 0 24 24" 
                    fill="none" 
                    stroke="currentColor" 
                    stroke-width="2" 
                    stroke-linecap="round" 
                    stroke-linejoin="round"
                  >
                    <polyline points="6 9 12 15 18 9"></polyline>
                  </svg>
                </span>
              </button>
              <div 
                v-show="activeFaq === index"
                class="p-5 bg-gray-50"
              >
                <p class="text-gray-700">{{ faq.answer }}</p>
              </div>
            </div>
          </div>
          
          <div class="mt-10 text-center">
            <p class="text-gray-600 mb-4">Still have questions?</p>
            <NuxtLink 
              to="/profile" 
              class="inline-flex items-center px-6 py-3 border border-transparent text-base font-medium rounded-md shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              Contact Support
            </NuxtLink>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Contact Section -->
    <section class="py-20 bg-gray-50">
      <div class="container-custom">
        <div class="grid md:grid-cols-2 gap-12 items-center">
          <div>
            <span class="text-primary-600 font-medium block mb-2">CONTACT US</span>
            <h2 class="text-3xl md:text-4xl font-bold mb-6">We're Here to Help</h2>
            <p class="text-lg text-gray-600 mb-10">
              Have questions about our payment platform? Our team is ready to assist you with any inquiries or support needs.
            </p>
            
            <div class="space-y-6">
              <div class="flex items-start space-x-4">
                <div class="bg-white p-3 rounded-lg shadow-sm">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                  </svg>
                </div>
                <div>
                  <h4 class="font-semibold text-gray-900 mb-1">Phone Support</h4>
                  <p class="text-gray-600">+1 (800) 123-4567</p>
                  <p class="text-sm text-gray-500 mt-1">Monday-Friday, 9am-5pm EST</p>
                </div>
              </div>
              
              <div class="flex items-start space-x-4">
                <div class="bg-white p-3 rounded-lg shadow-sm">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v14a2 2 0 002 2z" />
                  </svg>
                </div>
                <div>
                  <h4 class="font-semibold text-gray-900 mb-1">Email Support</h4>
                  <p class="text-gray-600">support@paymentportal.com</p>
                  <p class="text-sm text-gray-500 mt-1">We'll respond within 24 hours</p>
                </div>
              </div>
              
              <div class="flex items-start space-x-4">
                <div class="bg-white p-3 rounded-lg shadow-sm">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
                  </svg>
                </div>
                <div>
                  <h4 class="font-semibold text-gray-900 mb-1">Live Chat</h4>
                  <p class="text-gray-600">Available on our website</p>
                  <p class="text-sm text-gray-500 mt-1">24/7 instant support</p>
                </div>
              </div>
            </div>
          </div>
          
          <div>
            <div class="bg-white rounded-xl p-8 shadow-lg border border-gray-100">
              <h3 class="text-2xl font-bold mb-6">Send us a Message</h3>
              
              <form class="space-y-6">
                <div>
                  <label for="name" class="block text-sm font-medium text-gray-700 mb-1">Full Name</label>
                  <input type="text" id="name" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring focus:ring-primary-200 focus:border-primary-500 outline-none transition-colors" placeholder="Your name" />
                </div>
                
                <div>
                  <label for="email" class="block text-sm font-medium text-gray-700 mb-1">Email Address</label>
                  <input type="email" id="email" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring focus:ring-primary-200 focus:border-primary-500 outline-none transition-colors" placeholder="your@email.com" />
                </div>
                
                <div>
                  <label for="message" class="block text-sm font-medium text-gray-700 mb-1">Message</label>
                  <textarea id="message" rows="4" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring focus:ring-primary-200 focus:border-primary-500 outline-none transition-colors" placeholder="How can we help you?"></textarea>
                </div>
                
                <button type="submit" class="w-full bg-primary-600 hover:bg-primary-700 text-white font-medium py-3 px-6 rounded-lg transition-colors">
                  Send Message
                </button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>
    
  </div>
</template>

<script setup>
import { ref } from 'vue';

// FAQ data and functionality
const activeFaq = ref(null);
const faqs = ref([
  {
    question: "How secure are my payment details?",
    answer: "We use industry-standard encryption and security protocols to protect your payment information. All transactions are secured with SSL/TLS encryption, and we never store your complete credit card information on our servers."
  },
  {
    question: "What payment methods do you accept?",
    answer: "We accept all major credit and debit cards including Visa, MasterCard, American Express, and Discover. We also support digital wallets like Apple Pay, Google Pay, and PayPal for your convenience."
  },
  {
    question: "How quickly will my payment be processed?",
    answer: "Most payments are processed immediately. However, depending on your bank or payment provider, it might take 1-3 business days for the transaction to appear on your statement."
  },
  {
    question: "Can I get a refund if I'm not satisfied?",
    answer: "Yes, we offer a 30-day money-back guarantee if you're not completely satisfied with our services. Please contact our support team to initiate the refund process."
  },
  {
    question: "Do you offer recurring payment options?",
    answer: "Yes, you can set up automatic recurring payments for subscriptions or regular payments. You can manage your recurring payment settings from your dashboard at any time."
  },
  {
    question: "Is there a fee for using your payment service?",
    answer: "We charge a small processing fee of 2.5% for standard payments. For international transactions, an additional 1% foreign currency conversion fee may apply. Enterprise customers may qualify for custom pricing."
  }
]);

const toggleFaq = (index) => {
  activeFaq.value = activeFaq.value === index ? null : index;
};
</script>

<style scoped>
/* Add any component-specific styles here */
</style>