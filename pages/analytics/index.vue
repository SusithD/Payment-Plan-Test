<template>
  <div class="fade-in bg-gray-50">
    <!-- Enhanced Header Section -->
    <div class="bg-white shadow">
      <div class="container-custom py-4">
        <div class="flex flex-wrap items-center justify-between">
          <div class="flex items-center space-x-4 py-2">
            <div class="h-12 w-12 rounded-full bg-primary-500 text-white flex items-center justify-center text-xl font-bold">
              JD
            </div>
            <div>
              <h1 class="text-xl font-bold text-gray-900">Payment Analytics</h1>
              <div class="flex items-center">
                <span class="bg-success-100 text-success-800 text-xs px-2 py-0.5 rounded-full font-medium">
                  Financial Health Score: {{ financialHealthScore }}%
                </span>
                <span class="mx-2 text-gray-300">•</span>
                <span class="text-sm text-gray-600">May 23, 2025</span>
              </div>
            </div>
          </div>
          <div class="flex items-center space-x-3">
            <button class="p-2 rounded-full text-gray-500 hover:text-gray-700 hover:bg-gray-100">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
              </svg>
            </button>
            <div class="relative inline-block text-left">
              <button @click="downloadReport" class="btn-outline flex items-center py-1.5 px-3 text-sm">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
                </svg>
                Export Report
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Main Content Area -->
    <div class="container-custom py-8">
      <!-- Quick Stats Overview Cards -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
        <div class="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <div class="flex justify-between mb-4">
            <div>
              <p class="text-sm font-medium text-gray-500">Financial Health Score</p>
              <h3 class="text-2xl font-bold text-gray-900">{{ financialHealthScore }}%</h3>
            </div>
            <div class="h-12 w-12 rounded-full bg-success-100 flex items-center justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-success-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
          </div>
          <div class="flex justify-between text-sm">
            <span class="text-gray-500">Status:</span>
            <span class="font-medium" :class="getHealthScoreBadgeClass()">{{ getHealthScoreText() }}</span>
          </div>
          <div class="mt-4">
            <div class="w-full bg-gray-200 rounded-full h-2">
              <div class="h-2 rounded-full" :style="{ width: `${financialHealthScore}%`, backgroundColor: getHealthScoreBackground() }"></div>
            </div>
          </div>
        </div>

        <div class="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <div class="flex justify-between mb-4">
            <div>
              <p class="text-sm font-medium text-gray-500">Average Monthly Payment</p>
              <h3 class="text-2xl font-bold text-gray-900">${{ averagePayment.toFixed(2) }}</h3>
            </div>
            <div class="h-12 w-12 rounded-full bg-primary-100 flex items-center justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
          </div>
          <div class="flex justify-between text-sm">
            <span class="text-gray-500">Consistency:</span>
            <span class="font-medium text-gray-900">{{ paymentConsistency }}%</span>
          </div>
          <div class="mt-4">
            <div class="w-full bg-gray-200 rounded-full h-2">
              <div class="bg-primary-500 h-2 rounded-full" :style="{ width: `${paymentConsistency}%` }"></div>
            </div>
          </div>
        </div>

        <div class="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <div class="flex justify-between mb-4">
            <div>
              <p class="text-sm font-medium text-gray-500">Payment Plan Progress</p>
              <h3 class="text-2xl font-bold text-gray-900">{{ (completedPayments / totalPayments) * 100 }}%</h3>
            </div>
            <div class="h-12 w-12 rounded-full bg-blue-100 flex items-center justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-blue-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6" />
              </svg>
            </div>
          </div>
          <div class="flex justify-between text-sm">
            <span class="text-gray-500">Payments completed:</span>
            <span class="font-medium text-gray-900">{{ completedPayments }} of {{ totalPayments }}</span>
          </div>
          <div class="mt-4">
            <div class="w-full bg-gray-200 rounded-full h-2">
              <div class="bg-blue-500 h-2 rounded-full" :style="{ width: `${(completedPayments / totalPayments) * 100}%` }"></div>
            </div>
          </div>
        </div>
      </div>

      <!-- Main Grid Layout -->
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
        <!-- Left Column - Analytics Summary -->
        <div class="lg:col-span-1 space-y-6">
          <!-- Payment Trend Card -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="bg-gradient-to-r from-primary-500 to-primary-600 px-6 py-4">
              <div class="flex justify-between items-center">
                <h2 class="text-white font-bold text-lg">Payment Trend</h2>
                <span class="bg-white bg-opacity-20 text-white text-xs px-2.5 py-1 rounded-full">
                  Last 6 Months
                </span>
              </div>
              <div class="mt-4 mb-2">
                <div class="w-full bg-white bg-opacity-20 rounded-full h-2">
                  <div class="bg-white h-2 rounded-full" :style="{ width: `${paymentConsistency}%` }"></div>
                </div>
              </div>
            </div>
            
            <div class="px-6 py-5">
              <div class="flex items-center justify-between mb-4">
                <span class="text-gray-500 text-sm">Average Monthly Payment</span>
                <span class="font-bold text-gray-900">${{ averagePayment.toFixed(2) }}</span>
              </div>
              <div class="flex items-center justify-between">
                <div>
                  <span class="text-gray-500 text-sm">On-time</span>
                  <p class="font-bold text-success-600">{{ onTimePayments }}%</p>
                </div>
                <div class="h-8 w-px bg-gray-200"></div>
                <div>
                  <span class="text-gray-500 text-sm">Late</span>
                  <p class="font-bold text-warning-600">{{ latePercentage }}%</p>
                </div>
                <div class="h-8 w-px bg-gray-200"></div>
                <div>
                  <span class="text-gray-500 text-sm">Missed</span>
                  <p class="font-bold text-error-600">{{ missedPercentage }}%</p>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Financial Health Card -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="px-6 py-5 border-b border-gray-100">
              <div class="flex justify-between items-center">
                <h2 class="font-bold text-lg text-gray-900">Financial Health</h2>
                <span class="text-xs px-2.5 py-1 rounded-full" :class="getHealthScoreBadgeClass()">
                  {{ getHealthScoreText() }}
                </span>
              </div>
            </div>
            
            <div class="px-6 py-4">
              <div class="grid grid-cols-2 gap-4 mb-4">
                <div>
                  <span class="text-gray-500 text-sm">Total Paid</span>
                  <p class="font-semibold text-gray-900">${{ totalPaid.toFixed(2) }}</p>
                </div>
                <div>
                  <span class="text-gray-500 text-sm">Remaining Balance</span>
                  <p class="font-semibold text-gray-900">${{ remainingBalance.toFixed(2) }}</p>
                </div>
                <div>
                  <span class="text-gray-500 text-sm">Payments Made</span>
                  <p class="font-semibold text-gray-900">{{ completedPayments }} of {{ totalPayments }}</p>
                </div>
                <div>
                  <span class="text-gray-500 text-sm">Next Payment</span>
                  <p class="font-semibold text-gray-900">${{ monthlyPayment.toFixed(2) }}</p>
                </div>
              </div>
              
              <div class="mb-4">
                <span class="text-gray-500 text-sm block mb-1">Financial Health Score</span>
                <div class="w-full bg-gray-200 rounded-full h-3">
                  <div class="h-3 rounded-full" :style="{ width: `${financialHealthScore}%`, backgroundColor: getHealthScoreBackground() }"></div>
                </div>
              </div>
              
              <div class="mt-3">
                <NuxtLink to="/history" class="text-primary-600 text-sm font-medium hover:text-primary-700 inline-flex items-center">
                  View payment history
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                  </svg>
                </NuxtLink>
              </div>
            </div>
          </div>
          
          <!-- Insights Card -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="px-6 py-5 border-b border-gray-100">
              <div class="flex justify-between items-center">
                <h2 class="font-bold text-lg text-gray-900">Financial Insights</h2>
              </div>
            </div>
            
            <div class="divide-y divide-gray-100">
              <div v-for="(insight, index) in financialInsights" :key="index" class="px-6 py-4 flex items-start">
                <span class="h-8 w-8 rounded-full flex items-center justify-center mr-3 flex-shrink-0" :class="insight.color">
                  <svg v-if="insight.type === 'positive'" xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                  </svg>
                  <svg v-if="insight.type === 'warning'" xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
                  </svg>
                  <svg v-if="insight.type === 'tip'" xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                </span>
                <div class="min-w-0 flex-1">
                  <p class="text-sm text-gray-900 font-medium">{{ insight.text }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Right Column - Charts and Recommendations -->
        <div class="lg:col-span-2 space-y-6">
          <!-- Action Cards -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 p-6">
            <div class="flex justify-between items-center mb-6">
              <h2 class="font-bold text-lg text-gray-900">Quick Analytics</h2>
            </div>
            
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
              <button @click="activeChartTab = 'payments'" class="flex flex-col items-center justify-center rounded-lg p-4 transition-colors" :class="activeChartTab === 'payments' ? 'bg-primary-50 hover:bg-primary-100' : 'bg-gray-50 hover:bg-gray-100'">
                <div class="h-10 w-10 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mb-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                </div>
                <span class="text-sm font-medium text-gray-900">Payment Amounts</span>
              </button>
              
              <button @click="activeChartTab = 'timeliness'" class="flex flex-col items-center justify-center rounded-lg p-4 transition-colors" :class="activeChartTab === 'timeliness' ? 'bg-blue-50 hover:bg-blue-100' : 'bg-gray-50 hover:bg-gray-100'">
                <div class="h-10 w-10 bg-blue-100 text-blue-600 rounded-full flex items-center justify-center mb-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                </div>
                <span class="text-sm font-medium text-gray-900">Payment Timeliness</span>
              </button>
              
              <button @click="activeChartTab = 'balance'" class="flex flex-col items-center justify-center rounded-lg p-4 transition-colors" :class="activeChartTab === 'balance' ? 'bg-green-50 hover:bg-green-100' : 'bg-gray-50 hover:bg-gray-100'">
                <div class="h-10 w-10 bg-green-100 text-green-600 rounded-full flex items-center justify-center mb-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6" />
                  </svg>
                </div>
                <span class="text-sm font-medium text-gray-900">Balance Trends</span>
              </button>
              
              <button @click="activeChartTab = 'methods'" class="flex flex-col items-center justify-center rounded-lg p-4 transition-colors" :class="activeChartTab === 'methods' ? 'bg-purple-50 hover:bg-purple-100' : 'bg-gray-50 hover:bg-gray-100'">
                <div class="h-10 w-10 bg-purple-100 text-purple-600 rounded-full flex items-center justify-center mb-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
                  </svg>
                </div>
                <span class="text-sm font-medium text-gray-900">Payment Methods</span>
              </button>
            </div>
          </div>
          
          <!-- Payment Projection Alert -->
          <div class="bg-gradient-to-r from-amber-50 to-amber-100 rounded-xl shadow-sm overflow-hidden border border-amber-200">
            <div class="p-6">
              <div class="flex">
                <div class="flex-shrink-0">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-amber-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                </div>
                <div class="ml-3">
                  <h3 class="text-sm font-medium text-amber-800">
                    Payment Projection
                  </h3>
                  <div class="mt-2 text-sm text-amber-700">
                    <p>Based on your current payment rate, you'll complete your payments by {{ projectedCompletionDate }} ({{ remainingPayments }} payments remaining).</p>
                  </div>
                  <div class="mt-3">
                    <div class="flex space-x-3">
                      <button
                        type="button"
                        class="inline-flex items-center px-3 py-1.5 border border-transparent text-xs font-medium rounded-md shadow-sm text-white bg-amber-600 hover:bg-amber-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-amber-500"
                      >
                        Optimize my plan
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Main Chart Card -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="px-6 py-5 border-b border-gray-100">
              <div class="flex justify-between items-center">
                <h2 class="font-bold text-lg text-gray-900">
                  {{ getChartTitle() }}
                </h2>
                <div class="flex items-center space-x-3">
                  <button @click="chartPeriod = 'monthly'" class="text-sm px-3 py-1 rounded-md" :class="chartPeriod === 'monthly' ? 'bg-primary-50 text-primary-700' : 'text-gray-500 hover:bg-gray-100'">
                    Monthly
                  </button>
                  <button @click="chartPeriod = 'quarterly'" class="text-sm px-3 py-1 rounded-md" :class="chartPeriod === 'quarterly' ? 'bg-primary-50 text-primary-700' : 'text-gray-500 hover:bg-gray-100'">
                    Quarterly
                  </button>
                  <button @click="chartPeriod = 'yearly'" class="text-sm px-3 py-1 rounded-md" :class="chartPeriod === 'yearly' ? 'bg-primary-50 text-primary-700' : 'text-gray-500 hover:bg-gray-100'">
                    Yearly
                  </button>
                </div>
              </div>
            </div>
            
            <div class="p-6">
              <!-- Chart display area -->
              <div class="h-80 bg-gray-50 rounded-lg flex items-center justify-center">
                <div v-if="activeChartTab === 'payments'" class="w-full h-full px-4 py-6">
                  <!-- Payment amount chart (simple mockup) -->
                  <div class="h-full flex items-end">
                    <div v-for="(month, i) in chartData" :key="i" class="flex-1 flex flex-col items-center justify-end h-full">
                      <div class="w-4/5 bg-primary-500 rounded-t-sm" :style="{ height: `${(month.amount / maxChartAmount) * 100}%` }"></div>
                      <span class="text-xs text-gray-500 mt-2">{{ month.label }}</span>
                    </div>
                  </div>
                </div>
                
                <div v-else-if="activeChartTab === 'timeliness'" class="w-full h-full px-4 py-6">
                  <!-- Payment timeliness chart (simple mockup) -->
                  <div class="h-full flex items-end">
                    <div v-for="(month, i) in chartData" :key="i" class="flex-1 flex flex-col items-center justify-end h-full">
                      <div class="w-4/5 rounded-t-sm flex flex-col">
                        <div class="bg-success-500" :style="{ height: `${month.onTime * 80}px` }"></div>
                        <div class="bg-warning-500" :style="{ height: `${month.late * 80}px` }"></div>
                        <div class="bg-error-500" :style="{ height: `${month.missed * 80}px` }"></div>
                      </div>
                      <span class="text-xs text-gray-500 mt-2">{{ month.label }}</span>
                    </div>
                  </div>
                </div>
                
                <div v-else-if="activeChartTab === 'balance'" class="w-full h-full px-4 py-6">
                  <!-- Balance reduction chart (simple mockup with line) -->
                  <div class="h-full relative">
                    <div class="absolute inset-0 flex items-end">
                      <div v-for="(month, i) in chartData" :key="i" class="flex-1 flex flex-col items-center">
                        <div class="w-2 h-2 rounded-full bg-blue-500 z-10"></div>
                        <div v-if="i < chartData.length - 1" class="absolute h-[2px] bg-blue-500" 
                          :style="{
                            left: `${(i * 100 / (chartData.length - 1)) + (50 / chartData.length)}%`,
                            width: `${100 / chartData.length}%`,
                            bottom: `${(month.balance / maxBalance) * 100}%`,
                            transform: `rotate(${Math.atan2(
                              (chartData[i+1].balance - month.balance) / maxBalance * 100,
                              100 / chartData.length
                            )}rad)`,
                            transformOrigin: 'left bottom'
                          }">
                        </div>
                      </div>
                    </div>
                    <div class="absolute bottom-0 left-0 w-full border-t border-gray-200"></div>
                    <div class="absolute bottom-8 left-0 right-0 flex justify-between">
                      <span v-for="(month, i) in chartData" :key="i" class="text-xs text-gray-500">
                        {{ month.label }}
                      </span>
                    </div>
                  </div>
                </div>
                
                <div v-else class="w-full h-full px-4 py-6">
                  <!-- Payment methods chart -->
                  <div class="grid grid-cols-1 md:grid-cols-2 gap-6 h-full">
                    <div class="flex flex-col justify-center">
                      <div class="space-y-4">
                        <div v-for="(method, index) in paymentMethods" :key="index" class="flex items-center">
                          <div class="w-2 h-10 rounded-l-md" :style="{ backgroundColor: method.color }"></div>
                          <div class="flex-1 bg-gray-50 p-3 rounded-r-md">
                            <div class="flex justify-between items-center mb-1">
                              <span class="text-sm font-medium text-gray-700">{{ method.name }}</span>
                              <span class="text-sm font-medium text-gray-700">{{ method.percentage }}%</span>
                            </div>
                            <div class="w-full bg-gray-200 rounded-full h-2">
                              <div class="h-2 rounded-full" :style="{ width: `${method.percentage}%`, backgroundColor: method.color }"></div>
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                    <div class="flex items-center justify-center">
                      <!-- Simple pie chart mockup -->
                      <div class="aspect-square relative" style="width: 180px;">
                        <svg viewBox="0 0 100 100" class="w-full h-full">
                          <!-- Credit Card - Purple slice (65%) -->
                          <path d="M 50 50 L 50 0 A 50 50 0 0 1 97.6 65.5 Z" fill="#8B5CF6"></path>
                          <!-- Bank Transfer - Green slice (25%) -->
                          <path d="M 50 50 L 97.6 65.5 A 50 50 0 0 1 27.3 96.6 Z" fill="#10B981"></path>
                          <!-- PayPal - Blue slice (10%) -->
                          <path d="M 50 50 L 27.3 96.6 A 50 50 0 0 1 50 0 Z" fill="#3B82F6"></path>
                        </svg>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Chart summary -->
            <div class="px-6 py-5 bg-gray-50 border-t border-gray-100">
              <div class="grid grid-cols-3 gap-4">
                <div class="text-center">
                  <p class="text-sm text-gray-500 mb-1">Total Paid</p>
                  <p class="text-lg font-bold text-primary-700">${{ totalPaid.toFixed(2) }}</p>
                </div>
                <div class="text-center">
                  <p class="text-sm text-gray-500 mb-1">Avg. Payment</p>
                  <p class="text-lg font-bold text-primary-700">${{ averagePayment.toFixed(2) }}</p>
                </div>
                <div class="text-center">
                  <p class="text-sm text-gray-500 mb-1">Remaining</p>
                  <p class="text-lg font-bold text-blue-700">${{ remainingBalance.toFixed(2) }}</p>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Recommendations Card -->
          <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
            <div class="px-6 py-5 border-b border-gray-100">
              <div class="flex justify-between items-center">
                <h2 class="font-bold text-lg text-gray-900">Smart Recommendations</h2>
              </div>
            </div>
            
            <div class="p-6">
              <div class="relative">
                <div class="absolute inset-0 flex items-center" aria-hidden="true">
                  <div class="w-full border-t border-gray-200"></div>
                </div>
                <div class="relative flex justify-center">
                  <span class="px-3 bg-white text-sm text-gray-500">Based on your payment patterns</span>
                </div>
              </div>
              
              <div class="mt-6 grid grid-cols-1 md:grid-cols-2 gap-6">
                <div v-for="(recommendation, index) in recommendations.slice(0, 2)" :key="index" 
                  class="border border-gray-200 rounded-lg p-5" :class="recommendation.bgColor">
                  <div class="flex items-start">
                    <div class="flex-shrink-0 h-10 w-10 rounded-full flex items-center justify-center mr-4" :class="recommendation.iconBg">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" :class="recommendation.iconColor" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" :d="recommendation.icon" />
                      </svg>
                    </div>
                    <div>
                      <h3 class="font-medium mb-1" :class="recommendation.textColor">{{ recommendation.title }}</h3>
                      <p class="text-sm mb-2" :class="recommendation.descColor">{{ recommendation.description }}</p>
                      <button v-if="recommendation.action" class="text-sm font-medium flex items-center" :class="recommendation.actionColor">
                        {{ recommendation.action }}
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                        </svg>
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Report Generation Modal -->
    <div 
      v-if="showReportModal" 
      class="fixed inset-0 bg-gray-900 bg-opacity-50 flex items-center justify-center z-50 fade-in"
    >
      <div class="bg-white rounded-xl p-6 shadow-xl w-full max-w-xl mx-4 overflow-y-auto" style="max-height: 90vh;">
        <div class="flex justify-between items-center mb-4">
          <h3 class="text-lg font-bold">Generate Payment Analytics Report</h3>
          <button @click="cancelReportGeneration" class="text-gray-400 hover:text-gray-500" :disabled="isGeneratingReport">
            <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
        
        <div class="space-y-6">
          <!-- Report Format Selection -->
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">Report Format</label>
            <div class="grid grid-cols-3 gap-3">
              <label :class="[
                'cursor-pointer border rounded-lg p-3 flex flex-col items-center justify-center',
                reportFormat === 'pdf' ? 'border-primary-500 bg-primary-50' : 'border-gray-200 hover:bg-gray-50'
              ]">
                <input type="radio" v-model="reportFormat" value="pdf" class="sr-only" />
                <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 mb-2" :class="reportFormat === 'pdf' ? 'text-primary-600' : 'text-gray-400'" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                </svg>
                <span class="text-sm font-medium" :class="reportFormat === 'pdf' ? 'text-primary-700' : 'text-gray-700'">PDF</span>
              </label>
              
              <label :class="[
                'cursor-pointer border rounded-lg p-3 flex flex-col items-center justify-center',
                reportFormat === 'excel' ? 'border-primary-500 bg-primary-50' : 'border-gray-200 hover:bg-gray-50'
              ]">
                <input type="radio" v-model="reportFormat" value="excel" class="sr-only" />
                <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 mb-2" :class="reportFormat === 'excel' ? 'text-primary-600' : 'text-gray-400'" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
                </svg>
                <span class="text-sm font-medium" :class="reportFormat === 'excel' ? 'text-primary-700' : 'text-gray-700'">Excel</span>
              </label>
              
              <label :class="[
                'cursor-pointer border rounded-lg p-3 flex flex-col items-center justify-center',
                reportFormat === 'csv' ? 'border-primary-500 bg-primary-50' : 'border-gray-200 hover:bg-gray-50'
              ]">
                <input type="radio" v-model="reportFormat" value="csv" class="sr-only" />
                <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 mb-2" :class="reportFormat === 'csv' ? 'text-primary-600' : 'text-gray-400'" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                </svg>
                <span class="text-sm font-medium" :class="reportFormat === 'csv' ? 'text-primary-700' : 'text-gray-700'">CSV</span>
              </label>
            </div>
          </div>
          
          <!-- Time Period Selection -->
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">Time Period</label>
            <select v-model="reportTimePeriod" class="block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-primary-500 focus:border-primary-500 sm:text-sm rounded-md">
              <option value="3months">Last 3 Months</option>
              <option value="6months">Last 6 Months</option>
              <option value="1year">Last 12 Months</option>
              <option value="all">All Time</option>
              <option value="custom">Custom Range</option>
            </select>
          </div>
          
          <!-- Report Sections -->
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-2">Report Sections</label>
            <div class="bg-gray-50 rounded-lg p-4 space-y-2">
              <div class="flex items-center">
                <input id="payment-summary" type="checkbox" v-model="reportSections.paymentSummary" class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded">
                <label for="payment-summary" class="ml-2 block text-sm text-gray-700">Payment Summary</label>
              </div>
              <div class="flex items-center">
                <input id="payment-history" type="checkbox" v-model="reportSections.paymentHistory" class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded">
                <label for="payment-history" class="ml-2 block text-sm text-gray-700">Payment History</label>
              </div>
              <div class="flex items-center">
                <input id="financial-health" type="checkbox" v-model="reportSections.financialHealth" class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded">
                <label for="financial-health" class="ml-2 block text-sm text-gray-700">Financial Health Analysis</label>
              </div>
              <div class="flex items-center">
                <input id="payment-analytics" type="checkbox" v-model="reportSections.paymentAnalytics" class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded">
                <label for="payment-analytics" class="ml-2 block text-sm text-gray-700">Payment Analytics</label>
              </div>
              <div class="flex items-center">
                <input id="recommendations" type="checkbox" v-model="reportSections.recommendations" class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded">
                <label for="recommendations" class="ml-2 block text-sm text-gray-700">Recommendations</label>
              </div>
            </div>
          </div>
          
          <!-- Include Charts -->
          <div class="flex items-center">
            <input id="include-charts" type="checkbox" v-model="includeCharts" class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded">
            <label for="include-charts" class="ml-2 block text-sm text-gray-700">Include Visualizations & Charts</label>
          </div>
          
          <!-- Preview -->
          <div class="border border-gray-200 rounded-lg p-4">
            <h4 class="text-sm font-medium text-gray-700 mb-2">Report Preview</h4>
            <div class="bg-gray-100 rounded-md p-3 space-y-2">
              <div class="flex justify-between text-xs">
                <span class="text-gray-600">Format:</span>
                <span class="font-medium">{{ reportFormat.toUpperCase() }}</span>
              </div>
              <div class="flex justify-between text-xs">
                <span class="text-gray-600">Time Period:</span>
                <span class="font-medium">{{ 
                  reportTimePeriod === '3months' ? 'Last 3 Months' :
                  reportTimePeriod === '6months' ? 'Last 6 Months' :
                  reportTimePeriod === '1year' ? 'Last 12 Months' :
                  reportTimePeriod === 'all' ? 'All Time' : 'Custom Range'
                }}</span>
              </div>
              <div class="flex justify-between text-xs">
                <span class="text-gray-600">Sections:</span>
                <span class="font-medium">{{ Object.values(reportSections).filter(Boolean).length }} selected</span>
              </div>
              <div class="flex justify-between text-xs">
                <span class="text-gray-600">Charts:</span>
                <span class="font-medium">{{ includeCharts ? 'Included' : 'Not included' }}</span>
              </div>
              <div class="flex justify-between text-xs">
                <span class="text-gray-600">Estimated Size:</span>
                <span class="font-medium">{{ 
                  reportFormat === 'pdf' ? '2.4 MB' :
                  reportFormat === 'excel' ? '1.8 MB' : '0.9 MB'
                }}</span>
              </div>
            </div>
          </div>
        </div>
        
        <div class="mt-6 flex justify-end space-x-3">
          <button 
            @click="cancelReportGeneration" 
            class="btn-outline"
            :disabled="isGeneratingReport"
          >
            Cancel
          </button>
          <button 
            @click="generateReport" 
            class="btn-primary flex items-center"
            :disabled="isGeneratingReport"
          >
            <svg v-if="isGeneratingReport" class="animate-spin -ml-1 mr-2 h-4 w-4 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
              <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
              <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
            </svg>
            {{ isGeneratingReport ? 'Generating...' : 'Generate Report' }}
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

