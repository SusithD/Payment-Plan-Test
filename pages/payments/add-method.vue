<template>
  <div class="fade-in">
    <!-- Enhanced Header Section -->
    <div class="bg-white shadow">
      <div class="container-custom py-6">
        <div class="flex flex-col md:flex-row md:items-center md:justify-between">
          <div class="mb-4 md:mb-0">
            <h1 class="text-2xl font-bold text-gray-900">Add Payment Method</h1>
            <p class="text-sm text-gray-600 mt-1">Add a new payment method to your account</p>
          </div>
          <div class="flex items-center">
            <span class="bg-blue-100 text-blue-800 text-xs px-2.5 py-1 rounded-full font-medium">
              Secure Form
            </span>
          </div>
        </div>
      </div>
    </div>

    <div class="container-custom py-8">
      <!-- Select Payment Method Type -->
      <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 mb-8">
        <div class="px-6 py-5 border-b border-gray-100">
          <h2 class="text-xl font-bold text-gray-900">Select Payment Method Type</h2>
        </div>
        
        <div class="p-6">
          <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
            <!-- Credit/Debit Card Option -->
            <div 
              class="border p-4 rounded-lg cursor-pointer relative overflow-hidden transition-all duration-200"
              :class="{ 'border-primary-500 bg-primary-50': paymentType === 'card', 'border-gray-200 hover:border-gray-300': paymentType !== 'card' }"
              @click="paymentType = 'card'"
            >
              <div class="flex items-center">
                <div class="h-10 w-10 flex-shrink-0 rounded-full bg-primary-100 flex items-center justify-center mr-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
                  </svg>
                </div>
                <div>
                  <h3 class="font-medium">Credit / Debit Card</h3>
                  <p class="text-xs text-gray-500 mt-1">Visa, Mastercard, Amex, etc.</p>
                </div>
                <div class="absolute right-4">
                  <div class="h-5 w-5 rounded-full border-2"
                       :class="{ 'border-primary-500': paymentType === 'card', 'border-gray-300': paymentType !== 'card' }">
                    <div v-if="paymentType === 'card'" class="h-3 w-3 m-0.5 rounded-full bg-primary-500"></div>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Bank Account Option -->
            <div 
              class="border p-4 rounded-lg cursor-pointer relative overflow-hidden transition-all duration-200"
              :class="{ 'border-primary-500 bg-primary-50': paymentType === 'bank', 'border-gray-200 hover:border-gray-300': paymentType !== 'bank' }"
              @click="paymentType = 'bank'"
            >
              <div class="flex items-center">
                <div class="h-10 w-10 flex-shrink-0 rounded-full bg-accent-100 flex items-center justify-center mr-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-accent-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 14v3m4-3v3m4-3v3M3 21h18M3 10h18M3 7l9-4 9 4M4 10h16v11H4V10z" />
                  </svg>
                </div>
                <div>
                  <h3 class="font-medium">Bank Account</h3>
                  <p class="text-xs text-gray-500 mt-1">Direct debit from your account</p>
                </div>
                <div class="absolute right-4">
                  <div class="h-5 w-5 rounded-full border-2"
                       :class="{ 'border-primary-500': paymentType === 'bank', 'border-gray-300': paymentType !== 'bank' }">
                    <div v-if="paymentType === 'bank'" class="h-3 w-3 m-0.5 rounded-full bg-primary-500"></div>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Digital Wallet Option -->
            <div 
              class="border p-4 rounded-lg cursor-pointer relative overflow-hidden transition-all duration-200"
              :class="{ 'border-primary-500 bg-primary-50': paymentType === 'wallet', 'border-gray-200 hover:border-gray-300': paymentType !== 'wallet' }"
              @click="paymentType = 'wallet'"
            >
              <div class="flex items-center">
                <div class="h-10 w-10 flex-shrink-0 rounded-full bg-success-100 flex items-center justify-center mr-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-success-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z" />
                  </svg>
                </div>
                <div>
                  <h3 class="font-medium">Digital Wallet</h3>
                  <p class="text-xs text-gray-500 mt-1">PayPal, Apple Pay, etc.</p>
                </div>
                <div class="absolute right-4">
                  <div class="h-5 w-5 rounded-full border-2"
                       :class="{ 'border-primary-500': paymentType === 'wallet', 'border-gray-300': paymentType !== 'wallet' }">
                    <div v-if="paymentType === 'wallet'" class="h-3 w-3 m-0.5 rounded-full bg-primary-500"></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Credit Card Form -->
      <div v-if="paymentType === 'card'" class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 mb-8">
        <div class="px-6 py-5 border-b border-gray-100">
          <h2 class="text-xl font-bold text-gray-900">Credit Card Details</h2>
        </div>
        
        <div class="p-6">
          <form @submit.prevent="savePaymentMethod">
            <div class="space-y-6">
              <!-- Card Details -->
              <div class="grid grid-cols-1 gap-y-6 gap-x-4 sm:grid-cols-6">
                <div class="sm:col-span-6">
                  <label for="card-holder" class="block text-sm font-medium text-gray-700 mb-1">Cardholder Name</label>
                  <input 
                    type="text" 
                    id="card-holder" 
                    v-model="cardDetails.cardHolder"
                    class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                    placeholder="Name as shown on card"
                    required
                  />
                </div>

                <div class="sm:col-span-6">
                  <label for="card-number" class="block text-sm font-medium text-gray-700 mb-1">Card Number</label>
                  <div class="relative">
                    <input 
                      type="text" 
                      id="card-number" 
                      v-model="cardDetails.cardNumber"
                      class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                      placeholder="1234 5678 9012 3456"
                      maxlength="19"
                      required
                    />
                    <div class="absolute inset-y-0 right-0 flex items-center pr-3">
                      <div class="flex space-x-1">
                        <img src="https://cdn.jsdelivr.net/npm/payment-icons@1.0.0/min/flat/visa.svg" class="h-6 w-auto" alt="Visa" />
                        <img src="https://cdn.jsdelivr.net/npm/payment-icons@1.0.0/min/flat/mastercard.svg" class="h-6 w-auto" alt="Mastercard" />
                        <img src="https://cdn.jsdelivr.net/npm/payment-icons@1.0.0/min/flat/amex.svg" class="h-6 w-auto" alt="American Express" />
                      </div>
                    </div>
                  </div>
                </div>

                <div class="sm:col-span-3">
                  <label for="expiry-date" class="block text-sm font-medium text-gray-700 mb-1">Expiry Date</label>
                  <input 
                    type="text" 
                    id="expiry-date" 
                    v-model="cardDetails.expiryDate"
                    class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                    placeholder="MM/YY"
                    maxlength="5"
                    required
                  />
                </div>

                <div class="sm:col-span-3">
                  <label for="cvv" class="block text-sm font-medium text-gray-700 mb-1">Security Code (CVV)</label>
                  <div class="relative">
                    <input 
                      type="password" 
                      id="cvv" 
                      v-model="cardDetails.cvv"
                      class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                      placeholder="123"
                      maxlength="4"
                      required
                    />
                    <div class="absolute inset-y-0 right-0 flex items-center pr-3">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400 cursor-help" fill="none" viewBox="0 0 24 24" stroke="currentColor" @click="showCvvInfo = !showCvvInfo">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                      </svg>
                    </div>
                  </div>
                  <div v-if="showCvvInfo" class="mt-1 text-xs text-gray-500">
                    The CVV is the 3-digit security code on the back of your card (4 digits on the front for American Express)
                  </div>
                </div>
              </div>

              <!-- Billing Address -->
              <div class="pt-4">
                <h3 class="text-md font-medium text-gray-700 mb-3">Billing Address</h3>
                <div class="grid grid-cols-1 gap-y-6 gap-x-4 sm:grid-cols-6">
                  <div class="sm:col-span-6">
                    <label for="address" class="block text-sm font-medium text-gray-700 mb-1">Street Address</label>
                    <input 
                      type="text" 
                      id="address" 
                      v-model="cardDetails.billingAddress.street"
                      class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                      placeholder="123 Main St"
                      required
                    />
                  </div>

                  <div class="sm:col-span-6">
                    <label for="address2" class="block text-sm font-medium text-gray-700 mb-1">Apt, Suite, etc. (optional)</label>
                    <input 
                      type="text" 
                      id="address2" 
                      v-model="cardDetails.billingAddress.street2"
                      class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                      placeholder="Apartment 4B"
                    />
                  </div>

                  <div class="sm:col-span-3">
                    <label for="city" class="block text-sm font-medium text-gray-700 mb-1">City</label>
                    <input 
                      type="text" 
                      id="city" 
                      v-model="cardDetails.billingAddress.city"
                      class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                      placeholder="New York"
                      required
                    />
                  </div>

                  <div class="sm:col-span-3">
                    <label for="state" class="block text-sm font-medium text-gray-700 mb-1">State/Province</label>
                    <input 
                      type="text" 
                      id="state" 
                      v-model="cardDetails.billingAddress.state"
                      class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                      placeholder="NY"
                      required
                    />
                  </div>

                  <div class="sm:col-span-3">
                    <label for="postal-code" class="block text-sm font-medium text-gray-700 mb-1">ZIP/Postal Code</label>
                    <input 
                      type="text" 
                      id="postal-code" 
                      v-model="cardDetails.billingAddress.postalCode"
                      class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                      placeholder="10001"
                      required
                    />
                  </div>

                  <div class="sm:col-span-3">
                    <label for="country" class="block text-sm font-medium text-gray-700 mb-1">Country</label>
                    <select 
                      id="country" 
                      v-model="cardDetails.billingAddress.country"
                      class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                      required
                    >
                      <option value="">Select Country</option>
                      <option value="US">United States</option>
                      <option value="CA">Canada</option>
                      <option value="UK">United Kingdom</option>
                      <option value="AU">Australia</option>
                      <option value="Other">Other</option>
                    </select>
                  </div>
                </div>
              </div>

              <!-- Save as default payment method -->
              <div class="flex items-center">
                <input 
                  type="checkbox" 
                  id="default-payment" 
                  v-model="cardDetails.isDefault"
                  class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded"
                />
                <label for="default-payment" class="ml-2 block text-sm text-gray-700">
                  Set as default payment method
                </label>
              </div>

              <!-- Security Message -->
              <div class="bg-gray-50 p-4 rounded-lg">
                <div class="flex">
                  <div class="flex-shrink-0">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
                    </svg>
                  </div>
                  <div class="ml-3">
                    <p class="text-sm text-gray-500">
                      Your payment information is encrypted and secure. We use industry-standard security measures to protect your data.
                    </p>
                  </div>
                </div>
              </div>

              <div class="flex justify-end space-x-3">
                <NuxtLink to="/payments" class="btn-outline">
                  Cancel
                </NuxtLink>
                <button type="submit" class="btn-primary">
                  Save Payment Method
                </button>
              </div>
            </div>
          </form>
        </div>
      </div>
      
      <!-- Bank Account Form -->
      <div v-if="paymentType === 'bank'" class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 mb-8">
        <div class="px-6 py-5 border-b border-gray-100">
          <h2 class="text-xl font-bold text-gray-900">Bank Account Details</h2>
        </div>
        
        <div class="p-6">
          <form @submit.prevent="savePaymentMethod">
            <div class="space-y-6">
              <!-- Account Details -->
              <div class="grid grid-cols-1 gap-y-6 gap-x-4 sm:grid-cols-6">
                <div class="sm:col-span-6">
                  <label for="account-holder" class="block text-sm font-medium text-gray-700 mb-1">Account Holder Name</label>
                  <input 
                    type="text" 
                    id="account-holder" 
                    v-model="bankDetails.accountHolder"
                    class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                    placeholder="Full name on account"
                    required
                  />
                </div>

                <div class="sm:col-span-6">
                  <label for="bank-name" class="block text-sm font-medium text-gray-700 mb-1">Bank Name</label>
                  <input 
                    type="text" 
                    id="bank-name" 
                    v-model="bankDetails.bankName"
                    class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                    placeholder="Bank name"
                    required
                  />
                </div>

                <div class="sm:col-span-3">
                  <label for="account-type" class="block text-sm font-medium text-gray-700 mb-1">Account Type</label>
                  <select 
                    id="account-type" 
                    v-model="bankDetails.accountType"
                    class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                    required
                  >
                    <option value="">Select Account Type</option>
                    <option value="checking">Checking</option>
                    <option value="savings">Savings</option>
                    <option value="business">Business</option>
                  </select>
                </div>

                <div class="sm:col-span-3">
                  <label for="account-currency" class="block text-sm font-medium text-gray-700 mb-1">Currency</label>
                  <select 
                    id="account-currency" 
                    v-model="bankDetails.currency"
                    class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                    required
                  >
                    <option value="USD">USD - US Dollar</option>
                    <option value="CAD">CAD - Canadian Dollar</option>
                    <option value="GBP">GBP - British Pound</option>
                    <option value="EUR">EUR - Euro</option>
                    <option value="AUD">AUD - Australian Dollar</option>
                  </select>
                </div>

                <div class="sm:col-span-3">
                  <label for="routing-number" class="block text-sm font-medium text-gray-700 mb-1">Routing Number</label>
                  <input 
                    type="text" 
                    id="routing-number" 
                    v-model="bankDetails.routingNumber"
                    class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                    placeholder="9 digits"
                    required
                  />
                </div>

                <div class="sm:col-span-3">
                  <label for="account-number" class="block text-sm font-medium text-gray-700 mb-1">Account Number</label>
                  <input 
                    type="password" 
                    id="account-number" 
                    v-model="bankDetails.accountNumber"
                    class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                    placeholder="Your account number"
                    required
                  />
                </div>

                <div class="sm:col-span-6">
                  <label for="account-confirm" class="block text-sm font-medium text-gray-700 mb-1">Confirm Account Number</label>
                  <input 
                    type="text" 
                    id="account-confirm" 
                    v-model="bankDetails.accountNumberConfirm"
                    class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                    placeholder="Re-enter your account number"
                    required
                  />
                </div>
              </div>

              <!-- Billing Address -->
              <div class="pt-4">
                <h3 class="text-md font-medium text-gray-700 mb-3">Billing Address</h3>
                <div class="grid grid-cols-1 gap-y-6 gap-x-4 sm:grid-cols-6">
                  <div class="sm:col-span-6">
                    <label for="bank-address" class="block text-sm font-medium text-gray-700 mb-1">Street Address</label>
                    <input 
                      type="text" 
                      id="bank-address" 
                      v-model="bankDetails.billingAddress.street"
                      class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                      placeholder="123 Main St"
                      required
                    />
                  </div>

                  <div class="sm:col-span-6">
                    <label for="bank-address2" class="block text-sm font-medium text-gray-700 mb-1">Apt, Suite, etc. (optional)</label>
                    <input 
                      type="text" 
                      id="bank-address2" 
                      v-model="bankDetails.billingAddress.street2"
                      class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                      placeholder="Apartment 4B"
                    />
                  </div>

                  <div class="sm:col-span-3">
                    <label for="bank-city" class="block text-sm font-medium text-gray-700 mb-1">City</label>
                    <input 
                      type="text" 
                      id="bank-city" 
                      v-model="bankDetails.billingAddress.city"
                      class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                      placeholder="New York"
                      required
                    />
                  </div>

                  <div class="sm:col-span-3">
                    <label for="bank-state" class="block text-sm font-medium text-gray-700 mb-1">State/Province</label>
                    <input 
                      type="text" 
                      id="bank-state" 
                      v-model="bankDetails.billingAddress.state"
                      class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                      placeholder="NY"
                      required
                    />
                  </div>

                  <div class="sm:col-span-3">
                    <label for="bank-postal-code" class="block text-sm font-medium text-gray-700 mb-1">ZIP/Postal Code</label>
                    <input 
                      type="text" 
                      id="bank-postal-code" 
                      v-model="bankDetails.billingAddress.postalCode"
                      class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                      placeholder="10001"
                      required
                    />
                  </div>

                  <div class="sm:col-span-3">
                    <label for="bank-country" class="block text-sm font-medium text-gray-700 mb-1">Country</label>
                    <select 
                      id="bank-country" 
                      v-model="bankDetails.billingAddress.country"
                      class="block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-primary-500 focus:border-primary-500 sm:text-sm"
                      required
                    >
                      <option value="">Select Country</option>
                      <option value="US">United States</option>
                      <option value="CA">Canada</option>
                      <option value="UK">United Kingdom</option>
                      <option value="AU">Australia</option>
                      <option value="Other">Other</option>
                    </select>
                  </div>
                </div>
              </div>

              <!-- Authorization -->
              <div class="pt-4">
                <div class="bg-yellow-50 p-4 rounded-md mb-4">
                  <div class="flex">
                    <div class="flex-shrink-0">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-yellow-400" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd" />
                      </svg>
                    </div>
                    <div class="ml-3">
                      <h3 class="text-sm font-medium text-yellow-800">Important Information</h3>
                      <div class="mt-2 text-sm text-yellow-700">
                        <p>By adding your bank account, you authorize our payment processor to debit the account for future payments according to the payment schedule.</p>
                      </div>
                    </div>
                  </div>
                </div>

                <div class="flex items-start">
                  <div class="flex-shrink-0">
                    <input 
                      id="auth-agreement" 
                      type="checkbox" 
                      v-model="bankDetails.authorized"
                      class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded"
                      required
                    />
                  </div>
                  <div class="ml-3">
                    <label for="auth-agreement" class="text-sm text-gray-700">
                      I authorize the use of my bank account for automatic payments according to the payment schedule and agree to the <a href="#" class="text-primary-600 hover:text-primary-500">terms and conditions</a>.
                    </label>
                  </div>
                </div>
              </div>

              <!-- Save as default payment method -->
              <div class="flex items-center">
                <input 
                  type="checkbox" 
                  id="bank-default-payment" 
                  v-model="bankDetails.isDefault"
                  class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded"
                />
                <label for="bank-default-payment" class="ml-2 block text-sm text-gray-700">
                  Set as default payment method
                </label>
              </div>

              <!-- Security Message -->
              <div class="bg-gray-50 p-4 rounded-lg">
                <div class="flex">
                  <div class="flex-shrink-0">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
                    </svg>
                  </div>
                  <div class="ml-3">
                    <p class="text-sm text-gray-500">
                      Your bank account information is encrypted and secure. We use industry-standard security measures to protect your data.
                    </p>
                  </div>
                </div>
              </div>

              <div class="flex justify-end space-x-3">
                <NuxtLink to="/payments" class="btn-outline">
                  Cancel
                </NuxtLink>
                <button type="submit" class="btn-primary">
                  Save Payment Method
                </button>
              </div>
            </div>
          </form>
        </div>
      </div>
      
      <!-- Digital Wallet Form -->
      <div v-if="paymentType === 'wallet'" class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 mb-8">
        <div class="px-6 py-5 border-b border-gray-100">
          <h2 class="text-xl font-bold text-gray-900">Digital Wallet</h2>
        </div>
        
        <div class="p-6">
          <form @submit.prevent="connectWallet">
            <div class="space-y-6">
              <!-- Wallet Selection -->
              <div class="grid grid-cols-1 gap-4 sm:grid-cols-2">
                <div 
                  class="border p-4 rounded-lg cursor-pointer relative overflow-hidden transition-all duration-200"
                  :class="{ 'border-primary-500 bg-primary-50': walletDetails.provider === 'paypal', 'border-gray-200 hover:border-gray-300': walletDetails.provider !== 'paypal' }"
                  @click="walletDetails.provider = 'paypal'"
                >
                  <div class="flex items-center">
                    <div class="h-10 w-10 flex-shrink-0 rounded-full bg-blue-100 flex items-center justify-center mr-3">
                      <span class="text-blue-700 font-bold">P</span>
                    </div>
                    <div>
                      <h3 class="font-medium">PayPal</h3>
                      <p class="text-xs text-gray-500 mt-1">Connect your PayPal account</p>
                    </div>
                    <div class="absolute right-4">
                      <div class="h-5 w-5 rounded-full border-2"
                          :class="{ 'border-primary-500': walletDetails.provider === 'paypal', 'border-gray-300': walletDetails.provider !== 'paypal' }">
                        <div v-if="walletDetails.provider === 'paypal'" class="h-3 w-3 m-0.5 rounded-full bg-primary-500"></div>
                      </div>
                    </div>
                  </div>
                </div>
                
                <div 
                  class="border p-4 rounded-lg cursor-pointer relative overflow-hidden transition-all duration-200"
                  :class="{ 'border-primary-500 bg-primary-50': walletDetails.provider === 'applepay', 'border-gray-200 hover:border-gray-300': walletDetails.provider !== 'applepay' }"
                  @click="walletDetails.provider = 'applepay'"
                >
                  <div class="flex items-center">
                    <div class="h-10 w-10 flex-shrink-0 rounded-full bg-gray-900 flex items-center justify-center mr-3">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path d="M12 19c.8284 0 1.5-3.134 1.5-7S12.8284 5 12 5s-1.5 3.134-1.5 7 .6716 7 1.5 7Z" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path>
                        <path d="M12 5c-4.1421 0-7.5-1.1193-7.5-2.5v17c0 1.3807 3.3579 2.5 7.5 2.5m0-17c4.1421 0 7.5-1.1193 7.5-2.5v17c0 1.3807-3.3579 2.5-7.5 2.5" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"></path>
                      </svg>
                    </div>
                    <div>
                      <h3 class="font-medium">Apple Pay</h3>
                      <p class="text-xs text-gray-500 mt-1">Connect your Apple Pay</p>
                    </div>
                    <div class="absolute right-4">
                      <div class="h-5 w-5 rounded-full border-2"
                          :class="{ 'border-primary-500': walletDetails.provider === 'applepay', 'border-gray-300': walletDetails.provider !== 'applepay' }">
                        <div v-if="walletDetails.provider === 'applepay'" class="h-3 w-3 m-0.5 rounded-full bg-primary-500"></div>
                      </div>
                    </div>
                  </div>
                </div>
                
                <div 
                  class="border p-4 rounded-lg cursor-pointer relative overflow-hidden transition-all duration-200"
                  :class="{ 'border-primary-500 bg-primary-50': walletDetails.provider === 'googlepay', 'border-gray-200 hover:border-gray-300': walletDetails.provider !== 'googlepay' }"
                  @click="walletDetails.provider = 'googlepay'"
                >
                  <div class="flex items-center">
                    <div class="h-10 w-10 flex-shrink-0 rounded-full bg-white border border-gray-200 flex items-center justify-center mr-3">
                      <div class="text-2xl font-bold">
                        <span class="text-blue-600">G</span>
                      </div>
                    </div>
                    <div>
                      <h3 class="font-medium">Google Pay</h3>
                      <p class="text-xs text-gray-500 mt-1">Connect your Google Pay</p>
                    </div>
                    <div class="absolute right-4">
                      <div class="h-5 w-5 rounded-full border-2"
                          :class="{ 'border-primary-500': walletDetails.provider === 'googlepay', 'border-gray-300': walletDetails.provider !== 'googlepay' }">
                        <div v-if="walletDetails.provider === 'googlepay'" class="h-3 w-3 m-0.5 rounded-full bg-primary-500"></div>
                      </div>
                    </div>
                  </div>
                </div>
                
                <div 
                  class="border p-4 rounded-lg cursor-pointer relative overflow-hidden transition-all duration-200"
                  :class="{ 'border-primary-500 bg-primary-50': walletDetails.provider === 'other', 'border-gray-200 hover:border-gray-300': walletDetails.provider !== 'other' }"
                  @click="walletDetails.provider = 'other'"
                >
                  <div class="flex items-center">
                    <div class="h-10 w-10 flex-shrink-0 rounded-full bg-gray-100 flex items-center justify-center mr-3">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
                      </svg>
                    </div>
                    <div>
                      <h3 class="font-medium">Other Wallet</h3>
                      <p class="text-xs text-gray-500 mt-1">Connect a different wallet</p>
                    </div>
                    <div class="absolute right-4">
                      <div class="h-5 w-5 rounded-full border-2"
                          :class="{ 'border-primary-500': walletDetails.provider === 'other', 'border-gray-300': walletDetails.provider !== 'other' }">
                        <div v-if="walletDetails.provider === 'other'" class="h-3 w-3 m-0.5 rounded-full bg-primary-500"></div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              
              <!-- Provider-specific instructions -->
              <div v-if="walletDetails.provider === 'paypal'" class="bg-blue-50 p-4 rounded-md">
                <div class="flex">
                  <div class="flex-shrink-0">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-blue-400" viewBox="0 0 20 20" fill="currentColor">
                      <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd" />
                    </svg>
                  </div>
                  <div class="ml-3">
                    <h3 class="text-sm font-medium text-blue-800">PayPal Connection</h3>
                    <div class="mt-2 text-sm text-blue-700">
                      <p>You'll be redirected to PayPal to securely connect your account. After completing the connection, you'll return to this site to finish setting up your payment method.</p>
                    </div>
                  </div>
                </div>
              </div>
              
              <div v-if="walletDetails.provider === 'applepay'" class="bg-gray-50 p-4 rounded-md">
                <div class="flex">
                  <div class="flex-shrink-0">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" viewBox="0 0 20 20" fill="currentColor">
                      <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd" />
                    </svg>
                  </div>
                  <div class="ml-3">
                    <h3 class="text-sm font-medium text-gray-800">Apple Pay</h3>
                    <div class="mt-2 text-sm text-gray-700">
                      <p>To use Apple Pay, you'll need to authorize this device. Click "Connect" to begin the setup process. You'll need to authenticate with Face ID or Touch ID.</p>
                    </div>
                  </div>
                </div>
              </div>
              
              <div v-if="walletDetails.provider === 'googlepay'" class="bg-gray-50 p-4 rounded-md">
                <div class="flex">
                  <div class="flex-shrink-0">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" viewBox="0 0 20 20" fill="currentColor">
                      <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd" />
                    </svg>
                  </div>
                  <div class="ml-3">
                    <h3 class="text-sm font-medium text-gray-800">Google Pay</h3>
                    <div class="mt-2 text-sm text-gray-700">
                      <p>You'll be prompted to choose from your Google Pay payment methods. Click "Connect" to start the secure connection process.</p>
                    </div>
                  </div>
                </div>
              </div>
              
              <div v-if="walletDetails.provider === 'other'" class="bg-gray-50 p-4 rounded-md">
                <div class="flex">
                  <div class="flex-shrink-0">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" viewBox="0 0 20 20" fill="currentColor">
                      <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd" />
                    </svg>
                  </div>
                  <div class="ml-3">
                    <h3 class="text-sm font-medium text-gray-800">Other Digital Wallet</h3>
                    <div class="mt-2 text-sm text-gray-700">
                      <p>Please contact our support team to set up a different digital wallet. We're continuously adding new payment options.</p>
                    </div>
                  </div>
                </div>
              </div>

              <!-- Save as default payment method -->
              <div class="flex items-center">
                <input 
                  type="checkbox" 
                  id="wallet-default-payment" 
                  v-model="walletDetails.isDefault"
                  class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded"
                />
                <label for="wallet-default-payment" class="ml-2 block text-sm text-gray-700">
                  Set as default payment method
                </label>
              </div>

              <div class="flex justify-end space-x-3">
                <NuxtLink to="/payments" class="btn-outline">
                  Cancel
                </NuxtLink>
                <button type="submit" class="btn-primary" :disabled="!walletDetails.provider">
                  Connect {{ getWalletName(walletDetails.provider) }}
                </button>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue';
