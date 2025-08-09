<template>
  <div class="fade-in bg-gray-50">
    <!-- Top Stats Bar -->
    <div class="bg-white shadow-sm">
      <div class="container-custom py-4">
        <div class="flex flex-wrap items-center justify-between">
          <div class="flex items-center space-x-4 py-2">
            <div class="h-12 w-12 rounded-full bg-primary-500 text-white flex items-center justify-center text-xl font-bold">
              JD
            </div>
            <div>
              <h1 class="text-xl font-bold text-gray-900">Welcome back, John</h1>
              <div class="flex items-center">
                <span class="bg-success-100 text-success-800 text-xs px-2 py-0.5 rounded-full font-medium">
                  Account in Good Standing
                </span>
                <span class="mx-2 text-gray-300">•</span>
                <span class="text-sm text-gray-600">May 21, 2025</span>
              </div>
            </div>
          </div>
          <div class="flex items-center space-x-3">
            <button class="p-2 rounded-full text-gray-500 hover:text-gray-700 hover:bg-gray-100">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
              </svg>
            </button>
            <button class="p-2 rounded-full text-gray-500 hover:text-gray-700 hover:bg-gray-100">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
              </svg>
            </button>
            <div class="bg-gray-200 h-6 w-px mx-1"></div>
            <NuxtLink to="/profile" class="flex items-center text-primary-600 hover:text-primary-800">
              <span class="hidden sm:inline mr-1">My Profile</span>
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
              </svg>
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
    
    <div class="container-custom py-8">
      <!-- Main Grid Layout -->
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
        <!-- Left Column - Payment Plan Summary -->
        <div class="lg:col-span-1 space-y-6">
          <!-- Payment Progress Card -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="bg-gradient-to-r from-primary-500 to-primary-600 px-6 py-4">
              <div class="flex justify-between items-center">
                <h2 class="text-white font-bold text-lg">Payment Progress</h2>
                <span class="bg-white bg-opacity-20 text-white text-xs px-2.5 py-1 rounded-full">
                  40% Complete
                </span>
              </div>
              <div class="mt-4 mb-2">
                <div class="w-full bg-white bg-opacity-20 rounded-full h-2">
                  <div class="bg-white h-2 rounded-full" style="width: 40%"></div>
                </div>
              </div>
            </div>
            
            <div class="px-6 py-5">
              <div class="flex items-center justify-between mb-4">
                <span class="text-gray-500 text-sm">Total Plan Amount</span>
                <span class="font-bold text-gray-900">$2,500.00</span>
              </div>
              <div class="flex items-center justify-between">
                <div>
                  <span class="text-gray-500 text-sm">Paid</span>
                  <p class="font-bold text-success-600">$1,000.00</p>
                </div>
                <div class="h-8 w-px bg-gray-200"></div>
                <div>
                  <span class="text-gray-500 text-sm">Remaining</span>
                  <p class="font-bold text-primary-600">$1,500.00</p>
                </div>
                <div class="h-8 w-px bg-gray-200"></div>
                <div>
                  <span class="text-gray-500 text-sm">Next Due</span>
                  <p class="font-bold text-warning-600">$250.00</p>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Payment Plan Details Card -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="px-6 py-5 border-b border-gray-100">
              <div class="flex justify-between items-center">
                <h2 class="font-bold text-lg text-gray-900">Payment Plan Details</h2>
                <span class="text-xs px-2.5 py-1 rounded-full bg-blue-100 text-blue-800">
                  {{ planType }}
                </span>
              </div>
            </div>
            
            <div class="px-6 py-4">
              <div class="grid grid-cols-2 gap-4">
                <div>
                  <span class="text-gray-500 text-sm">Original Amount</span>
                  <p class="font-semibold text-gray-900">$2,500.00</p>
                </div>
                <div>
                  <span class="text-gray-500 text-sm">Interest Rate</span>
                  <p class="font-semibold text-gray-900">2.5%</p>
                </div>
                <div>
                  <span class="text-gray-500 text-sm">Start Date</span>
                  <p class="font-semibold text-gray-900">Jan 15, 2025</p>
                </div>
                <div>
                  <span class="text-gray-500 text-sm">End Date</span>
                  <p class="font-semibold text-gray-900">Oct 15, 2025</p>
                </div>
                <div>
                  <span class="text-gray-500 text-sm">Installment</span>
                  <p class="font-semibold text-gray-900">$250.00 / month</p>
                </div>
                <div>
                  <span class="text-gray-500 text-sm">Remaining</span>
                  <p class="font-semibold text-gray-900">6 payments</p>
                </div>
              </div>
              
              <div class="mt-5">
                <NuxtLink to="/payments" class="text-primary-600 text-sm font-medium hover:text-primary-700 inline-flex items-center">
                  View full payment schedule
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                  </svg>
                </NuxtLink>
              </div>
            </div>
          </div>
          
          <!-- Recent Activity Card -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="px-6 py-5 border-b border-gray-100">
              <div class="flex justify-between items-center">
                <h2 class="font-bold text-lg text-gray-900">Recent Activity</h2>
                <NuxtLink to="/history" class="text-primary-600 text-sm font-medium hover:text-primary-700">View all</NuxtLink>
              </div>
            </div>
            
            <div class="divide-y divide-gray-100">
              <div v-for="(activity, index) in recentActivity.slice(0, 3)" :key="index" class="px-6 py-4 flex items-start">
                <div
                  class="h-8 w-8 rounded-full flex items-center justify-center mr-3 flex-shrink-0"
                  :class="{
                    'bg-success-100 text-success-600': activity.type === 'payment',
                    'bg-primary-100 text-primary-600': activity.type === 'login',
                    'bg-warning-100 text-warning-600': activity.type === 'notification'
                  }"
                >
                  <svg v-if="activity.type === 'payment'" xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                  <svg v-if="activity.type === 'login'" xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 16l-4-4m0 0l4-4m-4 4h14m-5 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h7a3 3 0 013 3v1" />
                  </svg>
                  <svg v-if="activity.type === 'notification'" xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
                  </svg>
                </div>
                <div class="min-w-0 flex-1">
                  <p class="text-sm text-gray-900 font-medium truncate">{{ activity.description }}</p>
                  <p class="text-xs text-gray-500">{{ activity.time }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Right Column - Action Areas and Upcoming Payments -->
        <div class="lg:col-span-2 space-y-6">
          <!-- Action Cards -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 p-6">
            <div class="flex justify-between items-center mb-6">
              <h2 class="font-bold text-lg text-gray-900">Quick Actions</h2>
            </div>
            
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
              <button class="flex flex-col items-center justify-center bg-primary-50 rounded-lg p-4 hover:bg-primary-100 transition-colors">
                <div class="h-10 w-10 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mb-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z" />
                  </svg>
                </div>
                <span class="text-sm font-medium text-gray-900">Make Payment</span>
              </button>
              
              <button class="flex flex-col items-center justify-center bg-blue-50 rounded-lg p-4 hover:bg-blue-100 transition-colors">
                <div class="h-10 w-10 bg-blue-100 text-blue-600 rounded-full flex items-center justify-center mb-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                  </svg>
                </div>
                <span class="text-sm font-medium text-gray-900">Statements</span>
              </button>
              
              <button class="flex flex-col items-center justify-center bg-green-50 rounded-lg p-4 hover:bg-green-100 transition-colors">
                <div class="h-10 w-10 bg-green-100 text-green-600 rounded-full flex items-center justify-center mb-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
                  </svg>
                </div>
                <span class="text-sm font-medium text-gray-900">Schedule</span>
              </button>
              
              <NuxtLink to="/search" class="flex flex-col items-center justify-center bg-purple-50 rounded-lg p-4 hover:bg-purple-100 transition-colors">
                <div class="h-10 w-10 bg-purple-100 text-purple-600 rounded-full flex items-center justify-center mb-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                  </svg>
                </div>
                <span class="text-sm font-medium text-gray-900">Search</span>
              </NuxtLink>
            </div>
          </div>
          
          <!-- Important Notification -->
          <div v-if="notifications.length > 0" class="bg-gradient-to-r from-amber-50 to-amber-100 rounded-xl shadow-sm overflow-hidden border border-amber-200">
            <div class="p-6">
              <div class="flex">
                <div class="flex-shrink-0">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-amber-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
                  </svg>
                </div>
                <div class="ml-3">
                  <h3 class="text-sm font-medium text-amber-800">
                    {{ notifications[0].message }}
                  </h3>
                  <div class="mt-2 text-sm text-amber-700">
                    <p>Due date: May 15, 2025 (6 days from now)</p>
                  </div>
                  <div class="mt-3">
                    <div class="flex space-x-3">
                      <button
                        type="button"
                        class="inline-flex items-center px-3 py-1.5 border border-transparent text-xs font-medium rounded-md shadow-sm text-white bg-amber-600 hover:bg-amber-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-amber-500"
                      >
                        View payment
                      </button>
                      <button
                        type="button"
                        class="inline-flex items-center px-3 py-1.5 border border-gray-300 shadow-sm text-xs font-medium rounded-md text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-amber-500"
                      >
                        Dismiss
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Upcoming Payments Card -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="px-6 py-5 border-b border-gray-100">
              <div class="flex justify-between items-center">
                <h2 class="font-bold text-lg text-gray-900">Upcoming Payments</h2>
                <NuxtLink to="/payments" class="text-primary-600 text-sm font-medium hover:text-primary-700">View all</NuxtLink>
              </div>
            </div>
            
            <div class="overflow-x-auto">
              <table class="min-w-full divide-y divide-gray-200">
                <thead class="bg-gray-50">
                  <tr>
                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                      Due Date
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
                  <tr v-for="(payment, index) in upcomingPayments.slice(0, 3)" :key="index" 
                    :class="{'bg-yellow-50': payment.status === 'Due Soon'}">
                    <td class="px-6 py-4 whitespace-nowrap">
                      <div class="flex items-center">
                        <div class="flex-shrink-0 h-8 w-8 bg-gray-100 rounded-full flex items-center justify-center mr-3">
                          <span class="text-xs font-medium">
                            {{ payment.dueDate.split(' ')[0].substring(0, 3) }}
                          </span>
                        </div>
                        <div>
                          <div class="text-sm font-medium text-gray-900">{{ payment.dueDate }}</div>
                          <div class="text-xs text-gray-500">{{ payment.description }}</div>
                        </div>
                      </div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                      <div class="text-sm font-medium text-gray-900">${{ payment.amount.toFixed(2) }}</div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                      <span 
                        class="px-2 inline-flex text-xs leading-5 font-medium rounded-full" 
                        :class="{
                          'bg-warning-100 text-warning-800': payment.status === 'Due Soon',
                          'bg-error-100 text-error-800': payment.status === 'Overdue',
                          'bg-gray-100 text-gray-800': payment.status === 'Upcoming'
                        }"
                      >
                        {{ payment.status }}
                      </span>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-right">
                      <NuxtLink 
                        to="/payments" 
                        class="text-primary-600 hover:text-primary-900 text-sm font-medium"
                        :class="{'text-warning-600 hover:text-warning-900': payment.status === 'Due Soon'}"
                      >
                        Pay now
                      </NuxtLink>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
          
          <!-- Payment History Card -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="px-6 py-5 border-b border-gray-100">
              <div class="flex justify-between items-center">
                <h2 class="font-bold text-lg text-gray-900">Payment History</h2>
                <div class="flex space-x-2">
                  <NuxtLink to="/payments/invoices" class="text-secondary-600 text-sm font-medium hover:text-secondary-700">View Invoices</NuxtLink>
                  <NuxtLink to="/history" class="text-primary-600 text-sm font-medium hover:text-primary-700">View all</NuxtLink>
                </div>
              </div>
            </div>
            
            <div class="p-6">
              <div class="relative">
                <div class="absolute inset-0 flex items-center" aria-hidden="true">
                  <div class="w-full border-t border-gray-200"></div>
                </div>
                <div class="relative flex justify-center">
                  <span class="px-3 bg-white text-sm text-gray-500">Recent Payments</span>
                </div>
              </div>
              
              <div class="mt-6 grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="border border-gray-200 rounded-lg p-4">
                  <div class="flex justify-between mb-2">
                    <span class="text-xs text-gray-500">April 15, 2025</span>
                    <span class="text-xs font-medium text-success-600">Paid</span>
                  </div>
                  <div class="flex justify-between items-center">
                    <div>
                      <h4 class="font-medium text-gray-900">Monthly Instalment</h4>
                      <p class="text-xs text-gray-500">Transaction ID: TRX-2025-0415</p>
                    </div>
                    <div class="text-lg font-bold text-gray-900">$250.00</div>
                  </div>
                </div>
                
                <div class="border border-gray-200 rounded-lg p-4">
                  <div class="flex justify-between mb-2">
                    <span class="text-xs text-gray-500">March 15, 2025</span>
                    <span class="text-xs font-medium text-success-600">Paid</span>
                  </div>
                  <div class="flex justify-between items-center">
                    <div>
                      <h4 class="font-medium text-gray-900">Monthly Instalment</h4>
                      <p class="text-xs text-gray-500">Transaction ID: TRX-2025-0315</p>
                    </div>
                    <div class="text-lg font-bold text-gray-900">$250.00</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  layout: 'default',
});

