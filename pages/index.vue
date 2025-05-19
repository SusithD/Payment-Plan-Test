<template>
  <div>
    <!-- Hero Section -->
    <section class="bg-gradient-to-r from-primary-600 to-primary-800 text-white">
      <div class="container-custom py-16 md:py-24">
        <div class="max-w-3xl">
          <h1 class="text-4xl md:text-5xl font-bold mb-6 text-white">
            Simplify Your Payment Plans
          </h1>
          <p class="text-xl text-primary-100 mb-8">
            Manage your instalments, make payments, and stay on top of your financial commitments with our secure and easy-to-use payment portal.
          </p>
          <div class="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-4">
            <NuxtLink to="/auth/signup" class="btn bg-white text-primary-700 hover:bg-primary-50 focus:ring-white">
              Create Account
            </NuxtLink>
            <NuxtLink to="/auth/login" class="btn bg-primary-700 text-white hover:bg-primary-800 focus:ring-white">
              Sign In
            </NuxtLink>
          </div>
        </div>
      </div>
    </section>

    <!-- Features -->
    <section class="py-16 bg-white">
      <div class="container-custom">
        <div class="text-center max-w-3xl mx-auto mb-16">
          <h2 class="text-3xl font-bold mb-4">Everything You Need to Manage Your Payments</h2>
          <p class="text-lg text-gray-600">
            Our platform offers a comprehensive suite of tools to help you manage your payment plans efficiently.
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div class="card hover:shadow-raised transition-shadow duration-300">
            <div class="h-12 w-12 bg-primary-100 text-primary-600 rounded-lg flex items-center justify-center mb-4">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-3 7h3m-3 4h3m-6-4h.01M9 16h.01" />
              </svg>
            </div>
            <h3 class="text-xl font-semibold mb-2">View Instalments</h3>
            <p class="text-gray-600">
              Easily view all your pending instalments, including due dates, amounts, and descriptions in one place.
            </p>
          </div>

          <div class="card hover:shadow-raised transition-shadow duration-300">
            <div class="h-12 w-12 bg-secondary-100 text-secondary-600 rounded-lg flex items-center justify-center mb-4">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
              </svg>
            </div>
            <h3 class="text-xl font-semibold mb-2">Secure Payments</h3>
            <p class="text-gray-600">
              Make secure payments using our integrated payment gateway with multiple payment methods.
            </p>
          </div>

          <div class="card hover:shadow-raised transition-shadow duration-300">
            <div class="h-12 w-12 bg-accent-100 text-accent-600 rounded-lg flex items-center justify-center mb-4">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
              </svg>
            </div>
            <h3 class="text-xl font-semibold mb-2">Payment History</h3>
            <p class="text-gray-600">
              Access your complete payment history with detailed transaction records and receipts.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- How It Works -->
    <section class="py-16 bg-gray-50">
      <div class="container-custom">
        <div class="text-center max-w-3xl mx-auto mb-16">
          <h2 class="text-3xl font-bold mb-4">How It Works</h2>
          <p class="text-lg text-gray-600">
            Our simple process makes managing your payments effortless
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
          <div class="text-center">
            <div class="h-16 w-16 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mb-4 mx-auto">
              <span class="text-xl font-bold">1</span>
            </div>
            <h3 class="text-xl font-semibold mb-2">Create an Account</h3>
            <p class="text-gray-600">
              Sign up with your email and set a secure password to get started.
            </p>
          </div>

          <div class="text-center">
            <div class="h-16 w-16 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mb-4 mx-auto">
              <span class="text-xl font-bold">2</span>
            </div>
            <h3 class="text-xl font-semibold mb-2">View Your Instalments</h3>
            <p class="text-gray-600">
              See all your pending instalments with details like due dates and amounts.
            </p>
          </div>

          <div class="text-center">
            <div class="h-16 w-16 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mb-4 mx-auto">
              <span class="text-xl font-bold">3</span>
            </div>
            <h3 class="text-xl font-semibold mb-2">Select Payments</h3>
            <p class="text-gray-600">
              Choose which instalments you want to pay and proceed to checkout.
            </p>
          </div>

          <div class="text-center">
            <div class="h-16 w-16 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mb-4 mx-auto">
              <span class="text-xl font-bold">4</span>
            </div>
            <h3 class="text-xl font-semibold mb-2">Complete Payment</h3>
            <p class="text-gray-600">
              Pay securely using your preferred payment method and get instant confirmation.
            </p>
          </div>
        </div>
      </div>
    </section>
    
    <!-- CTA Section -->
    <section class="py-16 bg-gradient-to-r from-secondary-600 to-secondary-800 text-white">
      <div class="container-custom text-center">
        <h2 class="text-3xl font-bold mb-6">Ready to Manage Your Payments?</h2>
        <p class="text-xl mb-8 max-w-2xl mx-auto">
          Join thousands of users who are already simplifying their payment management.
        </p>
        <NuxtLink to="/auth/signup" class="btn bg-white text-secondary-700 hover:bg-secondary-50 focus:ring-white">
          Get Started Today
        </NuxtLink>
      </div>
    </section>
  </div>
</template>

<script setup>
definePageMeta({
  layout: 'default',
});
</script>