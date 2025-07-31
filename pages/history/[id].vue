<template>
  <div class="fade-in bg-gray-50">
    <!-- Top Stats Bar -->
    <div class="bg-white shadow-sm">
      <div class="container-custom py-4">
        <div class="flex flex-wrap items-center justify-between">
          <div>
            <h1 class="text-xl font-bold text-gray-900">Transaction Details</h1>
            <div class="flex items-center">
              <span class="text-sm text-gray-600">View detailed information about this transaction</span>
              <span class="mx-2 text-gray-300">•</span>
              <span class="text-sm text-gray-600">{{ currentDate }}</span>
            </div>
          </div>
          <div class="flex space-x-3">
            <NuxtLink to="/history" class="btn-outline flex items-center py-1.5 px-3 text-sm">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" />
              </svg>
              Back to History
            </NuxtLink>
            <button @click="printReceipt" class="btn-primary flex items-center py-1.5 px-3 text-sm">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 17h2a2 2 0 002-2v-4a2 2 0 00-2-2H5a2 2 0 00-2 2v4a2 2 0 002 2h2m2 4h6a2 2 0 002-2v-4a2 2 0 00-2-2H9a2 2 0 00-2 2v4a2 2 0 002 2z" />
              </svg>
              Print Receipt
            </button>
          </div>
        </div>
      </div>
    </div>
    
    <div class="container-custom py-8">
      <!-- Loading State -->
      <div v-if="isLoading" class="flex justify-center items-center py-20">
        <div class="animate-spin rounded-full h-12 w-12 border-b-2 border-primary-600"></div>
      </div>
      
      <!-- Error State -->
      <div v-else-if="error" class="bg-error-50 border border-error-200 rounded-xl p-6 text-center">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12 text-error-500 mx-auto mb-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
        </svg>
        <h2 class="text-xl font-bold text-error-800 mb-2">Transaction Not Found</h2>
        <p class="text-error-600 mb-6">We couldn't find the transaction you're looking for. It may have been removed or the ID is incorrect.</p>
        <NuxtLink to="/history" class="btn-primary">Return to Transaction History</NuxtLink>
      </div>
      
      <!-- Transaction Details -->
      <div v-else class="space-y-8">
        <!-- Transaction Status Card -->
        <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
          <div class="px-6 py-5 border-b border-gray-100">
            <div class="flex justify-between items-center">
              <h2 class="font-bold text-lg text-gray-900">Transaction Status</h2>
              <span 
                class="px-3 py-1 inline-flex text-xs leading-5 font-semibold rounded-full" 
                :class="{
                  'bg-success-100 text-success-800': transaction.status === 'Successful',
                  'bg-warning-100 text-warning-800': transaction.status === 'Pending',
                  'bg-error-100 text-error-800': transaction.status === 'Failed'
                }"
              >
                {{ transaction.status }}
              </span>
            </div>
          </div>
          
          <div class="p-6">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div>
                <h3 class="text-sm font-medium text-gray-500 mb-1">Transaction ID</h3>
                <p class="text-base font-medium text-gray-900">{{ transaction.transactionId }}</p>
              </div>
              <div>
                <h3 class="text-sm font-medium text-gray-500 mb-1">Date & Time</h3>
                <p class="text-base font-medium text-gray-900">{{ transaction.date }}</p>
              </div>
              <div>
                <h3 class="text-sm font-medium text-gray-500 mb-1">Amount</h3>
                <p class="text-xl font-bold text-gray-900">${{ transaction.amount?.toFixed(2) }}</p>
              </div>
              <div>
                <h3 class="text-sm font-medium text-gray-500 mb-1">Reference Number</h3>
                <p class="text-base font-medium text-gray-900">{{ transaction.referenceNumber || 'N/A' }}</p>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Transaction Details Card -->
        <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
          <div class="px-6 py-5 border-b border-gray-100">
            <h2 class="font-bold text-lg text-gray-900">Payment Details</h2>
          </div>
          
          <div class="p-6">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div>
                <h3 class="text-sm font-medium text-gray-500 mb-1">Description</h3>
                <p class="text-base font-medium text-gray-900">{{ transaction.description }}</p>
                <p v-if="transaction.notes" class="text-sm text-gray-600 mt-1 italic">{{ transaction.notes }}</p>
              </div>
              <div>
                <h3 class="text-sm font-medium text-gray-500 mb-1">Payment Method</h3>
                <div class="flex items-center">
                  <div class="flex-shrink-0 h-8 w-8 rounded-full bg-gray-100 flex items-center justify-center mr-3">
                    <svg v-if="transaction.paymentMethod?.includes('Credit')" xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
                    </svg>
                    <svg v-else-if="transaction.paymentMethod?.includes('Bank')" xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-gray-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 14v3m4-3v3m4-3v3M3 21h18M3 10h18M3 7l9-4 9 4M4 10h16v11H4V10z" />
                    </svg>
                    <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z" />
                    </svg>
                  </div>
                  <div>
                    <p class="text-base font-medium text-gray-900">{{ transaction.paymentMethod?.split(' (')[0] }}</p>
                    <p v-if="transaction.paymentMethod?.includes('(')" class="text-sm text-gray-600">{{ transaction.paymentMethod?.split('(')[1] }}</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Billing Information Card -->
        <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
          <div class="px-6 py-5 border-b border-gray-100">
            <h2 class="font-bold text-lg text-gray-900">Billing Information</h2>
          </div>
          
          <div class="p-6">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div>
                <h3 class="text-sm font-medium text-gray-500 mb-1">Billing Address</h3>
                <p class="text-base font-medium text-gray-900">{{ transaction.billingAddress || 'N/A' }}</p>
              </div>
              <div>
                <h3 class="text-sm font-medium text-gray-500 mb-1">Account</h3>
                <p class="text-base font-medium text-gray-900">John Doe</p>
                <p class="text-sm text-gray-600">Account #: AC-12345678</p>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Action Buttons -->
        <div class="flex justify-end space-x-3">
          <button @click="downloadReceipt" class="btn-outline flex items-center space-x-2 py-2 px-4">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
            </svg>
            <span>Download Receipt</span>
          </button>
          <button v-if="transaction.status === 'Failed'" @click="retryPayment" class="btn-primary flex items-center space-x-2 py-2 px-4">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
            </svg>
            <span>Retry Payment</span>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import { useRoute } from 'vue-router';

