<template>
  <div class="fade-in bg-gray-50 min-h-screen">
    <!-- Top Stats Bar -->
    <div class="bg-white shadow-sm">
      <div class="container-custom py-6">
        <div class="flex flex-wrap items-center justify-between">
          <div>
            <h1 class="text-xl font-bold text-gray-900">Payment History</h1>
            <div class="flex items-center">
              <span class="text-sm text-gray-600">Track and review all your past payments</span>
              <span class="mx-2 text-gray-300">•</span>
              <span class="text-sm text-gray-600">May 22, 2025</span>
            </div>
          </div>
          <div class="flex space-x-3">
            <button @click="downloadHistory" class="btn-outline flex items-center py-2 px-4 text-sm">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
              </svg>
              Download Statement
            </button>
            <NuxtLink to="/payments" class="btn-primary flex items-center py-2 px-4 text-sm">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
              </svg>
              Make Payment
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
    
    <div class="container-custom py-12">
      <!-- Main Grid Layout -->
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-10">
        <!-- Left Column - Summary Cards -->
        <div class="lg:col-span-1 space-y-10">
          <!-- Summary Card 1 -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="bg-gradient-to-r from-primary-500 to-primary-600 px-6 py-4">
              <div class="flex justify-between items-center">
                <h2 class="text-white font-bold text-lg">Total Payments</h2>
                <span class="bg-white bg-opacity-20 text-white text-xs px-2.5 py-1 rounded-full">
                  All Time
                </span>
              </div>
            </div>
            
            <div class="px-6 py-5">
              <div class="flex items-center justify-between mb-4">
                <div>
                  <span class="text-gray-500 text-sm">Amount Paid</span>
                  <p class="text-2xl font-bold text-gray-900">${{ totalPayments.toFixed(2) }}</p>
                </div>
                <div class="h-12 w-12 rounded-full bg-primary-100 flex items-center justify-center">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                </div>
              </div>
              
              <div class="pt-3 border-t border-gray-200">
                <div class="mb-1 flex justify-between text-sm">
                  <span class="text-gray-600">Success Rate:</span>
                  <span class="font-medium">{{ successRate }}%</span>
                </div>
                <div class="w-full bg-gray-200 rounded-full h-3">
                  <div class="bg-primary-500 h-3 rounded-full" :style="{ width: `${successRate}%` }"></div>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Summary Card 2 -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="px-6 py-5 border-b border-gray-100">
              <div class="flex justify-between items-center">
                <h2 class="font-bold text-lg text-gray-900">Payment Plan Progress</h2>
              </div>
            </div>
            
            <div class="p-6">
              <div class="flex justify-between mb-2">
                <div>
                  <span class="text-sm font-medium text-gray-700">Completion Progress</span>
                </div>
                <div>
                  <span class="text-sm font-medium text-primary-700">{{ paymentPlanProgress }}%</span>
                </div>
              </div>
              <div class="h-4 w-full bg-gray-200 rounded-full overflow-hidden">
                <div 
                  class="h-full bg-primary-600 rounded-full" 
                  :style="{ width: paymentPlanProgress + '%' }"
                ></div>
              </div>
              <div class="grid grid-cols-3 gap-4 mt-6">
                <div class="text-center px-4 py-3 bg-gray-50 rounded-lg">
                  <div class="text-sm text-gray-500 mb-1">Total Plan</div>
                  <div class="text-lg font-bold text-gray-900">$3,000.00</div>
                </div>
                <div class="text-center px-4 py-3 bg-gray-50 rounded-lg">
                  <div class="text-sm text-gray-500 mb-1">Paid</div>
                  <div class="text-lg font-bold text-primary-700">${{ totalPayments.toFixed(2) }}</div>
                </div>
                <div class="text-center px-4 py-3 bg-gray-50 rounded-lg">
                  <div class="text-sm text-gray-500 mb-1">Remaining</div>
                  <div class="text-lg font-bold text-warning-700">${{ (3000 - totalPayments).toFixed(2) }}</div>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Filter Card -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="px-6 py-5 border-b border-gray-100">
              <div class="flex justify-between items-center">
                <h2 class="font-bold text-lg text-gray-900">Filter Transactions</h2>
              </div>
            </div>
            
            <div class="p-6">
              <div class="space-y-4">
                <div>
                  <label for="date-range" class="block text-sm font-medium text-gray-700 mb-1">Date Range</label>
                  <select id="date-range" v-model="dateRange" class="form-input w-full">
                    <option value="all">All Time</option>
                    <option value="last30">Last 30 Days</option>
                    <option value="last90">Last 90 Days</option>
                    <option value="last180">Last 180 Days</option>
                    <option value="custom">Custom Range</option>
                  </select>
                </div>
                
                <div v-if="dateRange === 'custom'" class="grid grid-cols-2 gap-3">
                  <div>
                    <label for="start-date" class="block text-sm font-medium text-gray-700 mb-1">Start Date</label>
                    <input type="date" id="start-date" v-model="startDate" class="form-input w-full" />
                  </div>
                  <div>
                    <label for="end-date" class="block text-sm font-medium text-gray-700 mb-1">End Date</label>
                    <input type="date" id="end-date" v-model="endDate" class="form-input w-full" />
                  </div>
                </div>
                
                <div>
                  <label for="payment-status" class="block text-sm font-medium text-gray-700 mb-1">Payment Status</label>
                  <select id="payment-status" v-model="paymentStatus" class="form-input w-full">
                    <option value="all">All Statuses</option>
                    <option value="successful">Successful</option>
                    <option value="pending">Pending</option>
                    <option value="failed">Failed</option>
                  </select>
                </div>
                
                <div>
                  <label for="payment-method" class="block text-sm font-medium text-gray-700 mb-1">Payment Method</label>
                  <select id="payment-method" v-model="paymentMethod" class="form-input w-full">
                    <option value="all">All Methods</option>
                    <option value="credit">Credit Card</option>
                    <option value="bank">Bank Transfer</option>
                    <option value="paypal">PayPal</option>
                  </select>
                </div>
                
                <div class="flex space-x-3 pt-2">
                  <button @click="applyFilters" class="btn-primary flex-1">
                    Apply Filters
                  </button>
                  <button @click="resetFilters" class="btn-outline flex-1">
                    Reset
                  </button>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Next Payment Card -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="bg-gradient-to-r from-warning-500 to-warning-600 px-6 py-4">
              <div class="flex justify-between items-center">
                <h2 class="text-white font-bold text-lg">Next Payment Due</h2>
                <span class="bg-white bg-opacity-20 text-white text-xs px-2.5 py-1 rounded-full">
                  Reminder
                </span>
              </div>
            </div>
            
            <div class="px-6 py-5">
              <div class="flex items-center justify-between mb-4">
                <div>
                  <span class="text-gray-500 text-sm">Due Date</span>
                  <p class="text-xl font-bold text-gray-900">May 15, 2025</p>
                </div>
                <div class="h-12 w-12 rounded-full bg-warning-100 flex items-center justify-center">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-warning-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                </div>
              </div>
              
              <div class="pt-3 border-t border-gray-200">
                <div class="flex justify-between text-sm mb-2">
                  <span class="text-gray-600">Amount Due:</span>
                  <span class="font-bold">$250.00</span>
                </div>
                <div class="flex justify-between text-sm">
                  <span class="text-gray-600">Time Remaining:</span>
                  <span class="font-medium text-warning-600">{{ daysUntilNextPayment }} days</span>
                </div>
              </div>
              
              <div class="mt-4">
                <NuxtLink to="/payments" class="btn-primary w-full text-center py-2">
                  Make Payment
                </NuxtLink>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Right Column - Transaction History -->
        <div class="lg:col-span-2 space-y-10">
          <!-- Transaction History Card -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="px-6 py-5 border-b border-gray-100">
              <div class="flex justify-between items-center">
                <div>
                  <h2 class="font-bold text-lg text-gray-900">Transaction History</h2>
                  <p class="text-sm text-gray-500">Showing your payment history and transaction details</p>
                </div>
                
                <div class="relative">
                  <input 
                    type="text" 
                    v-model="searchQuery" 
                    placeholder="Search transactions..." 
                    class="block w-64 px-4 py-2 pl-9 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                    @input="searchTransactions"
                  />
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400 absolute left-2 top-1/2 transform -translate-y-1/2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                  </svg>
                </div>
              </div>
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
                      Payment Method
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
                  <tr v-for="(transaction, index) in filteredTransactions" :key="index" class="hover:bg-gray-50">
                    <td class="px-6 py-4 whitespace-nowrap">
                      <div class="flex items-center">
                        <div class="flex-shrink-0 h-8 w-8 bg-gray-100 rounded-full flex items-center justify-center mr-3">
                          <span class="text-xs font-medium">
                            {{ transaction.date.split(' ')[0].substring(0, 3) }}
                          </span>
                        </div>
                        <div>
                          <div class="text-sm text-gray-900">{{ transaction.date.split(' ')[0] }}</div>
                          <div class="text-xs text-gray-500">{{ transaction.date.split(' ').slice(1).join(' ') }}</div>
                        </div>
                      </div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                      <div class="text-sm text-gray-900">{{ transaction.transactionId }}</div>
                    </td>
                    <td class="px-6 py-4">
                      <div class="text-sm text-gray-900">{{ transaction.description }}</div>
                      <div v-if="transaction.notes" class="text-xs text-gray-500 mt-1">{{ transaction.notes }}</div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                      <div class="flex items-center">
                        <div class="flex-shrink-0 h-8 w-8 rounded-full bg-gray-100 flex items-center justify-center mr-2">
                          <svg v-if="transaction.paymentMethod.includes('Credit')" xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
                          </svg>
                          <svg v-else-if="transaction.paymentMethod.includes('Bank')" xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-gray-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 14v3m4-3v3m4-3v3M3 21h18M3 10h18M3 7l9-4 9 4M4 10h16v11H4V10z" />
                          </svg>
                          <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z" />
                          </svg>
                        </div>
                        <div class="text-sm text-gray-900">{{ transaction.paymentMethod }}</div>
                      </div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">
                      ${{ transaction.amount.toFixed(2) }}
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                      <span 
                        class="px-2 py-1 inline-flex text-xs leading-5 font-semibold rounded-full" 
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
                      <div class="flex space-x-3 justify-end">
                        <button 
                          @click="viewReceipt(transaction)" 
                          class="text-primary-600 hover:text-primary-900 flex items-center"
                          :disabled="transaction.status !== 'Successful'"
                          :class="{ 'opacity-50 cursor-not-allowed': transaction.status !== 'Successful' }"
                        >
                          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                          </svg>
                          Receipt
                        </button>
                        <button 
                          v-if="transaction.status === 'Failed'"
                          @click="retryPayment(transaction)" 
                          class="text-warning-600 hover:text-warning-900 flex items-center"
                        >
                          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
                          </svg>
                          Retry
                        </button>
                      </div>
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
              <p class="text-gray-500 max-w-md mx-auto">
                Try changing your filters or search criteria to view your payment history.
              </p>
              <button @click="resetFilters" class="mt-4 btn-primary">Reset All Filters</button>
            </div>
            
            <!-- Pagination -->
            <div v-if="filteredTransactions.length > 0" class="px-6 py-5 bg-gray-50 border-t border-gray-100 flex justify-between items-center">
              <div class="text-sm text-gray-700">
                Showing <span class="font-medium">1</span> to <span class="font-medium">{{ filteredTransactions.length }}</span> of <span class="font-medium">{{ transactions.length }}</span> results
              </div>
              <div class="flex space-x-3">
                <button class="btn-outline py-2 px-4 text-sm opacity-50 cursor-not-allowed">
                  Previous
                </button>
                <button class="btn-outline py-2 px-4 text-sm bg-primary-50 text-primary-700 border-primary-300">
                  1
                </button>
                <button class="btn-outline py-2 px-4 text-sm opacity-50 cursor-not-allowed">
                  Next
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Receipt Modal -->
    <div 
      v-if="showReceiptModal" 
      class="fixed inset-0 bg-gray-900 bg-opacity-50 flex items-center justify-center z-50 fade-in"
    >
      <div class="bg-white rounded-xl p-8 shadow-xl w-full max-w-lg mx-4">
        <div class="flex justify-between items-center mb-6">
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
            <div class="flex justify-between">
              <span class="text-gray-600">Reference Number:</span>
              <span class="font-medium">{{ selectedTransaction.referenceNumber || 'N/A' }}</span>
            </div>
            <div class="flex justify-between">
              <span class="text-gray-600">Billing Address:</span>
              <span class="font-medium text-right">
                {{ selectedTransaction.billingAddress || '123 Main St, Apt 4B, New York, NY 10001' }}
              </span>
            </div>
          </div>
        </div>
        
        <div class="mt-6 flex justify-end space-x-4">
          <button @click="printReceipt" class="btn-outline flex items-center space-x-2">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 17h2a2 2 0 002-2v-4a2 2 0 00-2-2H5a2 2 0 00-2 2v4a2 2 0 002 2h2m2 4h6a2 2 0 002-2v-4a2 2 0 00-2-2H9a2 2 0 00-2 2v4a2 2 0 002 2zm8-12V5a2 2 0 00-2-2H9a2 2 0 00-2 2v4h10z" />
            </svg>
            <span>Print</span>
          </button>
          <button @click="downloadReceipt" class="btn-outline flex items-center space-x-2">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
            </svg>
            <span>Download</span>
          </button>
          <button @click="showReceiptModal = false" class="btn-primary">
            Close
          </button>
        </div>
      </div>
    </div>
    
    <!-- Retry Payment Modal -->
    <div 
      v-if="showRetryModal" 
      class="fixed inset-0 bg-gray-900 bg-opacity-50 flex items-center justify-center z-50 fade-in"
    >
      <div class="bg-white rounded-xl p-8 shadow-xl w-full max-w-lg mx-4">
        <div class="flex justify-between items-center mb-6">
          <h3 class="text-lg font-bold">Retry Failed Payment</h3>
          <button @click="showRetryModal = false" class="text-gray-400 hover:text-gray-500">
            <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
        
        <div class="mb-6">
          <p class="text-gray-700 mb-4">
            You are about to retry the following failed payment:
          </p>
          
          <div class="bg-gray-50 p-5 rounded-lg mb-5">
            <div class="grid grid-cols-2 gap-3 text-sm">
              <div class="text-gray-600">Transaction ID:</div>
              <div class="font-medium">{{ retryTransaction.transactionId }}</div>
              
              <div class="text-gray-600">Date:</div>
              <div class="font-medium">{{ retryTransaction.date }}</div>
              
              <div class="text-gray-600">Description:</div>
              <div class="font-medium">{{ retryTransaction.description }}</div>
              
              <div class="text-gray-600">Amount:</div>
              <div class="font-medium">${{ retryTransaction.amount?.toFixed(2) }}</div>
            </div>
          </div>
          
          <div class="mb-5">
            <label class="form-label">Select Payment Method</label>
            <select v-model="retryPaymentMethod" class="form-input w-full">
              <option value="credit">Credit Card (ending in 1234)</option>
              <option value="bank">Bank Transfer</option>
              <option value="paypal">PayPal</option>
            </select>
          </div>
          
          <div class="bg-warning-50 border border-warning-200 rounded-lg p-4 text-sm text-warning-800">
            <div class="flex items-start">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
              <p>
                Your account will be charged immediately. Please ensure you have sufficient funds available.
              </p>
            </div>
          </div>
        </div>
        
        <div class="flex justify-end space-x-4">
          <button @click="showRetryModal = false" class="btn-outline">
            Cancel
          </button>
          <button @click="confirmRetryPayment" class="btn-primary">
            Retry Payment
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

