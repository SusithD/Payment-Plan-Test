<template>
  <div class="fade-in">
    <div class="bg-white shadow">
      <div class="container-custom py-6">
        <h1 class="text-2xl font-bold text-gray-900">Dashboard</h1>
      </div>
    </div>
    
    <div class="container-custom py-8">
      <!-- Welcome section with account summary badge -->
      <div class="card mb-8">
        <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between">
          <div class="mb-4 sm:mb-0">
            <div class="flex items-center">
              <h2 class="text-2xl font-bold mr-3">Welcome back, John!</h2>
              <span class="bg-success-100 text-success-800 text-xs px-2.5 py-1 rounded-full font-medium">Account in Good Standing</span>
            </div>
            <p class="text-gray-600 mt-1">Here's a summary of your payment plan.</p>
          </div>
          <div class="flex space-x-3">
            <NuxtLink to="/profile" class="btn-outline">
              My Profile
            </NuxtLink>
            <NuxtLink to="/payments" class="btn-primary">
              Make a payment
            </NuxtLink>
          </div>
        </div>
      </div>
      
      <!-- Payment Progress -->
      <div class="card mb-8">
        <h2 class="text-xl font-bold mb-4">Payment Progress</h2>
        <div class="mb-4">
          <div class="flex justify-between mb-1">
            <span class="text-sm font-medium text-gray-700">Overall Progress</span>
            <span class="text-sm font-medium text-gray-700">40% Complete</span>
          </div>
          <div class="w-full bg-gray-200 rounded-full h-2.5">
            <div class="bg-primary-600 h-2.5 rounded-full" style="width: 40%"></div>
          </div>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 text-center">
          <div>
            <span class="text-sm text-gray-500">Paid Amount</span>
            <p class="text-xl font-bold text-success-700">$1,000.00</p>
          </div>
          <div>
            <span class="text-sm text-gray-500">Total Plan Amount</span>
            <p class="text-xl font-bold">$2,500.00</p>
          </div>
          <div>
            <span class="text-sm text-gray-500">Remaining Balance</span>
            <p class="text-xl font-bold text-primary-700">$1,500.00</p>
          </div>
        </div>
      </div>
      
      <!-- Overview Cards -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
        <div class="card bg-primary-50 border border-primary-100">
          <div class="flex justify-between items-start">
            <div>
              <p class="text-sm font-medium text-primary-700 mb-1">Upcoming Payment</p>
              <p class="text-2xl font-bold text-primary-900">$250.00</p>
              <p class="text-sm text-primary-700 mt-1">Due on May 15, 2025</p>
            </div>
            <div class="h-10 w-10 bg-primary-100 text-primary-600 rounded-lg flex items-center justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
              </svg>
            </div>
          </div>
        </div>
        
        <div class="card bg-secondary-50 border border-secondary-100">
          <div class="flex justify-between items-start">
            <div>
              <p class="text-sm font-medium text-secondary-700 mb-1">Total Remaining</p>
              <p class="text-2xl font-bold text-secondary-900">$1,250.00</p>
              <p class="text-sm text-secondary-700 mt-1">Over 5 instalments</p>
            </div>
            <div class="h-10 w-10 bg-secondary-100 text-secondary-600 rounded-lg flex items-center justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
          </div>
        </div>
        
        <div class="card bg-accent-50 border border-accent-100">
          <div class="flex justify-between items-start">
            <div>
              <p class="text-sm font-medium text-accent-700 mb-1">Last Payment</p>
              <p class="text-2xl font-bold text-accent-900">$250.00</p>
              <p class="text-sm text-accent-700 mt-1">Paid on April 15, 2025</p>
            </div>
            <div class="h-10 w-10 bg-accent-100 text-accent-600 rounded-lg flex items-center justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Quick Links / Actions -->
      <div class="grid grid-cols-1 md:grid-cols-4 gap-4 mb-8">
        <div class="card bg-white hover:bg-gray-50 transition-colors cursor-pointer flex flex-col items-center justify-center text-center p-4">
          <div class="h-12 w-12 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mb-3">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
            </svg>
          </div>
          <h3 class="font-medium">Schedule Payment</h3>
          <p class="text-xs text-gray-500 mt-1">Set up future payments</p>
        </div>
        <div class="card bg-white hover:bg-gray-50 transition-colors cursor-pointer flex flex-col items-center justify-center text-center p-4">
          <div class="h-12 w-12 bg-secondary-100 text-secondary-600 rounded-full flex items-center justify-center mb-3">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
            </svg>
          </div>
          <h3 class="font-medium">View Statement</h3>
          <p class="text-xs text-gray-500 mt-1">Download or view statements</p>
        </div>
        <div class="card bg-white hover:bg-gray-50 transition-colors cursor-pointer flex flex-col items-center justify-center text-center p-4">
          <div class="h-12 w-12 bg-accent-100 text-accent-600 rounded-full flex items-center justify-center mb-3">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
            </svg>
          </div>
          <h3 class="font-medium">Contact Support</h3>
          <p class="text-xs text-gray-500 mt-1">Get help with your account</p>
        </div>
        <div class="card bg-white hover:bg-gray-50 transition-colors cursor-pointer flex flex-col items-center justify-center text-center p-4">
          <div class="h-12 w-12 bg-gray-100 text-gray-600 rounded-full flex items-center justify-center mb-3">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
            </svg>
          </div>
          <h3 class="font-medium">Account Settings</h3>
          <p class="text-xs text-gray-500 mt-1">Update your preferences</p>
        </div>
      </div>
      
      <!-- Payment Plan Details -->
      <div class="card mb-8">
        <div class="flex justify-between items-center mb-6">
          <h2 class="text-xl font-bold">Payment Plan Details</h2>
          <div class="text-sm px-3 py-1 rounded-full bg-blue-100 text-blue-800">
            {{ planType }}
          </div>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <div>
            <div class="mb-4">
              <p class="text-sm text-gray-500 mb-1">Original Amount</p>
              <p class="font-bold text-lg">$2,500.00</p>
            </div>
            <div class="mb-4">
              <p class="text-sm text-gray-500 mb-1">Instalment Amount</p>
              <p class="font-bold text-lg">$250.00</p>
            </div>
            <div>
              <p class="text-sm text-gray-500 mb-1">Interest Rate</p>
              <p class="font-bold text-lg">2.5%</p>
            </div>
          </div>
          <div>
            <div class="mb-4">
              <p class="text-sm text-gray-500 mb-1">Start Date</p>
              <p class="font-bold text-lg">January 15, 2025</p>
            </div>
            <div class="mb-4">
              <p class="text-sm text-gray-500 mb-1">End Date</p>
              <p class="font-bold text-lg">October 15, 2025</p>
            </div>
            <div>
              <p class="text-sm text-gray-500 mb-1">Payment Frequency</p>
              <p class="font-bold text-lg">Monthly</p>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Important Notifications -->
      <div v-if="notifications.length > 0" class="card mb-8 bg-yellow-50 border border-yellow-100">
        <h2 class="text-xl font-bold mb-4 flex items-center">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-yellow-500 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
          </svg>
          Important Notifications
        </h2>
        
        <div class="space-y-4">
          <div v-for="(notification, index) in notifications" :key="index" class="flex items-start p-3 rounded-lg bg-white shadow-sm">
            <div class="h-8 w-8 rounded-full text-yellow-600 flex items-center justify-center mr-3">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
              </svg>
            </div>
            <div>
              <p class="font-medium text-sm">{{ notification.message }}</p>
              <p class="text-xs text-gray-500 mt-1">{{ notification.date }}</p>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Upcoming Payments -->
      <div class="card mb-8">
        <div class="flex justify-between items-center mb-6">
          <h2 class="text-xl font-bold">Upcoming Payments</h2>
          <NuxtLink to="/payments" class="text-primary-600 hover:text-primary-700 text-sm font-medium">
            View all payments
          </NuxtLink>
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
              <tr v-for="(payment, index) in upcomingPayments" :key="index">
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                  {{ payment.dueDate }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                  {{ payment.description }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">
                  ${{ payment.amount.toFixed(2) }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <span 
                    class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full" 
                    :class="{
                      'bg-warning-100 text-warning-800': payment.status === 'Due Soon',
                      'bg-error-100 text-error-800': payment.status === 'Overdue',
                      'bg-gray-100 text-gray-800': payment.status === 'Upcoming'
                    }"
                  >
                    {{ payment.status }}
                  </span>
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                  <NuxtLink to="/payments" class="text-primary-600 hover:text-primary-900">
                    Pay now
                  </NuxtLink>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      
      <!-- Recent Activity -->
      <div class="card">
        <div class="flex justify-between items-center mb-6">
          <h2 class="text-xl font-bold">Recent Activity</h2>
          <NuxtLink to="/history" class="text-primary-600 hover:text-primary-700 text-sm font-medium">
            View all activity
          </NuxtLink>
        </div>
        
        <div class="space-y-4">
          <div v-for="(activity, index) in recentActivity" :key="index" class="flex items-start p-3 rounded-lg hover:bg-gray-50">
            <div 
              class="h-10 w-10 rounded-full flex items-center justify-center mr-4"
              :class="{
                'bg-success-100 text-success-600': activity.type === 'payment',
                'bg-primary-100 text-primary-600': activity.type === 'login',
                'bg-warning-100 text-warning-600': activity.type === 'notification'
              }"
            >
              <svg v-if="activity.type === 'payment'" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
              <svg v-if="activity.type === 'login'" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 16l-4-4m0 0l4-4m-4 4h14m-5 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h7a3 3 0 013 3v1" />
              </svg>
              <svg v-if="activity.type === 'notification'" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
              </svg>
            </div>
            <div class="flex-1">
              <p class="text-sm font-medium text-gray-900">{{ activity.description }}</p>
              <p class="text-xs text-gray-500">{{ activity.time }}</p>
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