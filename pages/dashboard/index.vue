<template>
  <div class="fade-in">
    <div class="bg-white shadow">
      <div class="container-custom py-6">
        <h1 class="text-2xl font-bold text-gray-900">Dashboard</h1>
      </div>
    </div>
    
    <div class="container-custom py-8">
      <!-- Welcome section -->
      <div class="card mb-8">
        <div class="flex items-center justify-between">
          <div>
            <h2 class="text-2xl font-bold mb-2">Welcome back, John!</h2>
            <p class="text-gray-600">Here's a summary of your payment plan.</p>
          </div>
          <NuxtLink to="/payments" class="btn-primary">
            Make a payment
          </NuxtLink>
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