definePageMeta({
  layout: 'default',
});

// Filter state
const dateRange = ref('all');
const startDate = ref('');
const endDate = ref('');
const paymentStatus = ref('all');
const paymentMethod = ref('all');
const amountRange = ref('all');
const searchQuery = ref('');

// Modal state
const showReceiptModal = ref(false);
const selectedTransaction = ref({});
const showRetryModal = ref(false);
const retryTransaction = ref({});
const retryPaymentMethod = ref('credit');

// Mock transaction data with added details
const transactions = ref([
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
    date: 'February 15, 2025 09:30 AM',
    transactionId: 'TRX-25021501',
    description: 'Monthly Instalment Payment',
    notes: 'Regular scheduled payment',
    amount: 250.00,
    status: 'Successful',
    paymentMethod: 'PayPal',
    referenceNumber: 'REF123456787',
    billingAddress: '123 Main St, Apt 4B, New York, NY 10001'
  },
  {
    date: 'January 17, 2025 03:15 PM',
    transactionId: 'TRX-25011701',
    description: 'Monthly Instalment Payment (Late)',
    notes: 'Payment received 2 days after due date',
    amount: 250.00,
    status: 'Successful',
    paymentMethod: 'Bank Transfer',
    referenceNumber: 'REF123456786',
    billingAddress: '123 Main St, Apt 4B, New York, NY 10001'
  },
  {
    date: 'December 15, 2024 10:10 AM',
    transactionId: 'TRX-24121501',
    description: 'Monthly Instalment Payment',
    notes: 'Regular scheduled payment',
    amount: 250.00,
    status: 'Successful',
    paymentMethod: 'Credit Card (ending in 1234)',
    referenceNumber: 'REF123456785',
    billingAddress: '123 Main St, Apt 4B, New York, NY 10001'
  },
  {
    date: 'November 15, 2024 10:33 AM',
    transactionId: 'TRX-24111501',
    description: 'Monthly Instalment Payment',
    notes: 'Regular scheduled payment',
    amount: 250.00,
    status: 'Successful',
    paymentMethod: 'Credit Card (ending in 1234)',
    referenceNumber: 'REF123456784',
    billingAddress: '123 Main St, Apt 4B, New York, NY 10001'
  },
  {
    date: 'October 15, 2024 11:05 AM',
    transactionId: 'TRX-24101501',
    description: 'Monthly Instalment Payment',
    notes: 'Regular scheduled payment',
    amount: 250.00,
    status: 'Successful',
    paymentMethod: 'Credit Card (ending in 1234)',
    referenceNumber: 'REF123456783',
    billingAddress: '123 Main St, Apt 4B, New York, NY 10001'
  },
  {
    date: 'September 15, 2024 09:45 AM',
    transactionId: 'TRX-24091501',
    description: 'Monthly Instalment Payment',
    amount: 250.00,
    status: 'Failed',
    paymentMethod: 'Credit Card (ending in 1234)',
    notes: 'Insufficient funds',
    referenceNumber: 'REF123456782',
    billingAddress: '123 Main St, Apt 4B, New York, NY 10001'
  }
]);

