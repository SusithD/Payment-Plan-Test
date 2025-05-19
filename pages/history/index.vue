<template>
  <div class="fade-in">
    <div class="bg-white shadow">
      <div class="container-custom py-6">
        <h1 class="text-2xl font-bold text-gray-900">Payment History</h1>
      </div>
    </div>
    
    <div class="container-custom py-8">
      <!-- Filter Controls -->
      <div class="card mb-8">
        <div class="flex flex-col md:flex-row md:items-end space-y-4 md:space-y-0 md:space-x-4">
          <div class="flex-1">
            <label for="date-range" class="form-label">Date Range</label>
            <select id="date-range" v-model="dateRange" class="form-input">
              <option value="all">All Time</option>
              <option value="last30">Last 30 Days</option>
              <option value="last90">Last 90 Days</option>
              <option value="last180">Last 180 Days</option>
              <option value="custom">Custom Range</option>
            </select>
          </div>
          
          <div v-if="dateRange === 'custom'" class="flex-1">
            <div class="grid grid-cols-2 gap-3">
              <div>
                <label for="start-date" class="form-label">Start Date</label>
                <input type="date" id="start-date" v-model="startDate" class="form-input" />
              </div>
              <div>
                <label for="end-date" class="form-label">End Date</label>
                <input type="date" id="end-date" v-model="endDate" class="form-input" />
              </div>
            </div>
          </div>
          
          <div class="flex-1">
            <label for="payment-status" class="form-label">Payment Status</label>
            <select id="payment-status" v-model="paymentStatus" class="form-input">
              <option value="all">All Statuses</option>
              <option value="successful">Successful</option>
              <option value="pending">Pending</option>
              <option value="failed">Failed</option>
            </select>
          </div>
          
          <button @click="applyFilters" class="btn-primary h-10 md:self-end">
            Apply Filters
          </button>
        </div>
      </div>
      
      <!-- Payment History Table -->
      <div class="card">
        <div class="flex justify-between items-center mb-6">
          <h2 class="text-xl font-bold">Transactions</h2>
          <button @click="downloadHistory" class="btn-outline flex items-center space-x-2 text-sm py-1.5">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
            </svg>
            <span>Download</span>
          </button>
        </div>
        
        <div class="overflow-x-auto">
          <table class="min-w-full divide-y divide-gray-200">
            <thead class="bg-gray-50">
              <tr>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Date
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Transaction ID
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Description
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Amount
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Status
                </th>
                <th scope="col" class="px-6 py-3 text-right text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Action
                </th>
              </tr>
            </thead>
            <tbody class="bg-white divide-y divide-gray-200">
              <tr v-for="(transaction, index) in filteredTransactions" :key="index">
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                  {{ transaction.date }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                  {{ transaction.transactionId }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                  {{ transaction.description }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">
                  ${{ transaction.amount.toFixed(2) }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <span 
                    class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full" 
                    :class="{
                      'bg-success-100 text-success-800': transaction.status === 'Successful',
                      'bg-warning-100 text-warning-800': transaction.status === 'Pending',
                      'bg-error-100 text-error-800': transaction.status === 'Failed'
                    }"
                  >
                    {{ transaction.status }}
                  </span>
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                  <button 
                    @click="viewReceipt(transaction)" 
                    class="text-primary-600 hover:text-primary-900"
                    :disabled="transaction.status !== 'Successful'"
                    :class="{ 'opacity-50 cursor-not-allowed': transaction.status !== 'Successful' }"
                  >
                    View Receipt
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        
        <!-- Empty State -->
        <div v-if="filteredTransactions.length === 0" class="text-center py-12">
          <div class="inline-flex items-center justify-center w-16 h-16 rounded-full bg-gray-100 text-gray-400 mb-4">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
            </svg>
          </div>
          <h3 class="text-lg font-medium text-gray-900 mb-2">No transactions found</h3>
          <p class="text-gray-500">
            Try changing your filters or search criteria.
          </p>
        </div>
        
        <!-- Pagination -->
        <div v-if="filteredTransactions.length > 0" class="flex justify-between items-center mt-6">
          <div class="text-sm text-gray-700">
            Showing <span class="font-medium">1</span> to <span class="font-medium">{{ filteredTransactions.length }}</span> of <span class="font-medium">{{ filteredTransactions.length }}</span> results
          </div>
          <div class="flex space-x-2">
            <button class="btn-outline py-1 px-2 text-sm opacity-50 cursor-not-allowed">
              Previous
            </button>
            <button class="btn-outline py-1 px-2 text-sm bg-primary-50 text-primary-700 border-primary-300">
              1
            </button>
            <button class="btn-outline py-1 px-2 text-sm opacity-50 cursor-not-allowed">
              Next
            </button>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Receipt Modal -->
    <div 
      v-if="showReceiptModal" 
      class="fixed inset-0 bg-gray-900 bg-opacity-50 flex items-center justify-center z-50 fade-in"
    >
      <div class="bg-white rounded-xl p-6 shadow-xl w-full max-w-lg mx-4">
        <div class="flex justify-between items-center mb-4">
          <h3 class="text-lg font-bold">Payment Receipt</h3>
          <button @click="showReceiptModal = false" class="text-gray-400 hover:text-gray-500">
            <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
        
        <div class="border-t border-b border-gray-200 py-6 mb-6">
          <div class="text-center mb-6">
            <h4 class="text-xl font-bold mb-1">Payment Plan Portal</h4>
            <p class="text-sm text-gray-600">Transaction Receipt</p>
          </div>
          
          <div class="space-y-4">
            <div class="flex justify-between">
              <span class="text-gray-600">Transaction ID:</span>
              <span class="font-medium">{{ selectedTransaction.transactionId }}</span>
            </div>
            <div class="flex justify-between">
              <span class="text-gray-600">Date & Time:</span>
              <span class="font-medium">{{ selectedTransaction.date }}</span>
            </div>
            <div class="flex justify-between">
              <span class="text-gray-600">Payment Method:</span>
              <span class="font-medium">{{ selectedTransaction.paymentMethod }}</span>
            </div>
            <div class="flex justify-between">
              <span class="text-gray-600">Description:</span>
              <span class="font-medium">{{ selectedTransaction.description }}</span>
            </div>
            <div class="flex justify-between">
              <span class="text-gray-600">Amount:</span>
              <span class="font-bold">${{ selectedTransaction.amount?.toFixed(2) }}</span>
            </div>
            <div class="flex justify-between">
              <span class="text-gray-600">Status:</span>
              <span 
                class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full" 
                :class="{'bg-success-100 text-success-800': selectedTransaction.status === 'Successful'}"
              >
                {{ selectedTransaction.status }}
              </span>
            </div>
          </div>
        </div>
        
        <div class="mt-6 flex justify-end space-x-3">
          <button @click="downloadReceipt" class="btn-outline flex items-center space-x-2">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
            </svg>
            <span>Download Receipt</span>
          </button>
          <button @click="showReceiptModal = false" class="btn-primary">
            Close
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

definePageMeta({
  layout: 'default',
});

// Filter state
const dateRange = ref('all');
const startDate = ref('');
const endDate = ref('');
const paymentStatus = ref('all');

// Modal state
const showReceiptModal = ref(false);
const selectedTransaction = ref({});

// Mock transaction data
const transactions = ref([
  {
    date: 'April 15, 2025 10:23 AM',
    transactionId: 'TRX-25041501',
    description: 'Monthly Instalment Payment',
    amount: 250.00,
    status: 'Successful',
    paymentMethod: 'Credit Card (ending in 1234)'
  },
  {
    date: 'March 15, 2025 11:45 AM',
    transactionId: 'TRX-25031501',
    description: 'Monthly Instalment Payment',
    amount: 250.00,
    status: 'Successful',
    paymentMethod: 'Credit Card (ending in 1234)'
  },
  {
    date: 'February 15, 2025 09:30 AM',
    transactionId: 'TRX-25021501',
    description: 'Monthly Instalment Payment',
    amount: 250.00,
    status: 'Successful',
    paymentMethod: 'PayPal'
  },
  {
    date: 'January 17, 2025 03:15 PM',
    transactionId: 'TRX-25011701',
    description: 'Monthly Instalment Payment (Late)',
    amount: 250.00,
    status: 'Successful',
    paymentMethod: 'Bank Transfer'
  },
  {
    date: 'December 15, 2024 10:10 AM',
    transactionId: 'TRX-24121501',
    description: 'Monthly Instalment Payment',
    amount: 250.00,
    status: 'Successful',
    paymentMethod: 'Credit Card (ending in 1234)'
  }
]);

// Filtered transactions based on applied filters
const filteredTransactions = computed(() => {
  // In a real app, this would apply actual filtering logic
  // For demo purposes, we'll just return all transactions
  return transactions.value;
});

// Method to apply filters
const applyFilters = () => {
  // In a real app, this would update the filtered results
  // For demo purposes, we'll just show an alert
  alert('Filters applied. In a real application, this would filter the transactions based on your criteria.');
};

// Method to view receipt
const viewReceipt = (transaction) => {
  if (transaction.status === 'Successful') {
    selectedTransaction.value = transaction;
    showReceiptModal.value = true;
  }
};

// Method to download receipt
const downloadReceipt = () => {
  alert('In a real application, this would download a PDF receipt.');
};

// Method to download transaction history
const downloadHistory = () => {
  alert('In a real application, this would download a CSV or PDF of your transaction history.');
};
</script>