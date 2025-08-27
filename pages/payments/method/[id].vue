<template>
  <div class="fade-in">
    <div class="bg-white shadow">
      <div class="container-custom py-6">
        <div class="flex items-center justify-between">
          <div class="flex items-center space-x-4">
            <button
              @click="$router.back()"
              class="p-2 text-gray-600 hover:text-gray-900 hover:bg-gray-100 rounded-md transition-colors"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
              </svg>
            </button>
            <h1 class="text-2xl font-bold text-gray-900">Payment Method Details</h1>
          </div>
          <div class="flex space-x-3">
            <button
              v-if="!isEditing"
              @click="startEditing"
              class="btn-outline py-2 px-4 text-sm"
            >
              Edit Details
            </button>
            <button
              v-if="!isEditing && !paymentMethod?.isDefault"
              @click="confirmDeleteMethod"
              class="btn-outline py-2 px-4 text-sm text-error-600 hover:bg-error-50 border-error-300"
            >
              Remove Method
            </button>
          </div>
        </div>
      </div>
    </div>

    <div class="container-custom py-8">
      <div class="max-w-4xl mx-auto">
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
          <!-- Payment Method Card Preview -->
          <div class="lg:col-span-1">
            <div class="card sticky top-6">
              <h3 class="text-lg font-semibold mb-4">Payment Method Preview</h3>

              <!-- Card Visual -->
              <div class="relative bg-gradient-to-r from-gray-900 to-gray-700 rounded-xl p-6 text-white mb-4" v-if="paymentMethod?.type === 'card'">
                <div class="flex justify-between items-start mb-8">
                  <div class="text-xs uppercase tracking-wider opacity-75">Payment Card</div>
                  <!-- Card Brand Icon -->
                  <div class="h-8 w-12 flex items-center justify-center">
                    <!-- Visa SVG -->
                    <svg
                      v-if="paymentMethod?.brand === 'visa'"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 48 48"
                      class="h-6"
                    >
                      <path fill="#1565C0" d="M45,35c0,2.209-1.791,4-4,4H7c-2.209,0-4-1.791-4-4V13c0-2.209,1.791-4,4-4h34c2.209,0,4,1.791,4,4V35z"/>
                      <path fill="#FFF" d="M15.186 19l-2.626 7.832c0 0-.667-3.313-.733-3.729-1.495-3.411-3.701-3.221-3.701-3.221L10.726 30v-.002h3.161L18.258 19H15.186zM17.689 30L20.56 30 22.296 19 19.389 19zM38.008 19h-3.021l-4.71 11h2.852l.588-1.571h3.596L37.619 30h2.613L38.008 19zM34.513 26.328l1.563-4.157.818 4.157H34.513zM26.369 22.206c0-.606.498-1.057 1.926-1.057.928 0 1.991.302 1.991.302l.466-2.158c0 0-1.358-.515-2.691-.515-3.019 0-4.576 1.444-4.576 3.272 0 3.294 3.979 2.824 3.979 4.38 0 .513-.545.884-1.7.884-1.407 0-2.773-.486-2.773-.486l-.495 2.202c0 0 1.303.594 3.132.594 2.744 0 4.576-1.39 4.576-3.258C30.205 23.175 26.369 23.457 26.369 22.206z"/>
                    </svg>

                    <!-- Mastercard SVG -->
                    <svg
                      v-else-if="paymentMethod?.brand === 'mastercard'"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 48 48"
                      class="h-6"
                    >
                      <path fill="#FF5F00" d="M32,25H16V8h16V25z"/>
                      <path fill="#EB001B" d="M19.5,16.5c0-3.59,1.69-6.79,4.3-8.86c-1.89-1.47-4.24-2.33-6.8-2.33c-6.14,0-11.14,5-11.14,11.14 s5,11.14,11.14,11.14c2.56,0,4.91-0.87,6.8-2.33C21.19,23.29,19.5,20.09,19.5,16.5z"/>
                      <path fill="#F79E1B" d="M42,16.5c0,6.14-5,11.14-11.14,11.14c-2.56,0-4.91-0.87-6.8-2.33c2.61-2.08,4.3-5.27,4.3-8.86 s-1.69-6.79-4.3-8.86c1.89-1.47,4.24-2.33,6.8-2.33C37,5.36,42,10.36,42,16.5z"/>
                    </svg>

                    <!-- American Express SVG -->
                    <svg
                      v-else-if="paymentMethod?.brand === 'amex'"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 48 48"
                      class="h-6"
                    >
                      <path fill="#1976D2" d="M45,35c0,2.209-1.791,4-4,4H7c-2.209,0-4-1.791-4-4V13c0-2.209,1.791-4,4-4h34c2.209,0,4,1.791,4,4V35z"/>
                      <path fill="#FFF" d="M22.255 20l-2.113 4.683L18.039 20h-2.695v6.726L12.341 20h-2.274L7 26.981h1.815l.642-1.47h3.312l.642 1.47h3.001v-5.227l2.127 5.227l2.127-5.246v5.246H22.5v-7H22.255zM10.132 24.068l.996-2.3.997 2.3H10.132zM33.5 26.981h2.403L33.5 23.488v-3.507h-3.866l-1.282 2.918L27.117 20H23.25v7H27v-4.99l1.883 2.99h.001v-3.004L30.7 26.981h1.883v-5.1L33.5 26.981zM40.936 26.981h1.815l-3.067-6.999h-2.274l-3.067 6.999h1.815l.642-1.47h3.494L40.936 26.981zM39.678 24.068h-2.178l1.09-2.511L39.678 24.068z"/>
                    </svg>

                    <!-- Generic Card SVG -->
                    <svg
                      v-else
                      xmlns="http://www.w3.org/2000/svg"
                      class="h-6 w-6 text-white"
                      fill="none"
                      viewBox="0 0 24 24"
                      stroke="currentColor"
                    >
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
                    </svg>
                  </div>
                </div>

                <div class="text-xl font-mono tracking-wider mb-4">
                  •••• •••• •••• {{ paymentMethod?.last4 }}
                </div>

                <div class="flex justify-between items-end">
                  <div>
                    <div class="text-xs opacity-75 mb-1">Card Holder</div>
                    <div class="text-sm font-medium">{{ paymentMethod?.holderName }}</div>
                  </div>
                  <div>
                    <div class="text-xs opacity-75 mb-1">Expires</div>
                    <div class="text-sm font-medium">{{ paymentMethod?.expMonth }}/{{ paymentMethod?.expYear }}</div>
                  </div>
                </div>
              </div>

              <!-- Bank Account Visual -->
              <div class="relative bg-gradient-to-r from-blue-900 to-blue-700 rounded-xl p-6 text-white mb-4" v-else-if="paymentMethod?.type === 'bank'">
                <div class="flex justify-between items-start mb-8">
                  <div class="text-xs uppercase tracking-wider opacity-75">Bank Account</div>
                  <!-- Bank Icon -->
                  <div class="h-8 w-12 flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 14v3m4-3v3m4-3v3M3 21h18M3 10h18M3 7l9-4 9 4M4 10h16v11H4V10z" />
                    </svg>
                  </div>
                </div>

                <div class="text-xl font-mono tracking-wider mb-4">
                  {{ paymentMethod?.bankName }}
                </div>

                <div class="flex justify-between items-end">
                  <div>
                    <div class="text-xs opacity-75 mb-1">Account Holder</div>
                    <div class="text-sm font-medium">{{ paymentMethod?.accountHolderName }}</div>
                  </div>
                  <div>
                    <div class="text-xs opacity-75 mb-1">Account</div>
                    <div class="text-sm font-medium">•••• {{ paymentMethod?.last4 }}</div>
                  </div>
                </div>
              </div>

              <!-- Status Badges -->
              <div class="space-y-2">
                <div
                  v-if="paymentMethod?.isDefault"
                  class="inline-flex items-center px-3 py-1 rounded-full text-sm font-medium bg-primary-100 text-primary-800"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                  </svg>
                  Default Payment Method
                </div>
                <div class="inline-flex items-center px-3 py-1 rounded-full text-sm font-medium bg-green-100 text-green-800">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                  Active
                </div>
              </div>
            </div>
          </div>

          <!-- Payment Method Details -->
          <div class="lg:col-span-2">
            <div class="card">
              <div class="flex justify-between items-center mb-6">
                <h2 class="text-xl font-bold">Payment Method Information</h2>
                <div v-if="!paymentMethod?.isDefault" class="flex items-center">
                  <button
                    @click="setAsDefault"
                    class="btn-outline py-1.5 px-3 text-sm"
                  >
                    Set as Default
                  </button>
                </div>
              </div>

              <form @submit.prevent="saveChanges">
                <div class="space-y-6">
                  <!-- Card Information -->
                  <div v-if="paymentMethod?.type === 'card'" class="bg-gray-50 rounded-lg p-4 border-2" :class="isEditing ? 'border-primary-200 bg-primary-50' : 'border-gray-200'">
                    <div class="flex items-center justify-between mb-4">
                      <h3 class="text-lg font-semibold text-gray-900">Card Information</h3>
                      <div v-if="isEditing" class="flex items-center text-primary-600 text-sm font-medium">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                        </svg>
                        Editing Mode
                      </div>
                    </div>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                      <div>
                        <label class="form-label text-gray-700">Card Type</label>
                        <div class="text-gray-900 font-medium capitalize">
                          {{ paymentMethod?.brand }} Card
                        </div>
                      </div>
                      <div>
                        <label class="form-label text-gray-700">Card Number</label>
                        <div class="text-gray-900 font-medium font-mono">
                          •••• •••• •••• {{ paymentMethod?.last4 }}
                        </div>
                      </div>
                      <div class="relative">
                        <label class="form-label text-gray-700 flex items-center">
                          Expiry Date
                          <span v-if="isEditing" class="ml-2 inline-flex items-center px-2 py-0.5 rounded text-xs font-medium bg-primary-100 text-primary-800">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-3 w-3 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                            </svg>
                            Editable
                          </span>
                        </label>
                        <div v-if="!isEditing" class="text-gray-900 font-medium bg-white p-2 rounded border">
                          {{ paymentMethod?.expMonth }}/{{ paymentMethod?.expYear }}
                        </div>
                        <div v-else class="grid grid-cols-2 gap-2">
                          <div class="relative">
                            <select
                              v-model="editableData.expMonth"
                              class="form-select text-sm bg-white border-primary-300 focus:border-primary-500 focus:ring-primary-500"
                              :class="{ 'ring-2 ring-primary-200': isEditing }"
                            >
                              <option value="">Month</option>
                              <option v-for="month in 12" :key="month" :value="String(month).padStart(2, '0')">
                                {{ String(month).padStart(2, '0') }} - {{ getMonthName(month) }}
                              </option>
                            </select>
                            <div class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none">
                              <svg class="h-4 w-4 text-primary-500" fill="currentColor" viewBox="0 0 20 20">
                                <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" />
                              </svg>
                            </div>
                          </div>
                          <div class="relative">
                            <select
                              v-model="editableData.expYear"
                              class="form-select text-sm bg-white border-primary-300 focus:border-primary-500 focus:ring-primary-500"
                              :class="{ 'ring-2 ring-primary-200': isEditing }"
                            >
                              <option value="">Year</option>
                              <option v-for="year in getYearOptions()" :key="year" :value="String(year).slice(-2)">
                                {{ year }}
                              </option>
                            </select>
                            <div class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none">
                              <svg class="h-4 w-4 text-primary-500" fill="currentColor" viewBox="0 0 20 20">
                                <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" />
                              </svg>
                            </div>
                          </div>
                        </div>
                        <div v-if="isEditing" class="mt-1 text-xs text-primary-600">
                          Select the card's expiration month and year
                        </div>
                      </div>
                      <div>
                        <label class="form-label text-gray-700">Added On</label>
                        <div class="text-gray-900 font-medium">
                          {{ paymentMethod?.addedDate }}
                        </div>
                      </div>
                    </div>
                    <div class="mt-3 text-sm text-gray-600" v-if="!isEditing">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 inline mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
                      </svg>
                      Card information is encrypted and secure. Click "Edit Details" to update the expiry date.
                    </div>
                    <div class="mt-3 text-sm text-primary-600" v-else>
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 inline mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                      </svg>
                      You can now update the card's expiry date. Other card details remain secure.
                    </div>
                  </div>

                  <!-- Bank Account Information -->
                  <div v-else-if="paymentMethod?.type === 'bank'" class="bg-blue-50 rounded-lg p-4 border-2" :class="isEditing ? 'border-blue-300 bg-blue-100' : 'border-blue-200'">
                    <div class="flex items-center justify-between mb-4">
                      <h3 class="text-lg font-semibold text-blue-900">Bank Account Information</h3>
                      <div v-if="isEditing" class="flex items-center text-blue-600 text-sm font-medium">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                        </svg>
                        Editing Mode
                      </div>
                    </div>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                      <div>
                        <label class="form-label text-blue-700">Bank Name</label>
                        <div class="text-blue-900 font-medium">
                          {{ paymentMethod?.bankName }}
                        </div>
                      </div>
                      <div class="relative">
                        <label class="form-label text-blue-700 flex items-center">
                          Account Type
                          <span v-if="isEditing" class="ml-2 inline-flex items-center px-2 py-0.5 rounded text-xs font-medium bg-blue-200 text-blue-800">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-3 w-3 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                            </svg>
                            Editable
                          </span>
                        </label>
                        <div v-if="!isEditing" class="text-blue-900 font-medium capitalize bg-white p-2 rounded border">
                          {{ paymentMethod?.accountType }}
                        </div>
                        <div v-else class="relative">
                          <select
                            v-model="editableData.accountType"
                            class="form-select text-sm bg-white border-blue-300 focus:border-blue-500 focus:ring-blue-500 w-full"
                            :class="{ 'ring-2 ring-blue-200': isEditing }"
                          >
                            <option value="">Select Account Type</option>
                            <option value="checking">Checking Account</option>
                            <option value="savings">Savings Account</option>
                            <option value="business_checking">Business Checking</option>
                            <option value="business_savings">Business Savings</option>
                          </select>
                          <div class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none">
                            <svg class="h-4 w-4 text-blue-500" fill="currentColor" viewBox="0 0 20 20">
                              <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" />
                            </svg>
                          </div>
                        </div>
                        <div v-if="isEditing" class="mt-1 text-xs text-blue-600">
                          Select the type of bank account for accurate processing
                        </div>
                      </div>
                      <div>
                        <label class="form-label text-blue-700">Account Number</label>
                        <div class="text-blue-900 font-medium font-mono">
                          •••• •••• •••• {{ paymentMethod?.last4 }}
                        </div>
                      </div>
                      <div>
                        <label class="form-label text-blue-700">Routing Number</label>
                        <div class="text-blue-900 font-medium">
                          {{ paymentMethod?.routingNumber }}
                        </div>
                      </div>
                      <div>
                        <label class="form-label text-blue-700">Added On</label>
                        <div class="text-blue-900 font-medium">
                          {{ paymentMethod?.addedDate }}
                        </div>
                      </div>
                      <div>
                        <label class="form-label text-blue-700">Verification Status</label>
                        <div class="flex items-center">
                          <span class="inline-flex items-center px-2 py-1 rounded-full text-xs font-medium bg-green-100 text-green-800">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-3 w-3 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                            </svg>
                            Verified
                          </span>
                        </div>
                      </div>
                    </div>
                    <div class="mt-3 text-sm text-blue-600" v-if="!isEditing">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 inline mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
                      </svg>
                      Bank account information is encrypted and secure. Click "Edit Details" to update the account type.
                    </div>
                    <div class="mt-3 text-sm text-blue-600" v-else>
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 inline mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                      </svg>
                      You can now update the account type. Other bank details remain secure.
                    </div>
                  </div>

                  <!-- Editable Account Holder Information -->
                  <div>
                    <h3 class="text-lg font-semibold mb-4">
                      {{ paymentMethod?.type === 'card' ? 'Cardholder Information' : 'Account Holder Information' }}
                    </h3>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                      <div class="md:col-span-2">
                        <label for="holder-name" class="form-label">
                          {{ paymentMethod?.type === 'card' ? 'Cardholder Name' : 'Account Holder Name' }}
                        </label>
                        <input
                          type="text"
                          id="holder-name"
                          v-model="editableData.holderName"
                          class="form-input"
                          :disabled="!isEditing"
                          :placeholder="paymentMethod?.type === 'card' ? 'Enter cardholder name' : 'Enter account holder name'"
                        />
                      </div>
                    </div>
                  </div>

                  <!-- Billing Address -->
                  <div>
                    <h3 class="text-lg font-semibold mb-4">
                      {{ paymentMethod?.type === 'card' ? 'Billing Address' : 'Account Address' }}
                    </h3>
                    <div class="grid grid-cols-1 gap-4">
                      <div>
                        <label for="street" class="form-label">Street Address</label>
                        <input
                          type="text"
                          id="street"
                          v-model="editableData.billingAddress.street"
                          class="form-input"
                          :disabled="!isEditing"
                          placeholder="123 Main Street"
                        />
                      </div>

                      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                          <label for="city" class="form-label">City</label>
                          <input
                            type="text"
                            id="city"
                            v-model="editableData.billingAddress.city"
                            class="form-input"
                            :disabled="!isEditing"
                            placeholder="New York"
                          />
                        </div>
                        <div>
                          <label for="state" class="form-label">State/Province</label>
                          <input
                            type="text"
                            id="state"
                            v-model="editableData.billingAddress.state"
                            class="form-input"
                            :disabled="!isEditing"
                            placeholder="NY"
                          />
                        </div>
                      </div>

                      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                          <label for="postal-code" class="form-label">Postal Code</label>
                          <input
                            type="text"
                            id="postal-code"
                            v-model="editableData.billingAddress.postalCode"
                            class="form-input"
                            :disabled="!isEditing"
                            placeholder="10001"
                          />
                        </div>
                        <div>
                          <label for="country" class="form-label">Country</label>
                          <select
                            id="country"
                            v-model="editableData.billingAddress.country"
                            class="form-select"
                            :disabled="!isEditing"
                          >
                            <option value="United States">United States</option>
                            <option value="Canada">Canada</option>
                            <option value="United Kingdom">United Kingdom</option>
                            <option value="Australia">Australia</option>
                            <option value="Germany">Germany</option>
                            <option value="France">France</option>
                            <option value="Japan">Japan</option>
                            <option value="China">China</option>
                            <option value="India">India</option>
                          </select>
                        </div>
                      </div>
                    </div>
                  </div>

                  <!-- Usage Statistics -->
                  <div class="bg-blue-50 rounded-lg p-4">
                    <h3 class="text-lg font-semibold mb-4 text-blue-900">Usage Statistics</h3>
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                      <div class="text-center">
                        <div class="text-2xl font-bold text-blue-900">{{ paymentMethod?.totalTransactions || 0 }}</div>
                        <div class="text-sm text-blue-700">Total Transactions</div>
                      </div>
                      <div class="text-center">
                        <div class="text-2xl font-bold text-blue-900">${{ paymentMethod?.totalAmount || '0.00' }}</div>
                        <div class="text-sm text-blue-700">Total Amount</div>
                      </div>
                      <div class="text-center">
                        <div class="text-2xl font-bold text-blue-900">{{ paymentMethod?.lastUsed || 'Never' }}</div>
                        <div class="text-sm text-blue-700">Last Used</div>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Action Buttons -->
                <div v-if="isEditing" class="mt-8 flex justify-end space-x-3 border-t border-gray-200 pt-6">
                  <button
                    type="button"
                    @click="cancelEditing"
                    class="btn-outline"
                  >
                    Cancel
                  </button>
                  <button
                    type="submit"
                    class="btn-primary"
                  >
                    Save Changes
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Delete Confirmation Modal -->
    <div v-if="showDeleteModal" class="fixed inset-0 bg-gray-900 bg-opacity-50 flex items-center justify-center z-50 fade-in">
      <div class="bg-white rounded-xl p-6 shadow-xl w-full max-w-md mx-4">
        <div class="flex justify-between items-center mb-4">
          <h3 class="text-lg font-bold">Remove Payment Method</h3>
          <button @click="showDeleteModal = false" class="text-gray-400 hover:text-gray-500">
            <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>

        <div class="mb-6">
          <p class="text-gray-700 mb-4">
            Are you sure you want to remove this payment method? This action cannot be undone.
          </p>
          <div class="bg-warning-50 text-warning-700 p-3 rounded-md mb-3">
            <p class="text-sm font-medium">
              This will remove: {{ paymentMethod?.brand?.charAt(0).toUpperCase() + paymentMethod?.brand?.slice(1) }} •••• {{ paymentMethod?.last4 }}
            </p>
          </div>
          <label class="flex items-center">
            <input type="checkbox" v-model="confirmDelete" class="h-4 w-4 text-error-600 border-gray-300 rounded focus:ring-error-500" />
            <span class="ml-2 text-sm text-gray-700">I understand this action is permanent</span>
          </label>
        </div>

        <div class="flex justify-end space-x-3">
          <button @click="showDeleteModal = false" class="btn-outline">
            Cancel
          </button>
          <button
            @click="deletePaymentMethod"
            class="btn bg-error-600 text-white hover:bg-error-700 focus:ring-error-500"
            :disabled="!confirmDelete"
            :class="{'opacity-50 cursor-not-allowed': !confirmDelete}"
          >
            Remove Method
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, computed, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';

