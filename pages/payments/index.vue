<template>
  <div class="fade-in">
    <!-- Enhanced Header Section -->
    <div class="bg-white shadow">
      <div class="container-custom py-6">
        <div class="flex flex-col md:flex-row md:items-center md:justify-between">
          <div class="mb-4 md:mb-0">
            <h1 class="text-2xl font-bold text-gray-900">Payments</h1>
            <p class="text-sm text-gray-600 mt-1">Manage your payment plans and schedule payments</p>
          </div>
          <div class="flex space-x-2">
            <button @click="openPaymentModal" class="btn-primary flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
              </svg>
              Make Payment
            </button>
            <button class="btn-outline flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
              </svg>
              Download Statement
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Status Overview Cards -->
    <div class="container-custom py-6">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
        <div class="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <div class="flex justify-between mb-4">
            <div>
              <p class="text-sm font-medium text-gray-500">Current Balance</p>
              <h3 class="text-2xl font-bold text-gray-900">${{ formatCurrency(totalBalance) }}</h3>
            </div>
            <div class="h-12 w-12 rounded-full bg-primary-100 flex items-center justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
          </div>
          <div class="flex justify-between text-sm">
            <span class="text-gray-500">Monthly payment:</span>
            <span class="font-medium text-gray-900">${{ formatCurrency(monthlyPayment) }}</span>
          </div>
          <div class="mt-4">
            <button @click="openPaymentModal" class="text-primary-600 text-sm font-medium hover:text-primary-800 flex items-center">
              Make Payment
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
            </button>
          </div>
        </div>

        <div class="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <div class="flex justify-between mb-4">
            <div>
              <p class="text-sm font-medium text-gray-500">Next Payment Due</p>
              <h3 class="text-2xl font-bold text-gray-900">${{ formatCurrency(nextPaymentAmount) }}</h3>
            </div>
            <div class="h-12 w-12 rounded-full bg-warning-100 flex items-center justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-warning-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
              </svg>
            </div>
          </div>
          <div class="flex justify-between text-sm">
            <span :class="getDueDateClass(nextPaymentDue)">Due {{ formatDueDate(nextPaymentDue) }}</span>
            <span class="font-medium text-gray-900">{{ remainingDays }} days left</span>
          </div>
          <div class="mt-4">
            <div class="w-full bg-gray-200 rounded-full h-2">
              <div class="bg-warning-500 h-2 rounded-full" :style="{ width: `${getDaysPercentage()}%` }"></div>
            </div>
          </div>
        </div>

        <div class="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <div class="flex justify-between mb-4">
            <div>
              <p class="text-sm font-medium text-gray-500">Payment Plan Progress</p>
              <h3 class="text-2xl font-bold text-gray-900">{{ completionPercentage }}%</h3>
            </div>
            <div class="h-12 w-12 rounded-full bg-success-100 flex items-center justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-success-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
          </div>
          <div class="flex justify-between text-sm">
            <span class="text-gray-500">Payments completed:</span>
            <span class="font-medium text-gray-900">{{ completedPayments }} of {{ totalPayments }}</span>
          </div>
          <div class="mt-4">
            <div class="w-full bg-gray-200 rounded-full h-2">
              <div class="bg-success-500 h-2 rounded-full" :style="{ width: `${completionPercentage}%` }"></div>
            </div>
          </div>
        </div>
      </div>

      <!-- Enhanced Payment Schedule Section -->
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
        <div class="lg:col-span-2">
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="px-6 py-5 border-b border-gray-100 flex justify-between items-center">
              <h2 class="text-xl font-bold text-gray-900">Upcoming Payments</h2>
              <div class="flex items-center">
                <div class="relative">
                  <select v-model="filterStatus" class="appearance-none bg-gray-100 text-gray-700 px-3 py-1 pr-8 rounded-md text-sm font-medium focus:outline-none focus:ring-2 focus:ring-primary-500">
                    <option value="all">All</option>
                    <option value="pending">Pending</option>
                    <option value="overdue">Overdue</option>
                    <option value="paid">Paid</option>
                  </select>
                  <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2">
                    <svg class="h-4 w-4 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                    </svg>
                  </div>
                </div>
                <button @click="refreshPaymentData" class="ml-2 p-1 rounded-md hover:bg-gray-100">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
                  </svg>
                </button>
              </div>
            </div>

            <!-- Payment schedule items -->
            <div v-if="filteredPayments.length > 0" class="overflow-hidden overflow-y-auto" style="max-height: 400px;">
              <div v-for="(payment, index) in filteredPayments" :key="index" :class="[
                'px-6 py-4 border-b border-gray-100 flex justify-between items-center hover:bg-gray-50',
                payment.selected ? 'bg-blue-50' : ''
              ]">
                <div class="flex items-center">
                  <div v-if="payment.status !== 'paid'" class="mr-3">
                    <input type="checkbox" :id="'payment-' + index" v-model="payment.selected" class="rounded text-primary-500 focus:ring-primary-500 h-4 w-4 cursor-pointer" />
                  </div>
                  <div v-else class="h-4 w-4 mr-3"><!-- Placeholder for alignment --></div>
                  <div class="flex-shrink-0 h-10 w-10 rounded-full flex items-center justify-center mr-3"
                    :class="{
                      'bg-warning-100 text-warning-800': payment.status === 'due-soon',
                      'bg-error-100 text-error-800': payment.status === 'overdue',
                      'bg-gray-100 text-gray-800': payment.status === 'upcoming',
                      'bg-success-100 text-success-800': payment.status === 'paid'
                    }">
                    <span class="text-xs font-medium">
                      {{ payment.dueDate.split(' ')[0].substring(0, 3) }}
                    </span>
                  </div>
                  <div>
                    <p class="font-medium text-gray-900">{{ payment.description }}</p>
                    <div class="flex items-center mt-1">
                      <span :class="[
                        'text-xs px-2 py-0.5 rounded-full',
                        payment.status === 'due-soon' ? 'bg-warning-100 text-warning-800' :
                        payment.status === 'overdue' ? 'bg-error-100 text-error-800' :
                        payment.status === 'upcoming' ? 'bg-gray-100 text-gray-500' :
                        'bg-success-100 text-success-800'
                      ]">
                        {{ getStatusText(payment.status) }}
                      </span>
                      <span class="text-xs text-gray-500 ml-2">Due: {{ payment.dueDate }}</span>
                    </div>
                  </div>
                </div>
                <div class="text-right">
                  <p class="font-medium text-gray-900">${{ formatCurrency(payment.amount) }}</p>
                  <p v-if="payment.status === 'paid'" class="text-xs text-gray-500 mt-1">
                    Paid on {{ payment.paidDate }}
                  </p>
                  <p v-else-if="payment.status === 'overdue'" class="text-xs text-error-600 mt-1">
                    {{ payment.daysLate }} days late
                  </p>
                </div>
              </div>
            </div>

            <div v-else class="px-6 py-12 text-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="mx-auto h-12 w-12 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
              </svg>
              <h3 class="mt-2 text-sm font-medium text-gray-900">No payments found</h3>
              <p class="mt-1 text-sm text-gray-500">
                No payments match your current filter criteria.
              </p>
            </div>

            <!-- Action buttons -->
            <div class="px-6 py-4 bg-gray-50 border-t border-gray-100 flex flex-col sm:flex-row justify-between">
              <div class="flex items-center mb-3 sm:mb-0">
                <span class="text-sm text-gray-700 mr-3">
                  {{ selectedCount }} selected: ${{ formatCurrency(selectedTotal) }}
                </span>
                <button 
                  @click="selectAllVisible" 
                  :disabled="!hasPayableItems"
                  :class="[
                    'text-sm font-medium mr-3',
                    hasPayableItems ? 'text-primary-600 hover:text-primary-800' : 'text-gray-400 cursor-not-allowed'
                  ]">
                  Select All
                </button>
                <button
                  @click="clearSelection"
                  :disabled="selectedCount === 0"
                  :class="[
                    'text-sm font-medium',
                    selectedCount > 0 ? 'text-primary-600 hover:text-primary-800' : 'text-gray-400 cursor-not-allowed'
                  ]">
                  Clear
                </button>
              </div>
              <button
                @click="paySelected"
                :disabled="selectedCount === 0"
                :class="[
                  'btn-primary',
                  selectedCount === 0 ? 'opacity-50 cursor-not-allowed' : ''
                ]">
                Pay Selected ({{ selectedCount }})
              </button>
            </div>
          </div>

          <!-- Payment History -->
          <div class="mt-6 bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="px-6 py-5 border-b border-gray-100 flex justify-between items-center">
              <h2 class="text-xl font-bold text-gray-900">Recent Payment History</h2>
              <NuxtLink to="/history" class="text-primary-600 hover:text-primary-800 text-sm font-medium">
                View All
              </NuxtLink>
            </div>

            <div class="overflow-hidden overflow-x-auto">
              <table class="min-w-full divide-y divide-gray-200">
                <thead>
                  <tr>
                    <th class="px-6 py-3 bg-gray-50 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                      Date
                    </th>
                    <th class="px-6 py-3 bg-gray-50 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                      Description
                    </th>
                    <th class="px-6 py-3 bg-gray-50 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                      Payment Method
                    </th>
                    <th class="px-6 py-3 bg-gray-50 text-right text-xs font-medium text-gray-500 uppercase tracking-wider">
                      Amount
                    </th>
                    <th class="px-6 py-3 bg-gray-50 text-right text-xs font-medium text-gray-500 uppercase tracking-wider">
                      Status
                    </th>
                  </tr>
                </thead>
                <tbody class="bg-white divide-y divide-gray-200">
                  <tr v-for="(payment, index) in recentPayments" :key="index" class="hover:bg-gray-50">
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                      {{ payment.date }}
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">
                      {{ payment.description }}
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                      <div class="flex items-center">
                        <span class="h-6 w-6 bg-gray-100 rounded-full flex items-center justify-center mr-2">
                          <span class="text-xs font-semibold">{{ payment.paymentMethod[0] }}</span>
                        </span>
                        <span>{{ payment.paymentMethod }}</span>
                      </div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900 text-right">
                      ${{ formatCurrency(payment.amount) }}
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-right">
                      <span :class="[
                        'px-2 inline-flex text-xs leading-5 font-semibold rounded-full',
                        payment.status === 'success' ? 'bg-success-100 text-success-800' :
                        payment.status === 'pending' ? 'bg-warning-100 text-warning-800' :
                        'bg-error-100 text-error-800'
                      ]">
                        {{ payment.status === 'success' ? 'Successful' : 
                           payment.status === 'pending' ? 'Processing' : 'Failed' }}
                      </span>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
            <div v-if="recentPayments.length === 0" class="px-6 py-8 text-center">
              <p class="text-gray-500 text-sm">No payment history available.</p>
            </div>
          </div>
        </div>

        <div>
          <!-- Payment Summary Card -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 mb-6">
            <div class="px-6 py-5 border-b border-gray-100">
              <h2 class="text-xl font-bold text-gray-900">Payment Summary</h2>
            </div>
            <div class="p-6">
              <div class="space-y-4">
                <div class="flex justify-between">
                  <span class="text-gray-600">Original Amount:</span>
                  <span class="font-medium">${{ formatCurrency(originalAmount) }}</span>
                </div>
                <div class="flex justify-between">
                  <span class="text-gray-600">Amount Paid:</span>
                  <span class="font-medium">${{ formatCurrency(amountPaid) }}</span>
                </div>
                <div class="flex justify-between">
                  <span class="text-gray-600">Remaining Balance:</span>
                  <span class="font-bold">${{ formatCurrency(totalBalance) }}</span>
                </div>
                <div class="pt-3 border-t border-gray-200">
                  <div class="mb-1 flex justify-between text-sm">
                    <span class="text-gray-600">Payment Progress:</span>
                    <span class="font-medium">{{ completionPercentage }}%</span>
                  </div>
                  <div class="w-full bg-gray-200 rounded-full h-3">
                    <div class="bg-primary-500 h-3 rounded-full" :style="{ width: `${completionPercentage}%` }"></div>
                  </div>
                </div>
              </div>
              <div class="mt-6 pt-4 border-t border-gray-200">
                <h3 class="text-md font-medium mb-3">Payment Schedule</h3>
                <div class="space-y-3">
                  <div class="flex justify-between text-sm">
                    <span class="text-gray-600">Payment Frequency:</span>
                    <span class="font-medium">{{ paymentFrequency }}</span>
                  </div>
                  <div class="flex justify-between text-sm">
                    <span class="text-gray-600">Next Payment:</span>
                    <span class="font-medium">{{ formatDueDate(nextPaymentDue) }}</span>
                  </div>
                  <div class="flex justify-between text-sm">
                    <span class="text-gray-600">Final Payment:</span>
                    <span class="font-medium">{{ finalPaymentDate }}</span>
                  </div>
                </div>
              </div>
              <div class="mt-6">
                <button @click="showAutopaySettings = !showAutopaySettings" class="text-primary-600 text-sm font-medium hover:text-primary-800 flex items-center w-full justify-between">
                  <span>Autopay Settings</span>
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1 transition-transform" :class="{ 'rotate-180': showAutopaySettings }" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                  </svg>
                </button>
                <div v-if="showAutopaySettings" class="mt-3 p-3 bg-gray-50 rounded-lg">
                  <div class="flex items-center justify-between mb-2">
                    <span class="text-sm font-medium">AutoPay Status</span>
                    <label class="relative inline-flex items-center cursor-pointer">
                      <input v-model="autopayEnabled" type="checkbox" class="sr-only peer">
                      <div class="w-11 h-6 bg-gray-200 peer-focus:outline-none peer-focus:ring-4 peer-focus:ring-primary-300 rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-primary-600"></div>
                    </label>
                  </div>
                  <div v-if="autopayEnabled" class="mt-3 space-y-2 text-sm">
                    <p class="text-gray-600">Your next automatic payment of ${{ formatCurrency(nextPaymentAmount) }} will be processed on {{ formatDueDate(nextPaymentDue) }}.</p>
                    <p class="text-gray-500">Using {{ defaultPaymentMethod }}</p>
                  </div>
                  <div v-else class="mt-2 text-sm text-gray-600">
                    Enable AutoPay to automatically pay your bills on the due date.
                  </div>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Assistance Options -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="px-6 py-5 border-b border-gray-100">
              <h2 class="text-xl font-bold text-gray-900">Need Assistance?</h2>
            </div>
            <div class="p-6">
              <div class="space-y-4">
                <button class="w-full flex items-center justify-between p-3 border border-gray-200 rounded-lg hover:bg-gray-50 transition-colors">
                  <div class="flex items-center">
                    <div class="h-8 w-8 rounded-full bg-primary-100 flex items-center justify-center mr-3">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                      </svg>
                    </div>
                    <span class="font-medium text-gray-900">Payment Plan Options</span>
                  </div>
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                  </svg>
                </button>
                
                <button class="w-full flex items-center justify-between p-3 border border-gray-200 rounded-lg hover:bg-gray-50 transition-colors">
                  <div class="flex items-center">
                    <div class="h-8 w-8 rounded-full bg-warning-100 flex items-center justify-center mr-3">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-warning-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                      </svg>
                    </div>
                    <span class="font-medium text-gray-900">Request Payment Extension</span>
                  </div>
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                  </svg>
                </button>
                
                <button class="w-full flex items-center justify-between p-3 border border-gray-200 rounded-lg hover:bg-gray-50 transition-colors">
                  <div class="flex items-center">
                    <div class="h-8 w-8 rounded-full bg-blue-100 flex items-center justify-center mr-3">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                      </svg>
                    </div>
                    <span class="font-medium text-gray-900">Contact Support</span>
                  </div>
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                  </svg>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Make Payment Modal -->
    <div v-if="showPaymentModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-4">
      <div class="bg-white rounded-xl shadow-xl max-w-md w-full mx-auto max-h-[90vh] overflow-hidden">
        <div class="px-6 py-4 border-b border-gray-200 flex justify-between items-center">
          <h3 class="text-xl font-bold text-gray-900">Make a Payment</h3>
          <button @click="closePaymentModal" class="text-gray-400 hover:text-gray-500">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
        <div class="px-6 py-4 overflow-y-auto" style="max-height: 60vh;">
          <div class="space-y-4">
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Payment Amount</label>
              <div class="mt-1 relative rounded-md shadow-sm">
                <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                  <span class="text-gray-500 sm:text-sm">$</span>
                </div>
                <input v-model="paymentAmount" type="text" class="focus:ring-primary-500 focus:border-primary-500 block w-full pl-7 pr-12 sm:text-sm border-gray-300 rounded-md" placeholder="0.00">
              </div>
            </div>
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Payment Method</label>
              <div class="mt-1 space-y-3">
                <div v-for="(method, index) in paymentMethods" :key="index" 
                    class="relative border p-3 rounded-lg cursor-pointer"
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
                
                <button @click="addNewPaymentMethod" class="w-full flex items-center justify-center p-3 border border-dashed border-gray-300 rounded-lg hover:bg-gray-50">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
                  </svg>
                  <span class="text-sm font-medium text-gray-600">Add Payment Method</span>
                </button>
              </div>
            </div>
          </div>
        </div>
        <div class="px-6 py-4 bg-gray-50 border-t border-gray-200 flex justify-end space-x-3">
          <button @click="closePaymentModal" class="btn-outline">Cancel</button>
          <button @click="proceedToReview" class="btn-primary">Continue to Review</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import { useRouter } from 'vue-router';