// Analytics settings state
const timePeriod = ref('6months');
const chartType = ref('bar');
const dataGrouping = ref('monthly');
const chartPeriod = ref('monthly');
const activeChartTab = ref('payments');

// Report generation state
const showReportModal = ref(false);
const reportFormat = ref('pdf');
const reportTimePeriod = ref('6months');
const reportSections = ref({
  paymentSummary: true,
  paymentHistory: true,
  financialHealth: true,
  paymentAnalytics: true,
  recommendations: true
});
const includeCharts = ref(true);
const isGeneratingReport = ref(false);

// Payment statistics
const averagePayment = ref(250);
const paymentConsistency = ref(88);
const onTimePayments = ref(75);
const missedPayments = ref(2);
const latePayments = ref(3);
const totalPaid = ref(2500);
const remainingBalance = ref(2500);
const monthlyPayment = ref(250);
const remainingPayments = ref(10);
const totalPayments = ref(20);
const completedPayments = ref(10);
const paymentRate = ref(1);
const paymentRateTrend = ref('stable');
const financialHealthScore = ref(85);
const projectedCompletionDate = ref('Jan 15, 2026');
const latePercentage = ref(20);
const missedPercentage = ref(5);

// Monthly data for the bar chart
const monthlyData = ref([
  { name: 'Dec', amount: 250, onTimePercentage: 100 },
  { name: 'Jan', amount: 250, onTimePercentage: 100 },
  { name: 'Feb', amount: 250, onTimePercentage: 100 },
  { name: 'Mar', amount: 250, onTimePercentage: 100 },
  { name: 'Apr', amount: 250, onTimePercentage: 80 },
  { name: 'May', amount: 250, onTimePercentage: 50 }
]);