// Calculate total payments
const totalPayments = computed(() => {
  return transactions.value
    .filter(t => t.status === 'Successful')
    .reduce((sum, t) => sum + t.amount, 0);
});

// Calculate successful payments count
const successfulCount = computed(() => {
  return transactions.value.filter(t => t.status === 'Successful').length;
});

// Calculate success rate
const successRate = computed(() => {
  return Math.round((successfulCount.value / transactions.value.length) * 100);
});

// Calculate days until next payment
const daysUntilNextPayment = computed(() => {
  // Assuming next payment is on May 15, 2025
  const today = new Date('2025-05-22');
  const nextPayment = new Date(2025, 4, 15); // May is month 4 (0-indexed)
  const diffTime = nextPayment - today;
  const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
  return diffDays > 0 ? diffDays : 0;
});

// Calculate payment plan progress
const paymentPlanProgress = computed(() => {
  // Assuming total payment plan is $3,000
  const totalPlan = 3000;
  return Math.round((totalPayments.value / totalPlan) * 100);
});

// Filtered transactions based on filters
const filteredTransactions = computed(() => {
  let result = [...transactions.value];
  
  // Apply status filter
  if (paymentStatus.value !== 'all') {
    const statusMap = {
      'successful': 'Successful',
      'pending': 'Pending',
      'failed': 'Failed'
    };
    result = result.filter(t => t.status === statusMap[paymentStatus.value]);
  }
  
  // Apply payment method filter
  if (paymentMethod.value !== 'all') {
    const methodMap = {
      'credit': 'Credit Card',
      'bank': 'Bank Transfer',
      'paypal': 'PayPal'
    };
    result = result.filter(t => t.paymentMethod.includes(methodMap[paymentMethod.value]));
  }
  
  // Apply date range filter
  if (dateRange.value !== 'all') {
    const today = new Date();
    let filterDate = new Date();
    
    if (dateRange.value === 'last30') {
      filterDate.setDate(today.getDate() - 30);
    } else if (dateRange.value === 'last90') {
      filterDate.setDate(today.getDate() - 90);
    } else if (dateRange.value === 'last180') {
      filterDate.setDate(today.getDate() - 180);
    } else if (dateRange.value === 'custom' && startDate.value && endDate.value) {
      const start = new Date(startDate.value);
      const end = new Date(endDate.value);
      result = result.filter(t => {
        const txDate = new Date(t.date);
        return txDate >= start && txDate <= end;
      });
      return result;
    }
    
    result = result.filter(t => {
      const txDate = new Date(t.date);
      return txDate >= filterDate;
    });
  }
  
  // Apply search query filter
  if (searchQuery.value) {
    const query = searchQuery.value.toLowerCase();
    result = result.filter(t => 
      t.transactionId.toLowerCase().includes(query) ||
      t.description.toLowerCase().includes(query) ||
      t.paymentMethod.toLowerCase().includes(query) ||
      (t.notes && t.notes.toLowerCase().includes(query))
    );
  }
  
  return result;
});

