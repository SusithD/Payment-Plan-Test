<template>
  <div class="fade-in">
    <div class="container-custom py-12">
      <div class="max-w-3xl mx-auto">
        <!-- Steps Indicator -->
        <div class="flex justify-between mb-8">
          <div class="flex flex-col items-center">
            <div class="h-8 w-8 bg-primary-500 text-white rounded-full flex items-center justify-center">
              1
            </div>
            <span class="text-sm font-medium text-primary-700 mt-2">Select Instalments</span>
          </div>
          <div class="flex-1 flex items-center px-4">
            <div class="h-1 w-full bg-primary-500"></div>
          </div>
          <div class="flex flex-col items-center">
            <div class="h-8 w-8 bg-primary-500 text-white rounded-full flex items-center justify-center">
              2
            </div>
            <span class="text-sm font-medium text-primary-700 mt-2">Review Payment</span>
          </div>
          <div class="flex-1 flex items-center px-4">
            <div class="h-1 w-full bg-primary-500"></div>
          </div>
          <div class="flex flex-col items-center">
            <div class="h-8 w-8 bg-primary-500 text-white rounded-full flex items-center justify-center">
              3
            </div>
            <span class="text-sm font-medium text-primary-700 mt-2">Confirmation</span>
          </div>
        </div>
        
        <!-- Success Message -->
        <div class="card text-center mb-8">
          <div class="inline-flex items-center justify-center w-16 h-16 rounded-full bg-success-100 text-success-600 mb-4">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
            </svg>
          </div>
          <h1 class="text-3xl font-bold text-gray-900 mb-2">Payment Successful!</h1>
          <p class="text-lg text-gray-600 mb-6">
            Your payment of $505.00 has been successfully processed.
          </p>
          <div class="bg-gray-50 rounded-lg p-4 inline-block">
            <p class="text-sm text-gray-600">Transaction Reference</p>
            <p class="text-lg font-bold text-gray-900">TRX-25042312</p>
          </div>
        </div>
        
        <!-- Payment Details -->
        <div class="card mb-8">
          <h2 class="text-xl font-bold mb-4">Payment Details</h2>
          
          <div class="space-y-4">
            <div class="flex justify-between pb-3 border-b border-gray-200">
              <span class="text-gray-600">Payment Date:</span>
              <span class="font-medium">April 23, 2025, 14:30 PM</span>
            </div>
            <div class="flex justify-between pb-3 border-b border-gray-200">
              <span class="text-gray-600">Payment Method:</span>
              <span class="font-medium">Credit Card (ending in 1234)</span>
            </div>
            <div class="flex justify-between pb-3 border-b border-gray-200">
              <span class="text-gray-600">Amount Paid:</span>
              <span class="font-medium">$500.00</span>
            </div>
            <div class="flex justify-between pb-3 border-b border-gray-200">
              <span class="text-gray-600">Processing Fee:</span>
              <span class="font-medium">$5.00</span>
            </div>
            <div class="flex justify-between font-bold">
              <span>Total:</span>
              <span>$505.00</span>
            </div>
          </div>
        </div>
        
        <!-- Paid Instalments -->
        <div class="card mb-8">
          <h2 class="text-xl font-bold mb-4">Paid Instalments</h2>
          
          <div class="space-y-4">
            <div 
              v-for="(instalment, index) in paidInstalments" 
              :key="index"
              class="flex justify-between items-center p-3 border-b border-gray-200 last:border-b-0"
            >
              <div>
                <p class="font-medium">{{ instalment.description }}</p>
                <p class="text-sm text-gray-600">Due: {{ instalment.dueDate }}</p>
              </div>
              <div class="text-right">
                <p class="font-bold">${{ instalment.amount.toFixed(2) }}</p>
                <span class="inline-flex items-center px-2 py-0.5 rounded-full text-xs font-medium bg-success-100 text-success-800">
                  Paid
                </span>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Action Buttons -->
        <div class="flex flex-col sm:flex-row justify-between space-y-4 sm:space-y-0">
          <button 
            @click="downloadReceipt" 
            class="btn-outline flex items-center justify-center space-x-2"
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
            </svg>
            <span>Download Receipt</span>
          </button>
          <NuxtLink to="/dashboard" class="btn-primary">
            Back to Dashboard
          </NuxtLink>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  layout: 'default',
});

// Mock paid instalments data
const paidInstalments = [
  {
    id: 1,
    dueDate: 'May 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Paid',
    reference: 'INS-2025-0501'
  },
  {
    id: 2,
    dueDate: 'June 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Paid',
    reference: 'INS-2025-0601'
  }
];

// Method to download receipt (just a placeholder in this demo)
const downloadReceipt = () => {
  alert('In a real application, this would download a PDF receipt.');
};
</script>