// Chart data
const chartData = ref([
  { label: 'Dec', amount: 250, onTime: 1, late: 0, missed: 0, balance: 3000 },
  { label: 'Jan', amount: 250, onTime: 1, late: 0, missed: 0, balance: 2750 },
  { label: 'Feb', amount: 250, onTime: 1, late: 0, missed: 0, balance: 2500 },
  { label: 'Mar', amount: 250, onTime: 1, late: 0, missed: 0, balance: 2250 },
  { label: 'Apr', amount: 250, onTime: 0, late: 1, missed: 0, balance: 2000 },
  { label: 'May', amount: 250, onTime: 0, late: 0, missed: 1, balance: 1750 }
]);

// Payment methods data
const paymentMethods = ref([
  { name: 'Credit Card', percentage: 65, color: '#8B5CF6' },
  { name: 'Bank Transfer', percentage: 25, color: '#10B981' },
  { name: 'PayPal', percentage: 10, color: '#3B82F6' }
]);

// Financial insights
const financialInsights = ref([
  { 
    type: 'positive', 
    text: 'Your payment consistency has improved by 12% over the last 3 months.',
    color: 'bg-success-100 text-success-800'
  },
  { 
    type: 'warning', 
    text: 'You\'ve had 1 late payment in the last 2 months. This could affect your financial score.',
    color: 'bg-warning-100 text-warning-800'
  },
  { 
    type: 'tip', 
    text: 'Setting up automatic payments could help you maintain a perfect payment record.',
    color: 'bg-blue-100 text-blue-800'
  }
]);