import { useRouter } from 'vue-router';

definePageMeta({
  layout: 'default',
});

const router = useRouter();

// Form state
const paymentType = ref('card'); // 'card', 'bank', or 'wallet'
const showCvvInfo = ref(false);

// Credit card form details
const cardDetails = reactive({
  cardHolder: '',
  cardNumber: '',
  expiryDate: '',
  cvv: '',
  billingAddress: {
    street: '',
    street2: '',
    city: '',
    state: '',
    postalCode: '',
    country: ''
  },
  isDefault: true
});

// Bank account form details
const bankDetails = reactive({
  accountHolder: '',
  bankName: '',
  accountType: '',
  routingNumber: '',
  accountNumber: '',
  accountNumberConfirm: '',
  currency: 'USD',
  billingAddress: {
    street: '',
    street2: '',
    city: '',
    state: '',
    postalCode: '',
    country: ''
  },
  authorized: false,
  isDefault: false
});

// Digital wallet details
const walletDetails = reactive({
  provider: 'paypal', // 'paypal', 'applepay', 'googlepay', 'other'
  isDefault: false
});

// Methods
const savePaymentMethod = () => {
  // In a real app, this would validate and send the payment method data to the server
  if (paymentType.value === 'card') {
    // Check if card number is valid
    if (cardDetails.cardNumber.replace(/\s/g, '').length < 13) {
      alert('Please enter a valid card number');
      return;
    }
    
    // Check if expiry date is in correct format (MM/YY)
    const expiryRegex = /^(0[1-9]|1[0-2])\/[0-9]{2}$/;
    if (!expiryRegex.test(cardDetails.expiryDate)) {
      alert('Please enter a valid expiry date in MM/YY format');
      return;
    }
    
    // In a real app, more comprehensive validation would be performed
    
    // For demo purposes, just simulate success and redirect
    alert('Credit card saved successfully!');
  } 
  else if (paymentType.value === 'bank') {
    // Validate bank details
    if (bankDetails.accountNumber !== bankDetails.accountNumberConfirm) {
      alert('Account numbers do not match');
      return;
    }
    
    if (!bankDetails.authorized) {
      alert('You must authorize automatic payments');
      return;
    }
    
    // For demo purposes, just simulate success and redirect
    alert('Bank account saved successfully!');
  }
  
  // Redirect back to payments page
  router.push('/payments');
};

const connectWallet = () => {
  // In a real app, this would redirect to the wallet provider's authentication page
  const providerName = getWalletName(walletDetails.provider);
  
  alert(`Redirecting to ${providerName} for authentication...`);
  
  // Simulate connection success for demo purposes
  setTimeout(() => {
    alert(`${providerName} connected successfully!`);
    router.push('/payments');
  }, 1000);
};

const getWalletName = (provider) => {
  switch (provider) {
    case 'paypal': return 'PayPal';
    case 'applepay': return 'Apple Pay';
    case 'googlepay': return 'Google Pay';
    default: return 'Wallet';
  }
};
</script>

<style scoped>
/* Add any component-specific styles here */
</style>