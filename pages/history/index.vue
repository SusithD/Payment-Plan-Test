<template>
  <div class="fade-in bg-gray-50">
    <!-- Top Stats Bar -->
    <div class="bg-white shadow-sm">
      <div class="container-custom py-4">
        <div class="flex flex-wrap items-center justify-between">
          <div>
            <h1 class="text-xl font-bold text-gray-900">Payment History</h1>
            <div class="flex items-center">
              <span class="text-sm text-gray-600">Track and review all your past payments</span>
              <span class="mx-2 text-gray-300">•</span>
              <span class="text-sm text-gray-600">May 27, 2025</span>
            </div>
          </div>
          <div class="flex space-x-3">
            <button @click="downloadHistory" class="btn-outline flex items-center py-1.5 px-3 text-sm">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
              </svg>
              Download Statement
            </button>
            <NuxtLink to="/payments" class="btn-primary flex items-center py-1.5 px-3 text-sm">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
              </svg>
              Make Payment
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
    
    <div class="container-custom py-8">
      <!-- Summary Stats Row -->
      <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-8">
        <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 p-6">
          <div class="flex items-center">
            <div class="flex-shrink-0">
              <div class="h-12 w-12 rounded-full bg-primary-100 flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
              </div>
            </div>
            <div class="ml-4">
              <div class="text-sm font-medium text-gray-500">Total Paid</div>
              <div class="text-2xl font-bold text-gray-900">${{ totalPayments.toFixed(2) }}</div>
            </div>
          </div>
        </div>

        <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 p-6">
          <div class="flex items-center">
            <div class="flex-shrink-0">
              <div class="h-12 w-12 rounded-full bg-success-100 flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-success-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
              </div>
            </div>
            <div class="ml-4">
              <div class="text-sm font-medium text-gray-500">Success Rate</div>
              <div class="text-2xl font-bold text-gray-900">{{ successRate }}%</div>
            </div>
          </div>
        </div>

        <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 p-6">
          <div class="flex items-center">
            <div class="flex-shrink-0">
              <div class="h-12 w-12 rounded-full bg-blue-100 flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z" />
                </svg>
              </div>
            </div>
            <div class="ml-4">
              <div class="text-sm font-medium text-gray-500">Plan Progress</div>
              <div class="text-2xl font-bold text-gray-900">{{ paymentPlanProgress }}%</div>
            </div>
          </div>
        </div>

        <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 p-6">
          <div class="flex items-center">
            <div class="flex-shrink-0">
              <div class="h-12 w-12 rounded-full bg-warning-100 flex items-center justify-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-warning-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
              </div>
            </div>
            <div class="ml-4">
              <div class="text-sm font-medium text-gray-500">Next Payment</div>
              <div class="text-lg font-bold text-gray-900">May 15, 2025</div>
              <div class="text-sm text-warning-600">{{ daysUntilNextPayment }} days left</div>
            </div>
          </div>
        </div>
      </div>

      <!-- Filters and Search Section -->
      <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 mb-8">
        <div class="px-6 py-4 border-b border-gray-100">
          <div class="flex justify-between items-center">
            <div>
              <h2 class="font-bold text-lg text-gray-900">Filter & Search Transactions</h2>
              <p class="text-sm text-gray-500 mt-1">
                Search across all your payment transactions and history
              </p>
            </div>
            <div class="flex items-center space-x-2">
              <NuxtLink 
                to="/search?q=payment history" 
                class="text-primary-600 hover:text-primary-700 text-sm font-medium inline-flex items-center"
              >
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                </svg>
                Advanced Search
              </NuxtLink>
              <button @click="resetFilters" class="text-sm text-gray-500 hover:text-gray-700 flex items-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
                </svg>
                Reset All
              </button>
            </div>
          </div>
        </div>
        
        <div class="p-6">
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 xl:grid-cols-6 gap-4 mb-6">
            <div class="lg:col-span-2">
              <label for="search" class="block text-sm font-medium text-gray-700 mb-1">Search Transactions</label>
              <div class="relative">
                <input 
                  type="text" 
                  id="search"
                  v-model="searchQuery" 
                  placeholder="Transaction ID, description..." 
                  class="form-input w-full pl-10"
                  @input="searchTransactions"
                />
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400 absolute left-3 top-1/2 transform -translate-y-1/2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                </svg>
              </div>
            </div>
            
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
            
            <div>
              <label for="payment-status" class="block text-sm font-medium text-gray-700 mb-1">Status</label>
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
            
            <div>
              <label for="amount-range" class="block text-sm font-medium text-gray-700 mb-1">Amount Range</label>
              <select id="amount-range" v-model="amountRange" class="form-input w-full">
                <option value="all">All Amounts</option>
                <option value="0-100">$0 - $100</option>
                <option value="100-250">$100 - $250</option>
                <option value="250-500">$250 - $500</option>
                <option value="500+">$500+</option>
              </select>
            </div>
          </div>
          
          <div v-if="dateRange === 'custom'" class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
            <div>
              <label for="start-date" class="block text-sm font-medium text-gray-700 mb-1">Start Date</label>
              <input type="date" id="start-date" v-model="startDate" class="form-input w-full" />
            </div>
            <div>
              <label for="end-date" class="block text-sm font-medium text-gray-700 mb-1">End Date</label>
              <input type="date" id="end-date" v-model="endDate" class="form-input w-full" />
            </div>
          </div>
          
          <!-- Filter Summary -->
          <div v-if="hasActiveFilters" class="bg-blue-50 border border-blue-200 rounded-lg p-4">
            <div class="flex items-center justify-between">
              <div class="flex items-center text-sm text-blue-800">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 4a1 1 0 011-1h16a1 1 0 011 1v2.586a1 1 0 01-.293.707l-6.414 6.414a1 1 0 00-.293.707V17l-4 4v-6.586a1 1 0 00-.293-.707L3.293 7.414A1 1 0 013 6.707V4z" />
                </svg>
                <span class="font-medium">
                  {{ filteredTransactions.length }} of {{ transactions.length }} transactions match your filters
                </span>
              </div>
              <button @click="resetFilters" class="text-blue-600 hover:text-blue-800 text-sm font-medium">
                Clear Filters
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- Transaction History Table -->
      <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
        <div class="px-6 py-5 border-b border-gray-100">
          <div class="flex justify-between items-center">
            <div>
              <h2 class="font-bold text-lg text-gray-900">Transaction History</h2>
              <p class="text-sm text-gray-500 mt-1">
                Complete record of all your payment transactions and their details
              </p>
            </div>
            
            <div class="flex items-center space-x-3">
              <div class="text-sm text-gray-500">
                Showing {{ filteredTransactions.length }} transactions
              </div>
              <button @click="exportTransactions" class="btn-outline py-2 px-3 text-sm flex items-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                </svg>
                Export CSV
              </button>
            </div>
          </div>
        </div>
        
        <div class="overflow-x-auto">
          <table class="min-w-full divide-y divide-gray-200">
            <thead class="bg-gray-50">
              <tr>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider cursor-pointer hover:bg-gray-100" @click="sortBy('date')">
                  <div class="flex items-center">
                    Date & Time
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16V4m0 0L3 8m4-4l4 4m6 0v12m0 0l4-4m-4 4l-4-4" />
                    </svg>
                  </div>
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Transaction Details
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Payment Method
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider cursor-pointer hover:bg-gray-100" @click="sortBy('amount')">
                  <div class="flex items-center">
                    Amount
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16V4m0 0L3 8m4-4l4 4m6 0v12m0 0l4-4m-4 4l-4-4" />
                    </svg>
                  </div>
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Status
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Reference
                </th>
                <th scope="col" class="px-6 py-3 text-right text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Actions
                </th>
              </tr>
            </thead>
            <tbody class="bg-white divide-y divide-gray-200">
              <tr v-for="(transaction, index) in paginatedTransactions" :key="index" class="hover:bg-gray-50 transition-colors">
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="flex items-center">
                    <div class="flex-shrink-0 h-10 w-10 bg-gray-100 rounded-lg flex items-center justify-center mr-3">
                      <span class="text-xs font-medium text-gray-600">
                        {{ transaction.date.split(' ')[0].substring(4, 7) }}
                      </span>
                    </div>
                    <div>
                      <div class="text-sm font-medium text-gray-900">{{ transaction.date.split(' ')[0] }}</div>
                      <div class="text-xs text-gray-500">{{ transaction.date.split(' ').slice(1, 3).join(' ') }}</div>
                    </div>
                  </div>
                </td>
                <td class="px-6 py-4">
                  <div class="text-sm font-medium text-gray-900">{{ transaction.description }}</div>
                  <div class="text-xs text-gray-600 mt-1">ID: {{ transaction.transactionId }}</div>
                  <div v-if="transaction.notes" class="text-xs text-gray-500 mt-1 italic">{{ transaction.notes }}</div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="flex items-center">
                    <div class="flex-shrink-0 h-8 w-8 rounded-full bg-gray-100 flex items-center justify-center mr-3">
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
                    <div>
                      <div class="text-sm font-medium text-gray-900">{{ transaction.paymentMethod.split(' (')[0] }}</div>
                      <div v-if="transaction.paymentMethod.includes('(')" class="text-xs text-gray-500">{{ transaction.paymentMethod.split('(')[1] }}</div>
                    </div>
                  </div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="text-lg font-bold text-gray-900">${{ transaction.amount.toFixed(2) }}</div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
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
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="text-sm text-gray-900">{{ transaction.referenceNumber || 'N/A' }}</div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                  <div class="flex space-x-2 justify-end">
                    <button 
                      @click="viewReceipt(transaction)" 
                      class="text-primary-600 hover:text-primary-900 p-1 rounded hover:bg-primary-50"
                      :disabled="transaction.status !== 'Successful'"
                      :class="{ 'opacity-50 cursor-not-allowed': transaction.status !== 'Successful' }"
                      title="View Receipt"
                    >
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                      </svg>
                    </button>
                    <NuxtLink 
                      v-if="transaction.status === 'Successful'"
                      :to="`/payments/invoices/${getInvoiceId(transaction)}`"
                      class="text-secondary-600 hover:text-secondary-900 p-1 rounded hover:bg-secondary-50"
                      title="View Invoice"
                    >
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                      </svg>
                    </NuxtLink>
                    <button 
                      v-if="transaction.status === 'Failed'"
                      @click="retryPayment(transaction)" 
                      class="text-warning-600 hover:text-warning-900 p-1 rounded hover:bg-warning-50"
                      title="Retry Payment"
                    >
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
                      </svg>
                    </button>
                    <button 
                      @click="viewTransactionDetails(transaction)" 
                      class="text-gray-600 hover:text-gray-900 p-1 rounded hover:bg-gray-50"
                      title="View Details"
                    >
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                      </svg>
                    </button>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        
        <!-- Empty State -->
        <div v-if="filteredTransactions.length === 0" class="text-center py-16">
          <div class="inline-flex items-center justify-center w-20 h-20 rounded-full bg-gray-100 text-gray-400 mb-6">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v10a2 2 0 002 2h8a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2" />
            </svg>
          </div>
          <h3 class="text-xl font-medium text-gray-900 mb-2">No transactions found</h3>
          <p class="text-gray-500 max-w-md mx-auto mb-6">
            We couldn't find any transactions that match your current filters. Try adjusting your search criteria or date range.
          </p>
          <button @click="resetFilters" class="btn-primary">Reset All Filters</button>
        </div>
        
        <!-- Pagination -->
        <div v-if="filteredTransactions.length > 0" class="px-6 py-4 bg-gray-50 border-t border-gray-100 flex justify-between items-center">
          <div class="text-sm text-gray-700">
            Showing <span class="font-medium">{{ startIndex + 1 }}</span> to <span class="font-medium">{{ endIndex }}</span> of <span class="font-medium">{{ filteredTransactions.length }}</span> results
          </div>
          <div class="flex items-center space-x-2">
            <button 
              @click="previousPage" 
              :disabled="currentPage === 1"
              class="btn-outline py-2 px-3 text-sm"
              :class="{ 'opacity-50 cursor-not-allowed': currentPage === 1 }"
            >
              Previous
            </button>
            
            <div class="flex space-x-1">
              <button 
                v-for="page in visiblePages" 
                :key="page"
                @click="goToPage(page)"
                class="px-3 py-2 text-sm rounded"
                :class="{
                  'bg-primary-600 text-white': page === currentPage,
                  'text-gray-700 hover:bg-gray-100': page !== currentPage
                }"
              >
                {{ page }}
              </button>
            </div>
            
            <button 
              @click="nextPage" 
              :disabled="currentPage === totalPages"
              class="btn-outline py-2 px-3 text-sm"
              :class="{ 'opacity-50 cursor-not-allowed': currentPage === totalPages }"
            >
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
        
        <div class="mt-6 flex justify-end space-x-3">
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
      <div class="bg-white rounded-xl p-6 shadow-xl w-full max-w-lg mx-4">
        <div class="flex justify-between items-center mb-4">
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
          
          <div class="bg-gray-50 p-4 rounded-lg mb-4">
            <div class="grid grid-cols-2 gap-2 text-sm">
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
          
          <div class="mb-4">
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
        
        <div class="flex justify-end space-x-3">
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
    date: 'November 15, 2024 02:20 PM',
    transactionId: 'TRX-24111501',
    description: 'Monthly Instalment Payment',
    notes: 'Regular scheduled payment',
    amount: 250.00,
    status: 'Failed',
    paymentMethod: 'Credit Card (ending in 1234)',
    referenceNumber: null,
    billingAddress: '123 Main St, Apt 4B, New York, NY 10001'
  },
  {
    date: 'October 15, 2024 01:30 PM',
    transactionId: 'TRX-24101501',
    description: 'Monthly Instalment Payment',
    notes: 'Regular scheduled payment',
    amount: 250.00,
    status: 'Successful',
    paymentMethod: 'Bank Transfer',
    referenceNumber: 'REF123456784',
    billingAddress: '123 Main St, Apt 4B, New York, NY 10001'
  },
  {
    date: 'September 15, 2024 12:15 PM',
    transactionId: 'TRX-24091501',
    description: 'Initial Setup Payment',
    notes: 'First payment to establish payment plan',
    amount: 500.00,
    status: 'Successful',
    paymentMethod: 'Credit Card (ending in 1234)',
    referenceNumber: 'REF123456783',
    billingAddress: '123 Main St, Apt 4B, New York, NY 10001'
  },
  {
    date: 'August 28, 2024 04:45 PM',
    transactionId: 'TRX-24082801',
    description: 'Payment Plan Setup Fee',
    notes: 'One-time administrative fee',
    amount: 50.00,
    status: 'Successful',
    paymentMethod: 'PayPal',
    referenceNumber: 'REF123456782',
    billingAddress: '123 Main St, Apt 4B, New York, NY 10001'
  },
  {
    date: 'May 10, 2025 09:15 AM',
    transactionId: 'TRX-25051001',
    description: 'Pending Monthly Payment',
    notes: 'Payment processing',
    amount: 250.00,
    status: 'Pending',
    paymentMethod: 'Credit Card (ending in 1234)',
    referenceNumber: null,
    billingAddress: '123 Main St, Apt 4B, New York, NY 10001'
  }
]);

