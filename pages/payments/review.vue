<template>
  <div class="fade-in">
    <!-- Enhanced Header Section -->
    <div class="bg-white shadow">
      <div class="container-custom py-6">
        <div class="flex flex-col md:flex-row md:items-center md:justify-between">
          <div class="mb-4 md:mb-0">
            <div class="flex items-center">
              <NuxtLink to="/payments" class="mr-2 text-gray-500 hover:text-gray-700">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
                </svg>
              </NuxtLink>
              <h1 class="text-2xl font-bold text-gray-900">Review Payment</h1>
            </div>
            <p class="text-sm text-gray-600 mt-1">Review your payment details before proceeding</p>
          </div>
          <div class="flex items-center">
            <span class="bg-blue-100 text-blue-800 text-xs px-2.5 py-1 rounded-full font-medium">
              Step 2 of 3
            </span>
          </div>
        </div>
      </div>
    </div>

    <div class="container-custom py-8">
      <!-- Payment Summary Card -->
      <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 mb-8">
        <div class="px-6 py-5 border-b border-gray-100">
          <h2 class="text-xl font-bold text-gray-900">Payment Summary</h2>
        </div>
        
        <div class="p-6">
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
            <div class="border-r border-gray-200 pr-6">
              <h3 class="text-md font-medium mb-4 text-gray-700">Selected Instalments</h3>
              <div class="space-y-4">
                <div v-for="(instalment, index) in selectedInstalments" :key="index" class="flex justify-between items-center pb-3 border-b border-gray-100">
                  <div>
                    <div class="flex items-center">
                      <div class="flex-shrink-0 h-8 w-8 rounded-full flex items-center justify-center mr-3"
                           :class="{
                             'bg-warning-100 text-warning-800': instalment.status === 'Due Soon',
                             'bg-error-100 text-error-800': instalment.status === 'Overdue',
                             'bg-gray-100 text-gray-800': instalment.status === 'Upcoming'
                           }">
                        <span class="text-xs font-medium">
                          {{ instalment.dueDate.split(' ')[0].substring(0, 3) }}
                        </span>
                      </div>
                      <div>
                        <p class="text-sm font-medium text-gray-900">{{ instalment.description }}</p>
                        <p class="text-xs text-gray-500">Due: {{ instalment.dueDate }}</p>
                      </div>
                    </div>
                  </div>
                  <div class="font-medium">${{ instalment.amount.toFixed(2) }}</div>
                </div>
              </div>
              
              <div class="mt-6 pt-4 border-t border-gray-200">
                <div class="flex justify-between mb-2">
                  <span class="text-gray-600">Number of Instalments:</span>
                  <span class="font-medium">{{ selectedInstalments.length }}</span>
                </div>
                <div class="flex justify-between mb-2">
                  <span class="text-gray-600">Subtotal:</span>
                  <span class="font-medium">${{ subtotal.toFixed(2) }}</span>
                </div>
                <div v-if="processingFee > 0" class="flex justify-between mb-2">
                  <span class="text-gray-600">Processing Fee:</span>
                  <span class="font-medium">${{ processingFee.toFixed(2) }}</span>
                </div>
                <div class="flex justify-between mt-3 pt-3 border-t border-gray-200">
                  <span class="text-gray-900 font-bold">Total Amount:</span>
                  <span class="font-bold text-lg text-gray-900">${{ totalAmount.toFixed(2) }}</span>
                </div>
              </div>
            </div>
            
            <div>
              <h3 class="text-md font-medium mb-4 text-gray-700">Payment Method</h3>
              <div class="space-y-4">
                <div v-for="(method, index) in paymentMethods" :key="index" 
                      class="relative border p-4 rounded-lg cursor-pointer"
                      :class="{ 'border-primary-500 bg-primary-50': selectedPaymentMethod === method.id, 'border-gray-200': selectedPaymentMethod !== method.id }"
                      @click="selectedPaymentMethod = method.id">
                  <div class="flex items-center">
                    <div class="h-8 w-8 flex items-center justify-center mr-3">
                      <img v-if="method.icon" :src="method.icon" class="h-6" :alt="method.name">
                      <span v-else class="h-6 w-6 rounded-full bg-gray-200 flex items-center justify-center text-xs">
                        {{ method.name[0] }}
                      </span>
                    </div>
                    <div class="flex-grow">
                      <h4 class="font-medium">{{ method.name }}</h4>
                      <p class="text-xs text-gray-500">{{ method.details }}</p>
                    </div>
                    <div class="flex-shrink-0">
                      <div class="h-5 w-5 rounded-full border-2"
                           :class="{ 'border-primary-500': selectedPaymentMethod === method.id, 'border-gray-300': selectedPaymentMethod !== method.id }">
                        <div v-if="selectedPaymentMethod === method.id" class="h-3 w-3 m-0.5 rounded-full bg-primary-500"></div>
                      </div>
                    </div>
                  </div>
                </div>
                
                <button @click="addNewPaymentMethod" class="w-full border border-dashed border-gray-300 p-3 rounded-lg text-center hover:bg-gray-50 transition-colors duration-150">
                  <div class="flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
                    </svg>
                    <span class="ml-2 text-sm font-medium text-gray-600">Add Payment Method</span>
                  </div>
                </button>
              </div>
            </div>
          </div>
          
          <!-- Payment Purpose Info -->
          <div class="border-t border-gray-200 pt-6 mt-4">
            <h3 class="text-md font-medium mb-4 text-gray-700">Payment Purpose</h3>
            <div class="bg-blue-50 p-4 rounded-lg">
              <div class="flex">
                <div class="flex-shrink-0">
                  <svg class="h-5 w-5 text-blue-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd" />
                  </svg>
                </div>
                <div class="ml-3">
                  <p class="text-sm text-blue-700">
                    This payment will be applied to your selected instalments and will help maintain your account in good standing. Regular payments contribute to a positive payment history.
                  </p>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Gateway Information -->
          <div class="border-t border-gray-200 pt-6 mt-6">
            <div class="bg-amber-50 p-4 rounded-lg">
              <div class="flex">
                <div class="flex-shrink-0">
                  <svg class="h-5 w-5 text-amber-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M8.257 3.099c.765-1.36 2.722-1.36 3.486 0l5.58 9.92c.75 1.334-.213 2.98-1.742 2.98H4.42c-1.53 0-2.493-1.646-1.743-2.98l5.58-9.92zM11 13a1 1 0 11-2 0 1 1 0 012 0zm-1-8a1 1 0 00-1 1v3a1 1 0 002 0V6a1 1 0 00-1-1z" clip-rule="evenodd" />
                  </svg>
                </div>
                <div class="ml-3">
                  <h3 class="text-sm font-medium text-amber-800">Important: External Payment Gateway</h3>
                  <div class="mt-2 text-sm text-amber-700">
                    <p>When you proceed with the payment, you will be redirected to a secure external payment gateway to complete your transaction. After completion, you will be automatically redirected back to the confirmation page.</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Contact Information Card -->
      <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 mb-8">
        <div class="px-6 py-5 border-b border-gray-100">
          <h2 class="text-xl font-bold text-gray-900">Contact Information</h2>
          <p class="text-sm text-gray-600 mt-1">We'll send payment confirmation to these contacts</p>
        </div>
        
        <div class="p-6">
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div class="flex items-center space-x-3">
              <div class="h-10 w-10 bg-gray-100 rounded-full flex items-center justify-center text-gray-500">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                </svg>
              </div>
              <div>
                <div class="flex items-center">
                  <p class="font-medium">{{ userEmail }}</p>
                  <span class="bg-success-100 text-success-800 text-xs px-2 py-0.5 rounded-full font-medium ml-2">Verified</span>
                </div>
                <p class="text-sm text-gray-500">Payment receipt will be sent to this email</p>
              </div>
            </div>
            
            <div class="flex items-center space-x-3">
              <div class="h-10 w-10 bg-gray-100 rounded-full flex items-center justify-center text-gray-500">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 18h.01M8 21h8a2 2 0 002-2V5a2 2 0 00-2-2H8a2 2 0 00-2 2v14a2 2 0 002 2z" />
                </svg>
              </div>
              <div>
                <div class="flex items-center">
                  <p class="font-medium">{{ userPhone }}</p>
                  <span class="bg-success-100 text-success-800 text-xs px-2 py-0.5 rounded-full font-medium ml-2">Verified</span>
                </div>
                <p class="text-sm text-gray-500">SMS notification will be sent to this number</p>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Actions -->
      <div class="flex flex-col-reverse sm:flex-row items-center justify-between">
        <NuxtLink to="/payments" class="btn-outline mt-3 sm:mt-0">
          Back to Payments
        </NuxtLink>
        
        <button 
          @click="proceedToPayment" 
          class="btn-primary w-full sm:w-auto"
          :disabled="!selectedPaymentMethod"
          :class="{'opacity-50 cursor-not-allowed': !selectedPaymentMethod}"
        >
          Proceed to Payment
        </button>
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
const selectedPaymentMethod = ref(1); // Default to first payment method