// Sample data - would come from API in real app
const planType = 'Standard Monthly Plan';
const notifications = [
  { 
    message: 'Your upcoming payment of $250.00 is due in 6 days. Please ensure sufficient funds are available.',
    date: 'May 9, 2025'
  },
  { 
    message: 'Special offer: Switch to annual payments and save 5% on total interest. Limited time offer ending May 31, 2025.',
    date: 'May 1, 2025'
  }
];

const upcomingPayments = [
  {
    dueDate: 'May 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Due Soon'
  },
  {
    dueDate: 'June 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Upcoming'
  },
  {
    dueDate: 'July 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Upcoming'
  },
  {
    dueDate: 'August 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Upcoming'
  },
  {
    dueDate: 'September 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Upcoming'
  }
];

const recentActivity = [
  {
    type: 'payment',
    description: 'Payment of $250.00 completed successfully',
    time: '15 Apr 2025, 10:23 AM'
  },
  {
    type: 'notification',
    description: 'Upcoming payment reminder sent for May instalment',
    time: '10 Apr 2025, 9:00 AM'
  },
  {
    type: 'login',
    description: 'New sign-in detected from Chrome on Windows',
    time: '05 Apr 2025, 3:45 PM'
  },
  {
    type: 'payment',
    description: 'Payment of $250.00 completed successfully',
    time: '15 Mar 2025, 11:30 AM'
  }
];
</script>