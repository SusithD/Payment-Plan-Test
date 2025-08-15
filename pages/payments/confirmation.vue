<template>
  <div class="fade-in">
    <!-- Enhanced Header Section with Status Banner -->
    <div v-if="status === 'success'" class="bg-success-500 text-white">
      <div class="container-custom py-3 px-4">
        <div class="flex items-center">
          <svg class="h-6 w-6 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
          <span class="font-medium">Payment successfully processed!</span>
        </div>
      </div>
    </div>
    
    <div v-if="status === 'error'" class="bg-error-500 text-white">
      <div class="container-custom py-3 px-4">
        <div class="flex items-center">
          <svg class="h-6 w-6 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
          <span class="font-medium">Payment failed. Please try again.</span>
        </div>
      </div>
    </div>

    <div class="bg-white shadow">
      <div class="container-custom py-6">
        <div class="flex flex-col md:flex-row md:items-center md:justify-between">
          <div class="mb-4 md:mb-0">
            <div class="flex items-center">
              <h1 class="text-2xl font-bold text-gray-900">Payment Confirmation</h1>
            </div>
            <p class="text-sm text-gray-600 mt-1">Your payment details and receipt</p>
          </div>
          <div class="flex items-center">
            <span class="bg-blue-100 text-blue-800 text-xs px-2.5 py-1 rounded-full font-medium">
              Step 3 of 3
            </span>
          </div>
        </div>
      </div>
    </div>

    <div class="container-custom py-8">
      <!-- Confirmation Card -->
      <div v-if="status === 'success'" class="mb-8 text-center">
        <div class="mx-auto bg-success-100 rounded-full h-24 w-24 flex items-center justify-center mb-6">
          <svg class="h-12 w-12 text-success-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
          </svg>
        </div>
        
        <h2 class="text-3xl font-bold text-gray-900 mb-2">Payment Successful!</h2>
        <p class="text-gray-600 max-w-md mx-auto">
          Your payment has been processed successfully. A confirmation has been sent to your email address and phone number.
        </p>
        
        <div class="mt-8 inline-flex items-center px-4 py-2 bg-gray-100 rounded-lg">
          <svg class="h-5 w-5 text-gray-500 mr-2" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M18 5v8a2 2 0 01-2 2h-5l-5 4v-4H4a2 2 0 01-2-2V5a2 2 0 012-2h12a2 2 0 012 2zM7 8H5v2h2V8zm2 0h2v2H9V8zm6 0h-2v2h2V8z" clip-rule="evenodd" />
          </svg>
          <span class="text-gray-600">Rate your payment experience</span>
          <div class="ml-2 flex">
            <button v-for="i in 5" :key="i" class="text-gray-300 hover:text-yellow-500 focus:text-yellow-500 ml-1">
              <svg class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
            </button>
          </div>
        </div>
      </div>
      
      <div v-if="status === 'error'" class="mb-8 text-center">
        <div class="mx-auto bg-error-100 rounded-full h-24 w-24 flex items-center justify-center mb-6">
          <svg class="h-12 w-12 text-error-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </div>
        
        <h2 class="text-3xl font-bold text-gray-900 mb-2">Payment Failed</h2>
        <p class="text-gray-600 max-w-md mx-auto">
          We couldn't process your payment. Please check your payment details and try again.
        </p>
        
        <button @click="retryPayment" class="mt-6 btn-primary">
          Try Again
        </button>
      </div>
      
      <!-- Payment Details Card -->
      <div v-if="status === 'success'" class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 mb-8">
        <div class="px-6 py-5 border-b border-gray-100 flex justify-between items-center">
          <h2 class="text-xl font-bold text-gray-900">Payment Receipt</h2>
          <button @click="downloadReceipt" class="btn-outline-sm flex items-center">
            <svg class="h-4 w-4 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
            </svg>
            Download PDF
          </button>
        </div>
        
        <div class="p-6">
          <!-- Receipt Details -->
          <div class="mb-8 pb-6 border-b border-gray-100">
            <div class="flex flex-col sm:flex-row justify-between mb-6">
              <div>
                <h3 class="text-sm uppercase font-medium text-gray-500">Receipt No.</h3>
                <p class="font-medium text-gray-900">{{ receipt.id }}</p>
              </div>
              <div class="mt-4 sm:mt-0">
                <h3 class="text-sm uppercase font-medium text-gray-500">Date & Time</h3>
                <p class="font-medium text-gray-900">{{ receipt.date }}</p>
              </div>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
              <div>
                <h3 class="text-sm uppercase font-medium text-gray-500">Payment Method</h3>
                <div class="flex items-center mt-1">
                  <span class="h-8 w-8 bg-gray-100 rounded-full flex items-center justify-center mr-2">
                    <span class="text-xs font-semibold">{{ receipt.paymentMethod[0] }}</span>
                  </span>
                  <span class="font-medium text-gray-900">{{ receipt.paymentMethod }}</span>
                </div>
              </div>
              
              <div>
                <h3 class="text-sm uppercase font-medium text-gray-500">Status</h3>
                <div class="mt-1">
                  <span class="bg-success-100 text-success-800 text-xs px-2.5 py-1 rounded-full font-medium">
                    {{ receipt.status }}
                  </span>
                </div>
              </div>
              
              <div>
                <h3 class="text-sm uppercase font-medium text-gray-500">Transaction ID</h3>
                <p class="font-medium text-gray-900">{{ receipt.transactionId }}</p>
              </div>
            </div>
          </div>
          
          <!-- Items Paid For -->
          <h3 class="font-medium text-gray-900 mb-4">Items Paid</h3>
          <div class="overflow-x-auto">
            <table class="min-w-full divide-y divide-gray-200">
              <thead>
                <tr>
                  <th class="px-6 py-3 bg-gray-50 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                    Description
                  </th>
                  <th class="px-6 py-3 bg-gray-50 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                    Due Date
                  </th>
                  <th class="px-6 py-3 bg-gray-50 text-right text-xs font-medium text-gray-500 uppercase tracking-wider">
                    Amount
                  </th>
                </tr>
              </thead>
              <tbody class="bg-white divide-y divide-gray-200">
                <tr v-for="(item, index) in receipt.items" :key="index">
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                    {{ item.description }}
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                    {{ item.dueDate }}
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900 text-right">
                    ${{ item.amount.toFixed(2) }}
                  </td>
                </tr>
              </tbody>
              <tfoot>
                <tr>
                  <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900" colspan="2">
                    Subtotal
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900 text-right">
                    ${{ receipt.subtotal.toFixed(2) }}
                  </td>
                </tr>
                <tr v-if="receipt.processingFee > 0">
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500" colspan="2">
                    Processing Fee ({{ receipt.processingFeePercentage }}%)
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500 text-right">
                    ${{ receipt.processingFee.toFixed(2) }}
                  </td>
                </tr>
                <tr>
                  <td class="px-6 py-4 whitespace-nowrap text-base font-bold text-gray-900" colspan="2">
                    Total
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-base font-bold text-gray-900 text-right">
                    ${{ receipt.total.toFixed(2) }}
                  </td>
                </tr>
              </tfoot>
            </table>
          </div>
        </div>
      </div>
      
      <!-- Next Payment Details Card -->
      <div v-if="status === 'success'" class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 mb-8">
        <div class="px-6 py-5 border-b border-gray-100">
          <h2 class="text-xl font-bold text-gray-900">Next Payment Details</h2>
        </div>
        
        <div class="p-6">
          <div class="bg-gradient-to-r from-primary-50 to-blue-50 p-6 rounded-lg mb-6">
            <div class="flex items-center justify-between mb-4">
              <div>
                <h3 class="text-lg font-semibold text-gray-900">Upcoming Payment</h3>
                <p class="text-sm text-gray-600">Due on {{ nextPayment.dueDate }}</p>
              </div>
              <div class="text-right">
                <div class="text-2xl font-bold text-primary-600">${{ nextPayment.amount.toFixed(2) }}</div>
                <div class="text-sm text-gray-500">{{ nextPayment.daysUntilDue }} days remaining</div>
              </div>
            </div>
            
            <div class="flex items-center justify-between">
              <div class="flex items-center space-x-4">
                <div class="flex items-center space-x-2">
                  <div class="h-2 w-2 bg-warning-500 rounded-full"></div>
                  <span class="text-sm text-gray-600">Payment Status: {{ nextPayment.status }}</span>
                </div>
                <div class="flex items-center space-x-2">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                  </svg>
                  <span class="text-sm text-gray-600">{{ nextPayment.description }}</span>
                </div>
              </div>
              
              <button 
                @click="makeNextPayment" 
                class="btn-primary flex items-center space-x-2"
              >
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
                </svg>
                <span>Make Payment</span>
              </button>
            </div>
          </div>
          
          <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
            <div class="text-center p-4 border border-gray-100 rounded-lg">
              <div class="text-2xl font-bold text-success-600 mb-1">
                {{ paymentImpact.planProgress }}%
              </div>
              <p class="text-gray-500 text-sm">Plan Progress</p>
            </div>
            
            <div class="text-center p-4 border border-gray-100 rounded-lg">
              <div class="text-2xl font-bold text-primary-600 mb-1">
                ${{ paymentImpact.remainingBalance.toFixed(0) }}
              </div>
              <p class="text-gray-500 text-sm">Remaining Balance</p>
            </div>
            
            <div class="text-center p-4 border border-gray-100 rounded-lg">
              <div class="text-2xl font-bold text-warning-600 mb-1">
                {{ nextPayment.daysUntilDue }}
              </div>
              <p class="text-gray-500 text-sm">Days Until Due</p>
            </div>
          </div>
          
          <div class="mt-6 bg-blue-50 p-4 rounded-lg">
            <div class="flex">
              <div class="flex-shrink-0">
                <svg class="h-5 w-5 text-blue-400" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd" />
                </svg>
              </div>
              <div class="ml-3">
                <h3 class="text-sm font-medium text-blue-800">Stay on Track</h3>
                <div class="mt-2 text-sm text-blue-700">
                  <p>Make your next payment early to avoid late fees and maintain a good payment history. You can also set up automatic payments for convenience.</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Actions -->
      <div class="flex flex-col sm:flex-row items-center justify-between">
        <div class="flex flex-col sm:flex-row space-y-2 sm:space-y-0 sm:space-x-3">
          <NuxtLink to="/history" class="btn-outline">
            View Payment History
          </NuxtLink>
          <NuxtLink to="/payments" class="btn-outline">
            View All Payments
          </NuxtLink>
        </div>
        
        <div class="space-x-2 mt-3 sm:mt-0">
          <button v-if="status === 'error'" @click="retryPayment" class="btn-primary">
            Try Again
          </button>
          <div v-if="status === 'success'" class="flex space-x-2">
            <button @click="makeNextPayment" class="btn-primary flex items-center space-x-2">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
              </svg>
              <span>Make Next Payment</span>
            </button>
            <NuxtLink to="/dashboard" class="btn-outline">
              Go to Dashboard
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import { useRouter, useRoute } from 'vue-router';