definePageMeta({
  layout: 'default',
});

const router = useRouter();

// Reactive state
const totalBalance = ref(2500.00);
const originalAmount = ref(5000.00);
const amountPaid = ref(2500.00);
const monthlyPayment = ref(250.00);
const nextPaymentAmount = ref(250.00);
const nextPaymentDue = ref(new Date('2025-06-15'));
const completedPayments = ref(10);
const totalPayments = ref(20);
const paymentFrequency = ref('Monthly');
const finalPaymentDate = ref('Jan 15, 2026');
const showAutopaySettings = ref(false);
const autopayEnabled = ref(true);
const defaultPaymentMethod = ref('Visa ending in 1234');

// Payment modal state
const showPaymentModal = ref(false);
const paymentAmount = ref('');
const selectedPaymentMethod = ref('card1');

// Payment schedule filter state
const filterStatus = ref('all');

// Mock data for payment schedule
const payments = ref([
  {
    id: 1,
    description: 'Monthly Instalment (June 2025)',
    dueDate: 'Jun 15, 2025',
    amount: 250.00,
    status: 'due-soon',
    selected: false,
  },
  {
    id: 2,
    description: 'Monthly Instalment (July 2025)',
    dueDate: 'Jul 15, 2025',
    amount: 250.00,
    status: 'upcoming',
    selected: false,
  },
  {
    id: 3,
    description: 'Monthly Instalment (August 2025)',
    dueDate: 'Aug 15, 2025',
    amount: 250.00,
    status: 'upcoming',
    selected: false,
  },
  {
    id: 4,
    description: 'Monthly Instalment (May 2025)',
    dueDate: 'May 15, 2025',
    amount: 250.00,
    status: 'overdue',
    daysLate: 6,
    selected: false,
  },
  {
    id: 5,
    description: 'Monthly Instalment (April 2025)',
    dueDate: 'April 15, 2025',
    amount: 250.00,
    status: 'paid',
    paidDate: 'April 14, 2025',
  },
]);