// Mock data for review page - would be passed from previous page or fetched from API
const selectedInstalments = ref([
  {
    id: 1,
    dueDate: 'May 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Due Soon',
    reference: 'INS-2025-0501',
    purpose: 'This payment covers your monthly loan instalment with principal and interest components. Timely payment keeps your loan in good standing.'
  },
  {
    id: 4,
    dueDate: 'April 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Overdue',
    reference: 'INS-2025-0401',
    purpose: 'This payment is now overdue. Please make your payment as soon as possible to avoid any additional late fees and negative impact on your credit history.'
  }
]);

// Mock payment methods
const paymentMethods = ref([
  {
    id: 1,
    name: 'Credit Card',
    details: 'Visa ending in 4242',
    icon: null
  },
  {
    id: 2,
    name: 'Bank Transfer',
    details: 'Direct bank transfer',
    icon: null
  },
  {
    id: 3,
    name: 'PayPal',
    details: 'Pay using your PayPal account',
    icon: null
  }
]);

// User contact information for confirmation
const userEmail = ref('john.doe@example.com');
const userPhone = ref('(123) 456-7890');

// Computed values
const subtotal = computed(() => {
  return selectedInstalments.value.reduce((total, instalment) => total + instalment.amount, 0);
});

const processingFee = computed(() => {
  // Calculate processing fee based on the payment method
  if (selectedPaymentMethod.value === 1) {
    return subtotal.value * 0.025; // 2.5% for credit card
  } else if (selectedPaymentMethod.value === 2) {
    return 0; // No fee for bank transfer
  } else if (selectedPaymentMethod.value === 3) {
    return subtotal.value * 0.03; // 3% for PayPal
  }
  return 0;
});

const totalAmount = computed(() => {
  return subtotal.value + processingFee.value;
});

// Method to handle adding a new payment method
const addNewPaymentMethod = () => {
  // This would open a modal/form to add a new payment method in a real application
  alert('This would open a form to add a new payment method in a real application');
};

// Method to proceed to external payment gateway
const proceedToPayment = () => {
  // In a real application, this would redirect to an external payment gateway
  // After payment, the user would be redirected back to the confirmation page
  
  // Simulating a redirect to the payment gateway and then to the confirmation page
  const loadingMessage = 'Redirecting to payment gateway...';
  alert(loadingMessage);
  
  // Simulate a successful payment and redirect to confirmation
  setTimeout(() => {
    router.push('/payments/confirmation?status=success');
  }, 1500);
};
</script>