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
        <div v-if="paymentStatus === 'success'" class="card text-center mb-8">
          <div class="inline-flex items-center justify-center w-16 h-16 rounded-full bg-success-100 text-success-600 mb-4">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
            </svg>
          </div>
          <h1 class="text-3xl font-bold text-gray-900 mb-2">Payment Successful!</h1>
          <p class="text-lg text-gray-600 mb-6">
            Your payment of ${{ totalAmount.toFixed(2) }} has been successfully processed.
          </p>
          <div class="bg-gray-50 rounded-lg p-4 inline-block">
            <p class="text-sm text-gray-600">Transaction Reference</p>
            <p class="text-lg font-bold text-gray-900">{{ transactionReference }}</p>
          </div>
          
          <!-- Notification Info -->
          <div class="mt-6 bg-green-50 border-l-4 border-green-400 p-4 rounded text-left">
            <div class="flex">
              <div class="flex-shrink-0">
                <svg class="h-5 w-5 text-green-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                  <path d="M2.003 5.884L10 9.882l7.997-3.998A2 2 0 0016 4H4a2 2 0 00-1.997 1.884z" />
                  <path d="M18 8.118l-8 4-8-4V14a2 2 0 002 2h12a2 2 0 002-2V8.118z" />
                </svg>
              </div>
              <div class="ml-3">
                <p class="text-sm text-green-700">
                  A payment confirmation has been sent to your email ({{ userEmail }}) and via SMS to {{ userPhone }}.
                </p>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Failure Message -->
        <div v-if="paymentStatus === 'failed'" class="card text-center mb-8">
          <div class="inline-flex items-center justify-center w-16 h-16 rounded-full bg-error-100 text-error-600 mb-4">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
            </svg>
          </div>
          <h1 class="text-3xl font-bold text-gray-900 mb-2">Payment Failed</h1>
          <p class="text-lg text-gray-600 mb-6">
            Your payment could not be processed. {{ failureReason }}
          </p>
          
          <div class="bg-error-50 rounded-lg p-4 inline-block mb-6">
            <p class="text-sm text-error-700">Error Code: {{ errorCode }}</p>
          </div>
          
          <div class="flex flex-col sm:flex-row items-center justify-center space-y-4 sm:space-y-0 sm:space-x-4">
            <button @click="retryPayment" class="btn-primary">
              Try Again
            </button>
            <button @click="changePaymentMethod" class="btn-outline">
              Change Payment Method
            </button>
          </div>
        </div>
        
        <!-- Payment Details -->
        <div v-if="paymentStatus === 'success'" class="card mb-8">
          <h2 class="text-xl font-bold mb-4">Payment Details</h2>
          
          <div class="space-y-4">
            <div class="flex justify-between pb-3 border-b border-gray-200">
              <span class="text-gray-600">Payment Date:</span>
              <span class="font-medium">{{ paymentDate }}</span>
            </div>
            <div class="flex justify-between pb-3 border-b border-gray-200">
              <span class="text-gray-600">Payment Method:</span>
              <span class="font-medium">{{ paymentMethod }}</span>
            </div>
            <div class="flex justify-between pb-3 border-b border-gray-200">
              <span class="text-gray-600">Amount Paid:</span>
              <span class="font-medium">${{ (totalAmount - processingFee).toFixed(2) }}</span>
            </div>
            <div class="flex justify-between pb-3 border-b border-gray-200">
              <span class="text-gray-600">Processing Fee:</span>
              <span class="font-medium">${{ processingFee.toFixed(2) }}</span>
            </div>
            <div class="flex justify-between font-bold">
              <span>Total:</span>
              <span>${{ totalAmount.toFixed(2) }}</span>
            </div>
          </div>
        </div>
        
        <!-- Paid Instalments -->
        <div v-if="paymentStatus === 'success'" class="card mb-8">
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
        
        <!-- Remaining Instalments -->
        <div v-if="paymentStatus === 'failed'" class="card mb-8">
          <div class="flex justify-between items-center mb-4">
            <h2 class="text-xl font-bold">Unpaid Instalments</h2>
            <span class="bg-warning-100 text-warning-800 px-3 py-1 rounded-full text-xs font-medium">
              Pending Payment
            </span>
          </div>
          
          <div class="overflow-x-auto">
            <table class="min-w-full divide-y divide-gray-200">
              <thead class="bg-gray-50">
                <tr>
                  <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                    Due Date
                  </th>
                  <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                    Description
                  </th>
                  <th scope="col" class="px-6 py-3 text-right text-xs font-medium text-gray-500 uppercase tracking-wider">
                    Amount
                  </th>
                </tr>
              </thead>
              <tbody class="bg-white divide-y divide-gray-200">
                <tr v-for="(instalment, index) in unpaidInstalments" :key="index">
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                    {{ instalment.dueDate }}
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                    {{ instalment.description }}
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900 text-right">
                    ${{ instalment.amount.toFixed(2) }}
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
        
        <!-- Action Buttons -->
        <div class="flex flex-col sm:flex-row justify-between space-y-4 sm:space-y-0">
          <button 
            v-if="paymentStatus === 'success'"
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
import { ref, computed } from 'vue';
import { useRouter } from 'vue-router';

definePageMeta({
  layout: 'default',
});

const router = useRouter();

// Payment status - would be determined by the response from payment gateway
// Options: 'success', 'failed'
const paymentStatus = ref('success'); // Default to success for demo

// Mock user data
const userEmail = ref('john.doe@example.com');
const userPhone = ref('+1 (555) 123-4567');

// Mock transaction details
const transactionReference = ref('TRX-2025-0423');
const paymentDate = ref('May 21, 2025, 14:30 PM');
const paymentMethod = ref('Credit Card (ending in 4242)');
const processingFee = ref(5.00);
const totalAmount = ref(505.00);
const errorCode = ref('ERR-4032');
const failureReason = ref('The transaction was declined by your card issuer. Please try a different payment method or contact your bank.');

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

// Mock unpaid instalments (shown on failure)
const unpaidInstalments = [
  {
    id: 1,
    dueDate: 'May 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Due Soon',
    reference: 'INS-2025-0501'
  },
  {
    id: 2,
    dueDate: 'June 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Upcoming',
    reference: 'INS-2025-0601'
  }
];

// Method to download receipt (just a placeholder in this demo)
const downloadReceipt = () => {
  alert('In a real application, this would download a PDF receipt.');
};

// Method to retry the payment
const retryPayment = () => {
  // In a real app, this would redirect back to the payment gateway
  router.push('/payments/review');
};

// Method to change payment method
const changePaymentMethod = () => {
  // In a real app, this would go back to the review page to change payment method
  router.push('/payments/review');
};

// For demonstration purposes, allow toggling between success and failure
// In a real app, this would be determined by the payment gateway response
if (import.meta.env.DEV) {
  setTimeout(() => {
    // Uncomment to test the failure state
    // paymentStatus.value = 'failed';
  }, 500);
}
</script>