// Mock data for payment methods
const paymentMethods = ref([
  {
    id: 'card1',
    name: 'Visa',
    details: 'Ending in 1234 • Expires 09/27',
    icon: null
  },
  {
    id: 'card2',
    name: 'Mastercard',
    details: 'Ending in 5678 • Expires 12/25',
    icon: null
  },
  {
    id: 'bank1',
    name: 'Bank Account',
    details: 'Checking **** 9012',
    icon: null
  }
]);

// Mock data for recent payments
const recentPayments = ref([
  {
    date: 'Apr 14, 2025',
    description: 'Monthly Instalment (April)',
    paymentMethod: 'Visa',
    amount: 250.00,
    status: 'success'
  },
  {
    date: 'Mar 15, 2025',
    description: 'Monthly Instalment (March)',
    paymentMethod: 'Visa',
    amount: 250.00,
    status: 'success'
  },
  {
    date: 'Feb 15, 2025',
    description: 'Monthly Instalment (February)',
    paymentMethod: 'Bank Account',
    amount: 250.00,
    status: 'success'
  },
]);

// Computed properties
const completionPercentage = computed(() => {
  return Math.round((completedPayments.value / totalPayments.value) * 100);
});

const remainingDays = computed(() => {
  const today = new Date();
  const due = new Date(nextPaymentDue.value);
  const timeDiff = due.getTime() - today.getTime();
  return Math.max(0, Math.ceil(timeDiff / (1000 * 3600 * 24)));
});