definePageMeta({
  layout: 'default',
});

const route = useRoute();
const transactionId = computed(() => route.params.id);

// State
const isLoading = ref(true);
const error = ref(null);
const transaction = ref({});

// Current date
const currentDate = computed(() => {
  const date = new Date();
  return date.toLocaleDateString('en-US', { 
    year: 'numeric', 
    month: 'long', 
    day: 'numeric' 
  });
});

// Mock transaction data - in a real app, this would be fetched from an API
const mockTransactions = [
  {
    date: 'April 15, 2025 10:23 AM',
    transactionId: 'TRX-25041501',
    description: 'Monthly Instalment Payment',
    notes: 'Regular scheduled payment',
    amount: 250.00,
    status: 'Successful',
    paymentMethod: 'Credit Card (ending in 1234)',
    referenceNumber: 'REF123456789',
    billingAddress: '123 Main St, Apt 4B, New York, NY 10001'
  },
  {
    date: 'March 15, 2025 11:45 AM',
    transactionId: 'TRX-25031501',
    description: 'Monthly Instalment Payment',
    notes: 'Regular scheduled payment',
    amount: 250.00,
    status: 'Successful',
    paymentMethod: 'Credit Card (ending in 1234)',
    referenceNumber: 'REF123456788',
    billingAddress: '123 Main St, Apt 4B, New York, NY 10001'
  },
  {
    date: 'November 15, 2024 02:20 PM',
    transactionId: 'TRX-24111501',
    description: 'Monthly Instalment Payment',
    notes: 'Regular scheduled payment',
    amount: 250.00,
    status: 'Failed',
    paymentMethod: 'Credit Card (ending in 1234)',
    referenceNumber: null,
    billingAddress: '123 Main St, Apt 4B, New York, NY 10001'
  }
];

// Methods
const fetchTransaction = () => {
  isLoading.value = true;
  error.value = null;
  
  // Simulate API call
  setTimeout(() => {
    const found = mockTransactions.find(t => t.transactionId === transactionId.value);
    
    if (found) {
      transaction.value = found;
    } else {
      error.value = 'Transaction not found';
    }
    
    isLoading.value = false;
  }, 1000);
};

const printReceipt = () => {
  window.print();
};

const downloadReceipt = () => {
  console.log('Downloading receipt for transaction:', transactionId.value);
  // In a real app, this would generate and download a PDF
};

const retryPayment = () => {
  console.log('Retrying payment for transaction:', transactionId.value);
  // In a real app, this would navigate to a payment retry page or show a modal
};

// Lifecycle hooks
onMounted(() => {
  fetchTransaction();
});
</script>

<style scoped>
.container-custom {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 1rem;
}

.btn-primary {
  @apply bg-gradient-to-r from-[#2C4880] to-[#1e3563] hover:from-[#1e3563] hover:to-[#2C4880] text-white font-medium py-2 px-4 rounded-lg transition-all duration-200 shadow-sm hover:shadow-md;
}

.btn-outline {
  @apply border border-gray-300 text-gray-700 hover:text-gray-900 hover:border-gray-400 font-medium py-2 px-4 rounded-lg transition-all duration-200;
}

.fade-in {
  animation: fadeIn 0.5s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@media print {
  .btn-primary, .btn-outline {
    display: none;
  }
}
</style>