definePageMeta({
  layout: 'default',
});

const route = useRoute();
const router = useRouter();

const isEditing = ref(false);
const showDeleteModal = ref(false);
const confirmDelete = ref(false);

// Mock payment methods data (in real app, this would come from an API)
const paymentMethodsData = [
  {
    id: 'pm_1',
    type: 'card',
    brand: 'visa',
    last4: '4242',
    expMonth: '12',
    expYear: '25',
    holderName: 'John Doe',
    isDefault: true,
    addedDate: 'March 15, 2024',
    totalTransactions: 24,
    totalAmount: '6,250.00',
    lastUsed: 'April 15, 2025',
    billingAddress: {
      street: '123 Main St',
      city: 'New York',
      state: 'NY',
      postalCode: '10001',
      country: 'United States'
    }
  },
  {
    id: 'pm_2',
    type: 'card',
    brand: 'mastercard',
    last4: '5678',
    expMonth: '08',
    expYear: '24',
    holderName: 'John Doe',
    isDefault: false,
    addedDate: 'January 22, 2024',
    totalTransactions: 12,
    totalAmount: '3,150.00',
    lastUsed: 'March 28, 2025',
    billingAddress: {
      street: '456 Park Ave',
      city: 'San Francisco',
      state: 'CA',
      postalCode: '94107',
      country: 'United States'
    }
  },
  {
    id: 'pm_3',
    type: 'bank',
    bankName: 'Chase Bank',
    accountType: 'checking',
    last4: '9876',
    routingNumber: '021000021',
    accountHolderName: 'John Doe',
    isDefault: false,
    addedDate: 'February 10, 2024',
    totalTransactions: 8,
    totalAmount: '2,100.00',
    lastUsed: 'March 20, 2025',
    billingAddress: {
      street: '789 Bank St',
      city: 'Chicago',
      state: 'IL',
      postalCode: '60601',
      country: 'United States'
    }
  }
];