const filteredPayments = computed(() => {
  if (filterStatus.value === 'all') {
    return payments.value;
  }
  return payments.value.filter(p => {
    if (filterStatus.value === 'pending') return p.status === 'due-soon' || p.status === 'upcoming';
    if (filterStatus.value === 'overdue') return p.status === 'overdue';
    if (filterStatus.value === 'paid') return p.status === 'paid';
    return true;
  });
});

const selectedCount = computed(() => {
  return payments.value.filter(p => p.selected).length;
});

const selectedTotal = computed(() => {
  return payments.value
    .filter(p => p.selected)
    .reduce((sum, payment) => sum + payment.amount, 0);
});

const hasPayableItems = computed(() => {
  return payments.value.some(p => p.status !== 'paid');
});

// Methods
const formatCurrency = (value) => {
  return value.toFixed(2).replace(/\d(?=(\d{3})+\.)/g, '$&,');
};

const formatDueDate = (date) => {
  if (typeof date === 'string') {
    return date;
  }
  
  const options = { month: 'short', day: 'numeric' };
  return new Date(date).toLocaleDateString('en-US', options);
};

const getDueDateClass = (date) => {
  const today = new Date();
  const dueDate = new Date(date);
  
  if (dueDate < today) {
    return 'text-error-600';
  }
  
  const daysDiff = Math.ceil((dueDate - today) / (1000 * 60 * 60 * 24));
  if (daysDiff <= 7) {
    return 'text-warning-600';
  }
  
  return 'text-gray-500';
};