// Recommendations
const recommendations = ref([
  {
    title: 'Increase your monthly payment',
    description: 'Adding just $50 to your monthly payment would save you $120 in interest and pay off your balance 2 months earlier.',
    action: 'Adjust payment plan',
    icon: 'M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z',
    bgColor: 'bg-success-50',
    iconBg: 'bg-success-100',
    iconColor: 'text-success-600',
    textColor: 'text-success-800',
    descColor: 'text-success-600',
    actionColor: 'text-success-700 hover:text-success-800'
  },
  {
    title: 'Set up automatic payments',
    description: 'Avoid late fees and maintain a consistent payment record by setting up automatic payments.',
    action: 'Enable autopay',
    icon: 'M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z',
    bgColor: 'bg-primary-50',
    iconBg: 'bg-primary-100',
    iconColor: 'text-primary-600',
    textColor: 'text-primary-800',
    descColor: 'text-primary-600',
    actionColor: 'text-primary-700 hover:text-primary-800'
  },
  {
    title: 'Consider refinancing options',
    description: 'Based on your payment history, you might qualify for a lower interest rate.',
    action: 'Explore options',
    icon: 'M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z',
    bgColor: 'bg-blue-50',
    iconBg: 'bg-blue-100',
    iconColor: 'text-blue-600',
    textColor: 'text-blue-800',
    descColor: 'text-blue-600',
    actionColor: 'text-blue-700 hover:text-blue-800'
  }
]);

