<template>
  <div class="fade-in">
    <div class="bg-white shadow">
      <div class="container-custom py-6">
        <h1 class="text-2xl font-bold text-gray-900">Review Payment</h1>
      </div>
    </div>
    
    <div class="container-custom py-8">
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
            <div class="h-1 w-full bg-gray-200"></div>
          </div>
          <div class="flex flex-col items-center">
            <div class="h-8 w-8 bg-gray-200 text-gray-600 rounded-full flex items-center justify-center">
              3
            </div>
            <span class="text-sm font-medium text-gray-500 mt-2">Confirmation</span>
          </div>
        </div>
        
        <!-- Selected Instalments -->
        <div class="card mb-6">
          <h2 class="text-xl font-bold mb-4">Selected Instalments</h2>
          
          <div class="overflow-x-auto mb-4">
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
                <tr v-for="(instalment, index) in selectedInstalments" :key="index">
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
              <tfoot class="bg-gray-50">
                <tr>
                  <td colspan="2" class="px-6 py-4 whitespace-nowrap text-sm font-bold text-gray-900 text-right">
                    Total:
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm font-bold text-gray-900 text-right">
                    ${{ totalAmount.toFixed(2) }}
                  </td>
                </tr>
              </tfoot>
            </table>
          </div>
          
          <div class="flex justify-end">
            <NuxtLink to="/payments" class="text-primary-600 hover:text-primary-700 text-sm font-medium">
              Edit Selection
            </NuxtLink>
          </div>
        </div>
        
        <!-- Payment Method Selection -->
        <div class="card mb-6">
          <h2 class="text-xl font-bold mb-4">Payment Method</h2>
          
          <div class="space-y-4">
            <div 
              v-for="(method, index) in paymentMethods" 
              :key="index"
              class="border rounded-lg p-4 cursor-pointer transition-colors"
              :class="{ 'border-primary-500 bg-primary-50': selectedPaymentMethod === method.id, 'border-gray-200 hover:border-primary-200': selectedPaymentMethod !== method.id }"
              @click="selectedPaymentMethod = method.id"
            >
              <div class="flex items-center">
                <div class="flex items-center justify-center h-6 w-6 mr-3">
                  <div class="h-4 w-4 rounded-full border-2 border-primary-500 flex items-center justify-center">
                    <div v-if="selectedPaymentMethod === method.id" class="h-2 w-2 rounded-full bg-primary-500"></div>
                  </div>
                </div>
                <div class="flex items-center flex-1">
                  <img :src="method.image" :alt="method.name" class="h-8 w-auto mr-3" />
                  <span class="font-medium">{{ method.name }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Payment Summary -->
        <div class="card bg-gray-50 mb-8">
          <h2 class="text-xl font-bold mb-4">Payment Summary</h2>
          
          <div class="space-y-3">
            <div class="flex justify-between">
              <span class="text-gray-600">Subtotal:</span>
              <span>${{ totalAmount.toFixed(2) }}</span>
            </div>
            <div class="flex justify-between">
              <span class="text-gray-600">Payment Processing Fee:</span>
              <span>${{ processingFee.toFixed(2) }}</span>
            </div>
            <div class="border-t border-gray-200 pt-3 flex justify-between font-bold">
              <span>Total to Pay:</span>
              <span>${{ (totalAmount + processingFee).toFixed(2) }}</span>
            </div>
          </div>
        </div>
        
        <div class="flex flex-col sm:flex-row justify-between space-y-4 sm:space-y-0">
          <NuxtLink to="/payments" class="btn-outline">
            Back to Instalments
          </NuxtLink>
          <button 
            @click="proceedToPayment" 
            class="btn-primary"
          >
            Proceed to Payment
          </button>
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
const selectedPaymentMethod = ref('card');

// Mock selected instalments - would come from state management in a real app
const selectedInstalments = ref([
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
]);

// Mock payment methods
const paymentMethods = [
  {
    id: 'card',
    name: 'Credit/Debit Card',
    image: 'https://cdn.pixabay.com/photo/2021/09/08/06/00/credit-card-6605864_640.png'
  },
  {
    id: 'paypal',
    name: 'PayPal',
    image: 'https://cdn.pixabay.com/photo/2015/05/26/09/37/paypal-784404_640.png'
  },
  {
    id: 'bank',
    name: 'Bank Transfer',
    image: 'https://cdn.pixabay.com/photo/2018/10/07/13/57/bank-3730590_640.png'
  }
];

// Computed values
const totalAmount = computed(() => {
  return selectedInstalments.value.reduce((sum, item) => sum + item.amount, 0);
});

const processingFee = computed(() => {
  // Simulated processing fee calculation
  return selectedPaymentMethod.value === 'card' ? 5.00 : 0;
});

// Method to proceed to payment
const proceedToPayment = () => {
  // In a real app, this would initiate the Mapco payment gateway integration
  // For now, just redirect to confirmation page
  router.push('/payments/confirmation');
};
</script>