const getDaysPercentage = () => {
  const totalDays = 30; // Assuming a monthly payment cycle
  const percentage = (remainingDays.value / totalDays) * 100;
  return 100 - Math.min(100, Math.max(0, percentage));
};

const getStatusText = (status) => {
  switch (status) {
    case 'due-soon': return 'Due Soon';
    case 'overdue': return 'Overdue';
    case 'upcoming': return 'Upcoming';
    case 'paid': return 'Paid';
    default: return status;
  }
};

const refreshPaymentData = () => {
  // In a real app, this would fetch the latest payment data
  console.log('Refreshing payment data...');
};

const selectAllVisible = () => {
  filteredPayments.value.forEach(payment => {
    if (payment.status !== 'paid') {
      payment.selected = true;
    }
  });
};

const clearSelection = () => {
  payments.value.forEach(payment => {
    payment.selected = false;
  });
};

const paySelected = () => {
  const selectedPayments = payments.value.filter(p => p.selected);
  if (selectedPayments.length > 0) {
    router.push('/payments/review');
  }
};

const openPaymentModal = () => {
  paymentAmount.value = nextPaymentAmount.value.toString();
  showPaymentModal.value = true;
};

const closePaymentModal = () => {
  showPaymentModal.value = false;
};

const addNewPaymentMethod = () => {
  // In a real app, this would open a payment method form
  alert('In a real app, this would open a form to add a new payment method');
};

const proceedToReview = () => {
  if (!paymentAmount.value || parseFloat(paymentAmount.value) <= 0) {
    alert('Please enter a valid payment amount');
    return;
  }
  
  if (!selectedPaymentMethod.value) {
    alert('Please select a payment method');
    return;
  }
  
  router.push('/payments/review');
};

onMounted(() => {
  // In a real app, this would fetch the initial payment data
  console.log('Payment page mounted');
});
</script>