// Computed values
const maxMonthlyAmount = computed(() => {
  return Math.max(...monthlyData.value.map(month => month.amount)) * 1.1;
});

const maxChartAmount = computed(() => {
  return Math.max(...chartData.value.map(data => data.amount)) * 1.1;
});

const maxBalance = computed(() => {
  return Math.max(...chartData.value.map(data => data.balance));
});

// Methods
const getHealthScoreBackground = () => {
  if (financialHealthScore.value >= 80) return '#10B981';
  if (financialHealthScore.value >= 60) return '#F59E0B';
  return '#EF4444';
};

const getHealthScoreBadgeClass = () => {
  if (financialHealthScore.value >= 80) return 'bg-success-100 text-success-800';
  if (financialHealthScore.value >= 60) return 'bg-warning-100 text-warning-800';
  return 'bg-error-100 text-error-800';
};

const getHealthScoreText = () => {
  if (financialHealthScore.value >= 80) return 'Excellent';
  if (financialHealthScore.value >= 60) return 'Good';
  return 'Needs Improvement';
};

const getChartTitle = () => {
  switch (activeChartTab) {
    case 'payments': return 'Payment Amount Analysis';
    case 'timeliness': return 'Payment Timeliness Analysis';
    case 'balance': return 'Balance Reduction Analysis';
    case 'methods': return 'Payment Methods Analysis';
    default: return 'Payment Analysis';
  }
};

const downloadReport = () => {
  showReportModal.value = true;
};

const generateReport = () => {
  isGeneratingReport.value = true;
  
  // Simulate report generation delay
  setTimeout(() => {
    isGeneratingReport.value = false;
    
    // For demo purposes, show success message
    alert(`Report successfully generated in ${reportFormat.value.toUpperCase()} format!`);
    showReportModal.value = false;
    
    // In a real application, this would trigger a file download
    console.log('Report generated with settings:', {
      format: reportFormat.value,
      timePeriod: reportTimePeriod.value,
      sections: Object.keys(reportSections.value).filter(key => reportSections.value[key]),
      includeCharts: includeCharts.value
    });
  }, 2000);
};

const cancelReportGeneration = () => {
  showReportModal.value = false;
};

onMounted(() => {
  // In a real app, this would fetch the initial analytics data
  console.log('Analytics page mounted');
});
</script>