definePageMeta({
  layout: 'default',
});

const router = useRouter();
const route = useRoute();
const status = ref('success'); // Default to success

// Mock receipt data
const receipt = ref({
  id: 'RCT-2025-0521-001',
  date: 'May 21, 2025 14:30:45',
  paymentMethod: 'Credit Card',
  status: 'Success',
  transactionId: 'TXN-12345-ABCDE',
  items: [
    {
      description: 'Monthly Instalment (May)',
      dueDate: 'May 15, 2025',
      amount: 250.00
    },
    {
      description: 'Monthly Instalment (April)',
      dueDate: 'April 15, 2025',
      amount: 250.00
    }
  ],
  subtotal: 500.00,
  processingFee: 12.50,
  processingFeePercentage: 2.5,
  total: 512.50
});

// Mock payment impact data
const paymentImpact = ref({
  planProgress: 45,
  remainingBalance: 1500,
  nextPaymentDate: 'Jun 15',
  nextPaymentAmount: 250
});

// Next payment details
const nextPayment = ref({
  id: 'payment_001',
  description: 'Monthly Instalment (June 2025)',
  dueDate: 'Jun 15, 2025',
  amount: 250.00,
  status: 'Due Soon',
  daysUntilDue: 25
});

onMounted(() => {
  // Check URL parameters for status
  if (route.query.status) {
    status.value = route.query.status;
  }
});

// Function to download a receipt (would be implemented properly in a real app)
const downloadReceipt = () => {
  alert('In a real app, this would generate and download a PDF receipt.');
};

// Function to retry a failed payment
const retryPayment = () => {
  router.push('/payments/review');
};

// Function to make the next payment
const makeNextPayment = () => {
  // Navigate to review page with the next payment details
  router.push({
    path: '/payments/review',
    query: {
      paymentId: nextPayment.value.id,
      amount: nextPayment.value.amount,
      description: nextPayment.value.description,
      dueDate: nextPayment.value.dueDate
    }
  });
};
</script>