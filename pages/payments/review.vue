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
                <!-- Credit Card Category -->
                <div class="border rounded-lg overflow-hidden"
                     :class="{ 'border-primary-500 bg-primary-50': selectedPaymentCategory === 'credit-card', 'border-gray-200': selectedPaymentCategory !== 'credit-card' }">
                  <div class="p-4 cursor-pointer" @click="toggleCategory('credit-card')">
                    <div class="flex items-center justify-between">
                      <div class="flex items-center">
                        <div class="h-8 w-8 flex items-center justify-center mr-3">
                          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
                          </svg>
                        </div>
                        <div>
                          <h4 class="font-medium">Credit Cards</h4>
                          <p class="text-xs text-gray-500">{{ getCategoryCount('creditCards') }} cards available</p>
                        </div>
                      </div>
                      <div class="flex items-center">
                        <div class="h-5 w-5 rounded-full border-2 mr-3"
                             :class="{ 'border-primary-500': selectedPaymentCategory === 'credit-card', 'border-gray-300': selectedPaymentCategory !== 'credit-card' }">
                          <div v-if="selectedPaymentCategory === 'credit-card'" class="h-3 w-3 m-0.5 rounded-full bg-primary-500"></div>
                        </div>
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400 transition-transform duration-200"
                             :class="{ 'rotate-180': expandedCategory === 'credit-card' }" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                        </svg>
                      </div>
                    </div>
                  </div>
                  
                  <!-- Expanded Credit Card Options -->
                  <div v-if="expandedCategory === 'credit-card'" class="border-t border-gray-200 bg-gray-50">
                    <div class="p-4 space-y-3">
                      <div v-for="card in paymentMethods.creditCards" :key="card.id" 
                           class="bg-white border rounded-lg p-3 cursor-pointer hover:bg-gray-50 transition-colors"
                           :class="{ 'border-primary-500 bg-primary-50': selectedPaymentMethod === card.id, 'border-gray-200': selectedPaymentMethod !== card.id }"
                           @click="selectPaymentMethod(card.id, 'credit-card')">
                        <div class="flex items-center justify-between">
                          <div class="flex items-center">
                            <div class="h-8 w-8 flex items-center justify-center mr-3">
                              <img v-if="card.brand === 'visa'" src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzIiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAzMiAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHJlY3Qgd2lkdGg9IjMyIiBoZWlnaHQ9IjI0IiByeD0iNCIgZmlsbD0iIzE0MzQ5QyIvPgo8dGV4dCB4PSI1IiB5PSIxNSIgZm9udC1mYW1pbHk9IkFyaWFsIiBmb250LXNpemU9IjhweCIgZmlsbD0id2hpdGUiPiVWaXNhPC90ZXh0Pgo8L3N2Zz4K" class="h-6" alt="Visa">
                              <img v-else-if="card.brand === 'mastercard'" src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzIiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAzMiAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHJlY3Qgd2lkdGg9IjMyIiBoZWlnaHQ9IjI0IiByeD0iNCIgZmlsbD0iI0VCMDAxQiIvPgo8dGV4dCB4PSI1IiB5PSIxNSIgZm9udC1mYW1pbHk9IkFyaWFsIiBmb250LXNpemU9IjZweCIgZmlsbD0id2hpdGUiPk1hc3RlckNhcmQ8L3RleHQ+Cjwvc3ZnPgo=" class="h-6" alt="MasterCard">
                              <div v-else class="h-6 w-6 rounded bg-gray-300 flex items-center justify-center text-xs text-gray-600">CC</div>
                            </div>
                            <div>
                              <p class="text-sm font-medium">{{ card.name }}</p>
                              <p class="text-xs text-gray-500">{{ card.details }}</p>
                            </div>
                          </div>
                          <div class="h-4 w-4 rounded-full border-2"
                               :class="{ 'border-primary-500': selectedPaymentMethod === card.id, 'border-gray-300': selectedPaymentMethod !== card.id }">
                            <div v-if="selectedPaymentMethod === card.id" class="h-2 w-2 m-0.5 rounded-full bg-primary-500"></div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Debit Card Category -->
                <div class="border rounded-lg overflow-hidden"
                     :class="{ 'border-primary-500 bg-primary-50': selectedPaymentCategory === 'debit-card', 'border-gray-200': selectedPaymentCategory !== 'debit-card' }">
                  <div class="p-4 cursor-pointer" @click="toggleCategory('debit-card')">
                    <div class="flex items-center justify-between">
                      <div class="flex items-center">
                        <div class="h-8 w-8 flex items-center justify-center mr-3">
                          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
                          </svg>
                        </div>
                        <div>
                          <h4 class="font-medium">Debit Cards</h4>
                          <p class="text-xs text-gray-500">{{ getCategoryCount('debitCards') }} cards available</p>
                        </div>
                      </div>
                      <div class="flex items-center">
                        <div class="h-5 w-5 rounded-full border-2 mr-3"
                             :class="{ 'border-primary-500': selectedPaymentCategory === 'debit-card', 'border-gray-300': selectedPaymentCategory !== 'debit-card' }">
                          <div v-if="selectedPaymentCategory === 'debit-card'" class="h-3 w-3 m-0.5 rounded-full bg-primary-500"></div>
                        </div>
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400 transition-transform duration-200"
                             :class="{ 'rotate-180': expandedCategory === 'debit-card' }" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                        </svg>
                      </div>
                    </div>
                  </div>
                  
                  <!-- Expanded Debit Card Options -->
                  <div v-if="expandedCategory === 'debit-card'" class="border-t border-gray-200 bg-gray-50">
                    <div class="p-4 space-y-3">
                      <div v-for="card in paymentMethods.debitCards" :key="card.id" 
                           class="bg-white border rounded-lg p-3 cursor-pointer hover:bg-gray-50 transition-colors"
                           :class="{ 'border-primary-500 bg-primary-50': selectedPaymentMethod === card.id, 'border-gray-200': selectedPaymentMethod !== card.id }"
                           @click="selectPaymentMethod(card.id, 'debit-card')">
                        <div class="flex items-center justify-between">
                          <div class="flex items-center">
                            <div class="h-8 w-8 flex items-center justify-center mr-3">
                              <img v-if="card.brand === 'visa'" src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzIiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAzMiAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHJlY3Qgd2lkdGg9IjMyIiBoZWlnaHQ9IjI0IiByeD0iNCIgZmlsbD0iIzE0MzQ5QyIvPgo8dGV4dCB4PSI1IiB5PSIxNSIgZm9udC1mYW1pbHk9IkFyaWFsIiBmb250LXNpemU9IjhweCIgZmlsbD0id2hpdGUiPiVWaXNhPC90ZXh0Pgo8L3N2Zz4K" class="h-6" alt="Visa">
                              <img v-else-if="card.brand === 'mastercard'" src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzIiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAzMiAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHJlY3Qgd2lkdGg9IjMyIiBoZWlnaHQ9IjI0IiByeD0iNCIgZmlsbD0iI0VCMDAxQiIvPgo8dGV4dCB4PSI1IiB5PSIxNSIgZm9udC1mYW1pbHk9IkFyaWFsIiBmb250LXNpemU9IjZweCIgZmlsbD0id2hpdGUiPk1hc3RlckNhcmQ8L3RleHQ+Cjwvc3ZnPgo=" class="h-6" alt="MasterCard">
                              <div v-else class="h-6 w-6 rounded bg-green-100 flex items-center justify-center text-xs text-green-600 font-medium">DB</div>
                            </div>
                            <div>
                              <p class="text-sm font-medium">{{ card.name }}</p>
                              <p class="text-xs text-gray-500">{{ card.details }}</p>
                            </div>
                          </div>
                          <div class="h-4 w-4 rounded-full border-2"
                               :class="{ 'border-primary-500': selectedPaymentMethod === card.id, 'border-gray-300': selectedPaymentMethod !== card.id }">
                            <div v-if="selectedPaymentMethod === card.id" class="h-2 w-2 m-0.5 rounded-full bg-primary-500"></div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Bank Transfer Category -->
                <div class="border rounded-lg overflow-hidden"
                     :class="{ 'border-primary-500 bg-primary-50': selectedPaymentCategory === 'bank-transfer', 'border-gray-200': selectedPaymentCategory !== 'bank-transfer' }">
                  <div class="p-4 cursor-pointer" @click="toggleCategory('bank-transfer')">
                    <div class="flex items-center justify-between">
                      <div class="flex items-center">
                        <div class="h-8 w-8 flex items-center justify-center mr-3">
                          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4" />
                          </svg>
                        </div>
                        <div>
                          <h4 class="font-medium">Bank Transfer</h4>
                          <p class="text-xs text-gray-500">{{ getCategoryCount('bankTransfers') }} accounts available</p>
                        </div>
                      </div>
                      <div class="flex items-center">
                        <div class="h-5 w-5 rounded-full border-2 mr-3"
                             :class="{ 'border-primary-500': selectedPaymentCategory === 'bank-transfer', 'border-gray-300': selectedPaymentCategory !== 'bank-transfer' }">
                          <div v-if="selectedPaymentCategory === 'bank-transfer'" class="h-3 w-3 m-0.5 rounded-full bg-primary-500"></div>
                        </div>
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400 transition-transform duration-200"
                             :class="{ 'rotate-180': expandedCategory === 'bank-transfer' }" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                        </svg>
                      </div>
                    </div>
                  </div>
                  
                  <!-- Expanded Bank Transfer Options -->
                  <div v-if="expandedCategory === 'bank-transfer'" class="border-t border-gray-200 bg-gray-50">
                    <div class="p-4 space-y-3">
                      <div v-for="bank in paymentMethods.bankTransfers" :key="bank.id" 
                           class="bg-white border rounded-lg p-3 cursor-pointer hover:bg-gray-50 transition-colors"
                           :class="{ 'border-primary-500 bg-primary-50': selectedPaymentMethod === bank.id, 'border-gray-200': selectedPaymentMethod !== bank.id }"
                           @click="selectPaymentMethod(bank.id, 'bank-transfer')">
                        <div class="flex items-center justify-between">
                          <div class="flex items-center">
                            <div class="h-8 w-8 flex items-center justify-center mr-3">
                              <div class="h-6 w-6 rounded bg-blue-100 flex items-center justify-center text-xs text-blue-600 font-medium">{{ bank.bankCode }}</div>
                            </div>
                            <div>
                              <p class="text-sm font-medium">{{ bank.name }}</p>
                              <p class="text-xs text-gray-500">{{ bank.details }}</p>
                            </div>
                          </div>
                          <div class="h-4 w-4 rounded-full border-2"
                               :class="{ 'border-primary-500': selectedPaymentMethod === bank.id, 'border-gray-300': selectedPaymentMethod !== bank.id }">
                            <div v-if="selectedPaymentMethod === bank.id" class="h-2 w-2 m-0.5 rounded-full bg-primary-500"></div>
                          </div>
                        </div>
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
const selectedPaymentCategory = ref(null);
const expandedCategory = ref(null);

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
const paymentMethods = ref({
  creditCards: [
    {
      id: 1,
      name: 'Visa ending in 4242',
      details: 'Expires 12/25',
      brand: 'visa'
    },
    {
      id: 2,
      name: 'MasterCard ending in 1234',
      details: 'Expires 11/24',
      brand: 'mastercard'
    }
  ],
  debitCards: [
    {
      id: 3,
      name: 'Visa Debit ending in 5678',
      details: 'Expires 12/23',
      brand: 'visa'
    },
    {
      id: 4,
      name: 'MasterCard Debit ending in 9101',
      details: 'Expires 11/22',
      brand: 'mastercard'
    }
  ],
  bankTransfers: [
    {
      id: 5,
      name: 'Bank of America',
      details: 'Account ending in 5678',
      bankCode: 'BOA'
    },
    {
      id: 6,
      name: 'Chase Bank',
      details: 'Account ending in 9101',
      bankCode: 'CHASE'
    }
  ]
});

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

// Method to toggle category expansion
const toggleCategory = (category) => {
  if (expandedCategory.value === category) {
    expandedCategory.value = null;
  } else {
    expandedCategory.value = category;
    selectedPaymentCategory.value = category;
  }
};

// Method to select a payment method
const selectPaymentMethod = (methodId, category) => {
  selectedPaymentMethod.value = methodId;
  selectedPaymentCategory.value = category;
};

// Method to get the count of payment methods in a category
const getCategoryCount = (category) => {
  return paymentMethods.value[category]?.length || 0;
};
</script>