// Pagination state
const currentPage = ref(1);
const itemsPerPage = ref(10);
const sortField = ref('date');
const sortOrder = ref('desc');

// Computed properties
const totalPayments = computed(() => {
  return transactions.value
    .filter(t => t.status === 'Successful')
    .reduce((sum, t) => sum + t.amount, 0);
});

const successRate = computed(() => {
  const total = transactions.value.length;
  const successful = transactions.value.filter(t => t.status === 'Successful').length;
  return total > 0 ? Math.round((successful / total) * 100) : 0;
});

const paymentPlanProgress = computed(() => {
  // Assuming a total plan amount of $5000
  const totalPlanAmount = 5000;
  const paidAmount = totalPayments.value;
  return Math.min(Math.round((paidAmount / totalPlanAmount) * 100), 100);
});

const daysUntilNextPayment = computed(() => {
  const nextPaymentDate = new Date('2025-06-15');
  const today = new Date();
  const diffTime = nextPaymentDate - today;
  const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
  return Math.max(diffDays, 0);
});

const filteredTransactions = computed(() => {
  let filtered = [...transactions.value];

  // Apply search filter
  if (searchQuery.value) {
    const query = searchQuery.value.toLowerCase();
    filtered = filtered.filter(t =>
      t.transactionId.toLowerCase().includes(query) ||
      t.description.toLowerCase().includes(query) ||
      (t.notes && t.notes.toLowerCase().includes(query))
    );
  }

  // Apply status filter
  if (paymentStatus.value !== 'all') {
    const statusMap = {
      'successful': 'Successful',
      'pending': 'Pending',
      'failed': 'Failed'
    };
    filtered = filtered.filter(t => t.status === statusMap[paymentStatus.value]);
  }

  // Apply payment method filter
  if (paymentMethod.value !== 'all') {
    const methodMap = {
      'credit': 'Credit Card',
      'bank': 'Bank Transfer',
      'paypal': 'PayPal'
    };
    filtered = filtered.filter(t => t.paymentMethod.includes(methodMap[paymentMethod.value]));
  }

  // Apply amount range filter
  if (amountRange.value !== 'all') {
    const ranges = {
      '0-100': [0, 100],
      '100-250': [100, 250],
      '250-500': [250, 500],
      '500+': [500, Infinity]
    };
    const [min, max] = ranges[amountRange.value] || [0, Infinity];
    filtered = filtered.filter(t => t.amount >= min && t.amount <= max);
  }

  // Apply date range filter
  if (dateRange.value !== 'all') {
    const now = new Date();
    let cutoffDate;
    
    switch (dateRange.value) {
      case 'last30':
        cutoffDate = new Date(now.setDate(now.getDate() - 30));
        break;
      case 'last90':
        cutoffDate = new Date(now.setDate(now.getDate() - 90));
        break;
      case 'last180':
        cutoffDate = new Date(now.setDate(now.getDate() - 180));
        break;
      case 'custom':
        if (startDate.value && endDate.value) {
          const start = new Date(startDate.value);
          const end = new Date(endDate.value);
          filtered = filtered.filter(t => {
            const transactionDate = new Date(t.date);
            return transactionDate >= start && transactionDate <= end;
          });
        }
        break;
    }
    
    if (cutoffDate) {
      filtered = filtered.filter(t => new Date(t.date) >= cutoffDate);
    }
  }

  // Apply sorting
  filtered.sort((a, b) => {
    let aValue = a[sortField.value];
    let bValue = b[sortField.value];
    
    if (sortField.value === 'date') {
      aValue = new Date(aValue);
      bValue = new Date(bValue);
    }
    
    if (sortOrder.value === 'asc') {
      return aValue < bValue ? -1 : aValue > bValue ? 1 : 0;
    } else {
      return aValue > bValue ? -1 : aValue < bValue ? 1 : 0;
    }
  });

  return filtered;
});