const paymentMethod = ref(null);
const originalData = ref(null);

// Editable data
const editableData = reactive({
  holderName: '',
  billingAddress: {
    street: '',
    city: '',
    state: '',
    postalCode: '',
    country: 'United States'
  },
  expMonth: '',
  expYear: '',
  accountType: ''
});

// Load payment method data
onMounted(() => {
  const methodId = route.params.id;
  const method = paymentMethodsData.find(pm => pm.id === methodId);

  if (!method) {
    // Redirect back if payment method not found
    router.push('/profile?section=payment');
    return;
  }

  paymentMethod.value = method;
  originalData.value = JSON.parse(JSON.stringify(method));

  // Initialize editable data
  editableData.holderName = method.holderName || method.accountHolderName;
  editableData.billingAddress = { ...method.billingAddress };
  editableData.expMonth = method.expMonth;
  editableData.expYear = method.expYear;
  editableData.accountType = method.accountType;
});

// Start editing
const startEditing = () => {
  isEditing.value = true;
};

// Cancel editing
const cancelEditing = () => {
  // Reset to original values
  editableData.holderName = originalData.value.holderName || originalData.value.accountHolderName;
  editableData.billingAddress = { ...originalData.value.billingAddress };
  editableData.expMonth = originalData.value.expMonth;
  editableData.expYear = originalData.value.expYear;
  editableData.accountType = originalData.value.accountType;
  isEditing.value = false;
};