// Methods
const viewReceipt = (transaction) => {
  selectedTransaction.value = transaction;
  showReceiptModal.value = true;
};

const printReceipt = () => {
  // Implement print functionality
  window.print();
};

const downloadReceipt = () => {
  // Implement download functionality
  alert('Receipt download started');
};

const downloadHistory = () => {
  // Implement download history functionality
  alert('Statement download started');
};

const retryPayment = (transaction) => {
  retryTransaction.value = transaction;
  showRetryModal.value = true;
};

const confirmRetryPayment = () => {
  // Implement retry payment logic here
  alert(`Payment retry initiated for transaction ${retryTransaction.value.transactionId}`);
  showRetryModal.value = false;
  
  // Update the transaction status for demo purposes
  const index = transactions.value.findIndex(t => t.transactionId === retryTransaction.value.transactionId);
  if (index !== -1) {
    transactions.value[index].status = 'Pending';
    transactions.value[index].notes = 'Payment retry in progress';
  }
};

const applyFilters = () => {
  // Already implemented through computed properties
};

const resetFilters = () => {
  dateRange.value = 'all';
  startDate.value = '';
  endDate.value = '';
  paymentStatus.value = 'all';
  paymentMethod.value = 'all';
  searchQuery.value = '';
};

const searchTransactions = () => {
  // Already implemented through computed properties
};

// Lifecycle hooks
onMounted(() => {
  // Any initialization code
});
</script>

<style scoped>
.container-custom {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 1rem;
}

.btn-primary {
  @apply bg-primary-600 hover:bg-primary-700 text-white font-medium rounded-lg shadow-sm py-2 px-4;
}

.btn-outline {
  @apply border border-gray-300 bg-white text-gray-700 hover:bg-gray-50 font-medium rounded-lg shadow-sm py-2 px-4;
}

.form-input {
  @apply mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-primary-500 focus:ring-primary-500 sm:text-sm py-2 px-3;
}

.form-label {
  @apply block text-sm font-medium text-gray-700 mb-2;
}

.fade-in {
  animation: fadeIn 0.3s ease-in-out;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
</style>