const totalPages = computed(() => Math.ceil(filteredTransactions.value.length / itemsPerPage.value));

const paginatedTransactions = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage.value;
  const end = start + itemsPerPage.value;
  return filteredTransactions.value.slice(start, end);
});

const startIndex = computed(() => (currentPage.value - 1) * itemsPerPage.value);
const endIndex = computed(() => Math.min(startIndex.value + itemsPerPage.value, filteredTransactions.value.length));

const visiblePages = computed(() => {
  const pages = [];
  const start = Math.max(1, currentPage.value - 2);
  const end = Math.min(totalPages.value, currentPage.value + 2);
  
  for (let i = start; i <= end; i++) {
    pages.push(i);
  }
  
  return pages;
});

const hasActiveFilters = computed(() => {
  return searchQuery.value !== '' ||
         dateRange.value !== 'all' ||
         paymentStatus.value !== 'all' ||
         paymentMethod.value !== 'all' ||
         amountRange.value !== 'all';
});

// Methods
const searchTransactions = () => {
  currentPage.value = 1;
};

const resetFilters = () => {
  searchQuery.value = '';
  dateRange.value = 'all';
  startDate.value = '';
  endDate.value = '';
  paymentStatus.value = 'all';
  paymentMethod.value = 'all';
  amountRange.value = 'all';
  currentPage.value = 1;
};