// Save changes
const saveChanges = () => {
  // In a real app, this would make an API call
  if (paymentMethod.value.type === 'card') {
    paymentMethod.value.holderName = editableData.holderName;
    paymentMethod.value.expMonth = editableData.expMonth;
    paymentMethod.value.expYear = editableData.expYear;
  } else if (paymentMethod.value.type === 'bank') {
    paymentMethod.value.accountHolderName = editableData.holderName;
    paymentMethod.value.accountType = editableData.accountType;
  }
  
  paymentMethod.value.billingAddress = { ...editableData.billingAddress };

  // Update original data
  originalData.value = JSON.parse(JSON.stringify(paymentMethod.value));

  isEditing.value = false;

  // Show success message
  alert('Payment method updated successfully!');
};

// Set as default
const setAsDefault = () => {
  // In a real app, this would make an API call
  paymentMethod.value.isDefault = true;
  alert('Payment method set as default!');
};

// Confirm delete
const confirmDeleteMethod = () => {
  showDeleteModal.value = true;
  confirmDelete.value = false;
};

// Delete payment method
const deletePaymentMethod = () => {
  if (confirmDelete.value) {
    // In a real app, this would make an API call
    alert('Payment method removed successfully!');
    router.push('/profile?section=payment');
  }
};

// Get month name
const getMonthName = (month) => {
  const date = new Date();
  date.setMonth(month - 1);
  return date.toLocaleString('default', { month: 'long' });
};

// Get year options
const getYearOptions = () => {
  const currentYear = new Date().getFullYear();
  const years = [];
  for (let i = 0; i < 10; i++) {
    years.push(currentYear + i);
  }
  return years;
};
</script>