const sortBy = (field) => {
  if (sortField.value === field) {
    sortOrder.value = sortOrder.value === 'asc' ? 'desc' : 'asc';
  } else {
    sortField.value = field;
    sortOrder.value = 'desc';
  }
};

const previousPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
  }
};

const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
  }
};

const goToPage = (page) => {
  currentPage.value = page;
};

const viewReceipt = (transaction) => {
  selectedTransaction.value = transaction;
  showReceiptModal.value = true;
};

const retryPayment = (transaction) => {
  retryTransaction.value = transaction;
  showRetryModal.value = true;
};

const viewTransactionDetails = (transaction) => {
  // Navigate to transaction details or show modal
  console.log('View details for transaction:', transaction.transactionId);
};

const downloadHistory = () => {
  console.log('Downloading payment history...');
};

const exportTransactions = () => {
  console.log('Exporting transactions to CSV...');
};

const printReceipt = () => {
  window.print();
};

const downloadReceipt = () => {
  console.log('Downloading receipt...');
};

const confirmRetryPayment = () => {
  console.log('Retrying payment with method:', retryPaymentMethod.value);
  showRetryModal.value = false;
  // Here you would typically make an API call to retry the payment
};

const getInvoiceId = (transaction) => {
  // Generate invoice ID based on transaction date and ID
  // This would typically come from your API response
  const year = new Date(transaction.date).getFullYear();
  const month = String(new Date(transaction.date).getMonth() + 1).padStart(2, '0');
  return `INV-${year}-${month}${transaction.transactionId.slice(-2)}`;
};

onMounted(() => {
  // Any initialization logic
});
</script>