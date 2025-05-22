<template>
  <div class="fade-in">
    <div class="bg-white shadow">
      <div class="container-custom py-6">
        <h1 class="text-2xl font-bold text-gray-900">My Account</h1>
      </div>
    </div>
    
    <div class="container-custom py-8">
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
        <!-- Profile sidebar -->
        <div class="lg:col-span-1">
          <div class="card mb-6">
            <div class="flex items-center mb-6">
              <div class="h-16 w-16 rounded-full bg-primary-500 text-white flex items-center justify-center mr-4 text-xl font-bold">
                JD
              </div>
              <div>
                <h2 class="text-xl font-bold">John Doe</h2>
                <p class="text-gray-600">john.doe@example.com</p>
              </div>
            </div>
            
            <div class="border-t border-gray-200 pt-4">
              <nav class="space-y-1">
                <button 
                  @click="activeSection = 'personal'"
                  class="w-full flex items-center px-3 py-2 text-sm font-medium rounded-md transition-colors"
                  :class="activeSection === 'personal' ? 'bg-primary-50 text-primary-700' : 'text-gray-700 hover:bg-gray-50 hover:text-gray-900'"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                  </svg>
                  Personal Information
                </button>
                <button 
                  @click="activeSection = 'payment'"
                  class="w-full flex items-center px-3 py-2 text-sm font-medium rounded-md transition-colors"
                  :class="activeSection === 'payment' ? 'bg-primary-50 text-primary-700' : 'text-gray-700 hover:bg-gray-50 hover:text-gray-900'"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
                  </svg>
                  Payment Details
                </button>
                <button 
                  @click="activeSection = 'pending'"
                  class="w-full flex items-center px-3 py-2 text-sm font-medium rounded-md transition-colors"
                  :class="activeSection === 'pending' ? 'bg-primary-50 text-primary-700' : 'text-gray-700 hover:bg-gray-50 hover:text-gray-900'"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                  Pending Payments
                </button>
                <button 
                  @click="activeSection = 'completed'"
                  class="w-full flex items-center px-3 py-2 text-sm font-medium rounded-md transition-colors"
                  :class="activeSection === 'completed' ? 'bg-primary-50 text-primary-700' : 'text-gray-700 hover:bg-gray-50 hover:text-gray-900'"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                  Completed Payments
                </button>
              </nav>
              
              <div class="mt-6 pt-6 border-t border-gray-200">
                <button 
                  @click="logout"
                  class="w-full flex items-center px-3 py-2 text-sm font-medium rounded-md text-error-600 hover:bg-error-50 hover:text-error-700 transition-colors"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1" />
                  </svg>
                  Log Out
                </button>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Profile content -->
        <div class="lg:col-span-2">
          <!-- Personal Details Section -->
          <div v-if="activeSection === 'personal'" class="card">
            <div class="flex justify-between items-center mb-6">
              <h2 class="text-xl font-bold">View/Update Personal Details</h2>
              <div class="flex space-x-2">
                <button 
                  v-if="!isEditing" 
                  @click="startEditing" 
                  class="btn-outline py-1.5 px-3 text-sm"
                >
                  Edit
                </button>
                <button
                  v-if="!isEditing"
                  @click="confirmDeleteAccount"
                  class="btn-outline py-1.5 px-3 text-sm text-error-600 hover:bg-error-50"
                >
                  Delete Account
                </button>
              </div>
            </div>
            
            <form @submit.prevent="saveProfile">
              <div class="space-y-6">
                <div class="grid grid-cols-1 gap-y-6 gap-x-4 sm:grid-cols-6">
                  <div class="sm:col-span-3">
                    <label for="first-name" class="form-label">First Name</label>
                    <input 
                      type="text" 
                      name="first-name" 
                      id="first-name" 
                      autocomplete="given-name" 
                      v-model="profile.firstName"
                      class="form-input"
                      :disabled="!isEditing"
                    />
                  </div>

                  <div class="sm:col-span-3">
                    <label for="last-name" class="form-label">Last Name</label>
                    <input 
                      type="text" 
                      name="last-name" 
                      id="last-name" 
                      autocomplete="family-name" 
                      v-model="profile.lastName"
                      class="form-input"
                      :disabled="!isEditing"
                    />
                  </div>

                  <div class="sm:col-span-6">
                    <label for="email" class="form-label">Email Address</label>
                    <input 
                      type="email" 
                      name="email" 
                      id="email" 
                      autocomplete="email" 
                      v-model="profile.email"
                      class="form-input"
                      disabled
                    />
                    <p class="mt-1 text-sm text-gray-500">
                      For security reasons, email address cannot be changed here. Please contact support.
                    </p>
                  </div>
                  
                  <div class="sm:col-span-6">
                    <label for="phone" class="form-label">Contact Number</label>
                    <div class="flex">
                      <div class="relative">
                        <select 
                          v-model="profile.countryCode" 
                          class="form-input w-28 pl-8 pr-6 focus:ring-2 focus:ring-primary-500 transition-all duration-200 rounded-r-none border-r-0"
                          :disabled="!isEditing"
                        >
                          <option v-for="country in countries" :key="country.code" :value="country.code">
                            {{ country.code }}
                          </option>
                        </select>
                        <span class="absolute inset-y-0 left-3 flex items-center text-gray-400 pointer-events-none">
                          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                          </svg>
                        </span>
                        <span class="absolute inset-y-0 right-2 flex items-center pointer-events-none">
                          <svg class="h-4 w-4 text-gray-500" fill="currentColor" viewBox="0 0 20 20">
                            <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" />
                          </svg>
                        </span>
                      </div>
                      <div class="relative flex-1">
                        <input 
                          type="tel" 
                          name="phone" 
                          id="phone" 
                          autocomplete="tel" 
                          v-model="profile.phoneNumber"
                          class="form-input w-full pl-3 focus:ring-2 focus:ring-primary-500 transition-all duration-200 rounded-l-none"
                          :disabled="!isEditing"
                        />
                      </div>
                    </div>
                  </div>

                  <div class="sm:col-span-6">
                    <label for="address" class="form-label">Address</label>
                    <input 
                      type="text" 
                      name="address" 
                      id="address" 
                      autocomplete="street-address" 
                      v-model="profile.address"
                      class="form-input"
                      :disabled="!isEditing"
                    />
                  </div>
                </div>
              </div>
              
              <div v-if="isEditing" class="mt-6 flex justify-end space-x-3">
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
          
          <!-- Payment Details Section -->
          <div v-if="activeSection === 'payment'" class="card">
            <div class="flex justify-between items-center mb-6">
              <h2 class="text-xl font-bold">Payment Methods</h2>
              <NuxtLink to="/payments/add-method" class="btn-primary py-1.5 px-3 text-sm">
                Add New Method
              </NuxtLink>
            </div>
            
            <div v-if="paymentMethods.length === 0" class="text-center py-8">
              <div class="mx-auto h-12 w-12 text-gray-400 mb-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-full w-full" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
                </svg>
              </div>
              <h3 class="text-lg font-medium text-gray-900 mb-1">No payment methods</h3>
              <p class="text-gray-500 mb-4">You haven't added any payment methods yet.</p>
              <NuxtLink to="/payments/add-method" class="btn-primary">
                Add Payment Method
              </NuxtLink>
            </div>
            
            <div v-else class="space-y-4">
              <!-- Payment method cards -->
              <div 
                v-for="(method, index) in paymentMethods" 
                :key="index"
                class="border border-gray-200 rounded-lg p-4 hover:shadow-sm transition-shadow"
              >
                <div class="flex items-start justify-between">
                  <div class="flex items-center space-x-3">
                    <!-- Card Icon based on type - Replaced with inline SVGs -->
                    <div class="h-10 w-14 flex items-center justify-center rounded bg-gray-50">
                      <!-- Visa Card SVG -->
                      <svg 
                        v-if="method.brand === 'visa'" 
                        xmlns="http://www.w3.org/2000/svg" 
                        viewBox="0 0 48 48" 
                        class="h-6"
                      >
                        <path fill="#1565C0" d="M45,35c0,2.209-1.791,4-4,4H7c-2.209,0-4-1.791-4-4V13c0-2.209,1.791-4,4-4h34c2.209,0,4,1.791,4,4V35z"/>
                        <path fill="#FFF" d="M15.186 19l-2.626 7.832c0 0-.667-3.313-.733-3.729-1.495-3.411-3.701-3.221-3.701-3.221L10.726 30v-.002h3.161L18.258 19H15.186zM17.689 30L20.56 30 22.296 19 19.389 19zM38.008 19h-3.021l-4.71 11h2.852l.588-1.571h3.596L37.619 30h2.613L38.008 19zM34.513 26.328l1.563-4.157.818 4.157H34.513zM26.369 22.206c0-.606.498-1.057 1.926-1.057.928 0 1.991.302 1.991.302l.466-2.158c0 0-1.358-.515-2.691-.515-3.019 0-4.576 1.444-4.576 3.272 0 3.294 3.979 2.824 3.979 4.38 0 .513-.545.884-1.7.884-1.407 0-2.773-.486-2.773-.486l-.495 2.202c0 0 1.303.594 3.132.594 2.744 0 4.576-1.39 4.576-3.258C30.205 23.175 26.369 23.457 26.369 22.206z"/>
                      </svg>
                      
                      <!-- Mastercard SVG -->
                      <svg 
                        v-else-if="method.brand === 'mastercard'" 
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
                        v-else-if="method.brand === 'amex'" 
                        xmlns="http://www.w3.org/2000/svg" 
                        viewBox="0 0 48 48" 
                        class="h-6"
                      >
                        <path fill="#1976D2" d="M45,35c0,2.209-1.791,4-4,4H7c-2.209,0-4-1.791-4-4V13c0-2.209,1.791-4,4-4h34c2.209,0,4,1.791,4,4V35z"/>
                        <path fill="#FFF" d="M22.255 20l-2.113 4.683L18.039 20h-2.695v6.726L12.341 20h-2.274L7 26.981h1.815l.642-1.47h3.312l.642 1.47h3.001v-5.227l2.127 5.227l2.127-5.246v5.246H22.5v-7H22.255zM10.132 24.068l.996-2.3.997 2.3H10.132zM33.5 26.981h2.403L33.5 23.488v-3.507h-3.866l-1.282 2.918L27.117 20H23.25v7H27v-4.99l1.883 2.99h.001v-3.004L30.7 26.981h1.883v-5.1L33.5 26.981zM40.936 26.981h1.815l-3.067-6.999h-2.274l-3.067 6.999h1.815l.642-1.47h3.494L40.936 26.981zM39.678 24.068h-2.178l1.09-2.511L39.678 24.068z"/>
                      </svg>
                      
                      <!-- Generic Card SVG for other card types -->
                      <svg 
                        v-else
                        xmlns="http://www.w3.org/2000/svg" 
                        class="h-6 w-6 text-gray-400" 
                        fill="none" 
                        viewBox="0 0 24 24" 
                        stroke="currentColor"
                      >
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
                      </svg>
                    </div>
                    
                    <div>
                      <div class="font-medium">
                        {{ method.brand.charAt(0).toUpperCase() + method.brand.slice(1) }} •••• {{ method.last4 }}
                        <span 
                          v-if="method.isDefault" 
                          class="ml-2 px-2 py-0.5 text-xs bg-primary-100 text-primary-800 rounded"
                        >
                          Default
                        </span>
                      </div>
                      <div class="text-sm text-gray-500">
                        Expires {{ method.expMonth }}/{{ method.expYear }}
                      </div>
                    </div>
                  </div>
                  
                  <div class="flex space-x-1">
                    <button 
                      v-if="!method.isDefault"
                      @click="setAsDefault(method.id)"
                      class="p-1.5 text-sm text-gray-600 hover:text-primary-600 hover:bg-gray-50 rounded-md"
                      title="Set as default"
                    >
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                      </svg>
                    </button>
                    <button 
                      @click="removePaymentMethod(method.id)"
                      class="p-1.5 text-sm text-gray-600 hover:text-error-600 hover:bg-gray-50 rounded-md"
                      title="Remove"
                    >
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
                      </svg>
                    </button>
                  </div>
                </div>
                
                <div class="mt-3 flex justify-between text-sm">
                  <div class="text-gray-500">
                    {{ method.holderName }}
                  </div>
                  <button 
                    @click="editBillingAddress(method.id)"
                    class="text-primary-600 hover:text-primary-800"
                  >
                    Edit billing address
                  </button>
                </div>
              </div>
            </div>
          </div>
          
          <!-- Pending Payments Section -->
          <div v-if="activeSection === 'pending'" class="card">
            <h2 class="text-xl font-bold mb-6">Pending Payments</h2>
            
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
                  <tr v-for="(payment, index) in pendingPayments" :key="index">
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
                  <tr v-if="pendingPayments.length === 0">
                    <td colspan="5" class="px-6 py-10 text-center text-sm text-gray-500">
                      No pending payments found
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
          
          <!-- Completed Payments Section -->
          <div v-if="activeSection === 'completed'" class="card">
            <h2 class="text-xl font-bold mb-6">Completed Payments</h2>
            
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
                      Amount
                    </th>
                    <th scope="col" class="px-6 py-3 text-right text-xs font-medium text-gray-500 uppercase tracking-wider">
                      Receipt
                    </th>
                  </tr>
                </thead>
                <tbody class="bg-white divide-y divide-gray-200">
                  <tr v-for="(payment, index) in completedPayments" :key="index">
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                      {{ payment.date }}
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                      {{ payment.transactionId }}
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                      {{ payment.description }}
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">
                      ${{ payment.amount.toFixed(2) }}
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                      <button @click="viewReceipt(payment)" class="text-primary-600 hover:text-primary-900">
                        View Receipt
                      </button>
                    </td>
                  </tr>
                  <tr v-if="completedPayments.length === 0">
                    <td colspan="5" class="px-6 py-10 text-center text-sm text-gray-500">
                      No completed payments found
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Delete Account Confirmation Modal -->
    <div v-if="showDeleteModal" class="fixed inset-0 bg-gray-900 bg-opacity-50 flex items-center justify-center z-50 fade-in">
      <div class="bg-white rounded-xl p-6 shadow-xl w-full max-w-md mx-4">
        <div class="flex justify-between items-center mb-4">
          <h3 class="text-lg font-bold">Delete Account</h3>
          <button @click="showDeleteModal = false" class="text-gray-400 hover:text-gray-500">
            <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
        
        <div class="mb-6">
          <p class="text-gray-700 mb-4">Are you sure you want to delete your account? This action cannot be undone, and all your data will be permanently removed.</p>
          <div class="bg-error-50 text-error-700 p-3 rounded-md mb-3">
            <p class="text-sm font-medium">Warning: This will delete all your payment history and account information.</p>
          </div>
          <label class="flex items-center">
            <input type="checkbox" v-model="confirmDelete" class="h-4 w-4 text-primary-600 border-gray-300 rounded focus:ring-primary-500" />
            <span class="ml-2 text-sm text-gray-700">I understand that this action is permanent</span>
          </label>
        </div>
        
        <div class="flex justify-end space-x-3">
          <button @click="showDeleteModal = false" class="btn-outline">
            Cancel
          </button>
          <button 
            @click="deleteAccount" 
            class="btn bg-error-600 text-white hover:bg-error-700 focus:ring-error-500"
            :disabled="!confirmDelete"
            :class="{'opacity-50 cursor-not-allowed': !confirmDelete}"
          >
            Delete Account
          </button>
        </div>
      </div>
    </div>
    
    <!-- Receipt Modal -->
    <div v-if="showReceiptModal" class="fixed inset-0 bg-gray-900 bg-opacity-50 flex items-center justify-center z-50 fade-in">
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
            <p class="text-sm text-gray-500">Receipt for Transaction</p>
          </div>
          
          <div class="space-y-3">
            <div class="flex justify-between">
              <span class="text-gray-600">Transaction ID:</span>
              <span class="font-medium">{{ selectedPayment.transactionId }}</span>
            </div>
            <div class="flex justify-between">
              <span class="text-gray-600">Date:</span>
              <span class="font-medium">{{ selectedPayment.date }}</span>
            </div>
            <div class="flex justify-between">
              <span class="text-gray-600">Description:</span>
              <span class="font-medium">{{ selectedPayment.description }}</span>
            </div>
            <div class="flex justify-between">
              <span class="text-gray-600">Payment Amount:</span>
              <span class="font-bold">${{ selectedPayment.amount?.toFixed(2) }}</span>
            </div>
            <div class="flex justify-between">
              <span class="text-gray-600">Payment Method:</span>
              <span class="font-medium">Credit Card (•••• {{ selectedPayment.last4 }})</span>
            </div>
          </div>
        </div>
        
        <div class="flex justify-end space-x-3">
          <button class="btn-outline flex items-center space-x-2">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4" />
            </svg>
            <span>Download Receipt</span>
          </button>
          <button @click="showReceiptModal = false" class="btn-primary">
            Close
          </button>
        </div>
      </div>
    </div>
    
    <!-- Edit Billing Address Modal -->
    <div v-if="showBillingAddressModal" class="fixed inset-0 bg-gray-900 bg-opacity-50 flex items-center justify-center z-50 fade-in">
      <div class="bg-white rounded-xl p-6 shadow-xl w-full max-w-md mx-4">
        <div class="flex justify-between items-center mb-4">
          <h3 class="text-lg font-bold">Edit Billing Address</h3>
          <button @click="closeBillingAddressModal" class="text-gray-400 hover:text-gray-500">
            <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
        
        <form @submit.prevent="saveBillingAddress">
          <div class="space-y-4 mb-6">
            <div>
              <label for="street-address" class="form-label">Street Address</label>
              <input 
                type="text" 
                id="street-address" 
                v-model="billingAddress.street" 
                class="form-input"
                placeholder="123 Main St"
                required
              />
            </div>
            
            <div class="grid grid-cols-2 gap-4">
              <div>
                <label for="city" class="form-label">City</label>
                <input 
                  type="text" 
                  id="city" 
                  v-model="billingAddress.city" 
                  class="form-input"
                  placeholder="New York"
                  required
                />
              </div>
              <div>
                <label for="state" class="form-label">State</label>
                <input 
                  type="text" 
                  id="state" 
                  v-model="billingAddress.state" 
                  class="form-input"
                  placeholder="NY"
                  required
                />
              </div>
            </div>
            
            <div class="grid grid-cols-2 gap-4">
              <div>
                <label for="postal-code" class="form-label">Postal Code</label>
                <input 
                  type="text" 
                  id="postal-code" 
                  v-model="billingAddress.postalCode" 
                  class="form-input"
                  placeholder="10001"
                  required
                />
              </div>
              <div>
                <label for="country" class="form-label">Country</label>
                <select 
                  id="country" 
                  v-model="billingAddress.country" 
                  class="form-select"
                  required
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
                  <!-- Add more countries as needed -->
                </select>
              </div>
            </div>
          </div>
          
          <div class="flex justify-end space-x-3">
            <button type="button" @click="closeBillingAddressModal" class="btn-outline">
              Cancel
            </button>
            <button type="submit" class="btn-primary">
              Save Address
            </button>
          </div>
        </form>
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
const activeSection = ref('personal');
const showDeleteModal = ref(false);
const confirmDelete = ref(false);
const showReceiptModal = ref(false);
const selectedPayment = ref({});
const showBillingAddressModal = ref(false);
const selectedPaymentMethodId = ref(null);

// Billing address state
const billingAddress = reactive({
  street: '',
  city: '',
  state: '',
  postalCode: '',
  country: 'United States'
});

// Profile editing state
const isEditing = ref(false);
const isEditingPayment = ref(false);

// Country codes for phone numbers
const countries = ref([
  { code: '+1', name: 'United States/Canada' },
  { code: '+44', name: 'United Kingdom' },
  { code: '+91', name: 'India' },
  { code: '+61', name: 'Australia' },
  { code: '+64', name: 'New Zealand' },
  { code: '+49', name: 'Germany' },
  { code: '+33', name: 'France' },
  { code: '+81', name: 'Japan' },
  { code: '+86', name: 'China' },
  { code: '+65', name: 'Singapore' },
  { code: '+971', name: 'United Arab Emirates' },
  { code: '+966', name: 'Saudi Arabia' },
  { code: '+27', name: 'South Africa' },
  { code: '+234', name: 'Nigeria' },
  { code: '+55', name: 'Brazil' },
  { code: '+52', name: 'Mexico' },
  // Add more countries as needed
]);

// Parse the full phone number into country code and phone number
const parsePhoneNumber = (fullPhone) => {
  // Simple parsing - assumes format like "+1 (555) 123-4567"
  const match = fullPhone.match(/^(\+\d+)\s+(.*)/);
  if (match) {
    return {
      countryCode: match[1],
      phoneNumber: match[2]
    };
  }
  return { countryCode: '+1', phoneNumber: fullPhone };
};

// Personal details
const originalProfile = reactive({
  firstName: 'John',
  lastName: 'Doe',
  email: 'john.doe@example.com',
  phone: '+1 (555) 123-4567',
  address: '123 Main Street'
});

// Create a copy of the profile that we can edit
const profile = reactive({ 
  ...originalProfile,
  ...parsePhoneNumber(originalProfile.phone)
});

// Payment details
const originalPaymentDetails = reactive({
  cardHolder: 'John Doe',
  cardNumber: '•••• •••• •••• 4242',
  expiryDate: '12/25',
  cvv: '•••',
  billingAddress: '123 Main Street, New York, NY 10001'
});

const paymentDetails = reactive({ ...originalPaymentDetails });

// Payment methods data
const paymentMethods = ref([
  {
    id: 'pm_1',
    brand: 'visa',
    last4: '4242',
    expMonth: '12',
    expYear: '25',
    holderName: 'John Doe', // Ensure holderName exists
    isDefault: true,
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
    brand: 'mastercard',
    last4: '5678',
    expMonth: '08',
    expYear: '24',
    holderName: 'John Doe', // Ensure holderName exists
    isDefault: false,
    billingAddress: {
      street: '456 Park Ave',
      city: 'San Francisco',
      state: 'CA',
      postalCode: '94107',
      country: 'United States'
    }
  }
]);

// Sample data for pending payments
const pendingPayments = ref([
  {
    id: 'pay_1',
    dueDate: '2025-06-01',
    description: 'Monthly Payment - June 2025',
    amount: 250.00,
    status: 'Upcoming'
  },
  {
    id: 'pay_2',
    dueDate: '2025-05-25',
    description: 'Monthly Payment - May 2025',
    amount: 250.00,
    status: 'Due Soon'
  }
]);

// Sample data for completed payments
const completedPayments = ref([
  {
    id: 'pay_completed_1',
    date: '2025-04-15',
    transactionId: 'TXN123456789',
    description: 'Monthly Payment - April 2025',
    amount: 250.00,
    last4: '4242'
  },
  {
    id: 'pay_completed_2',
    date: '2025-03-15',
    transactionId: 'TXN987654321',
    description: 'Monthly Payment - March 2025',
    amount: 250.00,
    last4: '4242'
  }
]);

// Start editing profile
const startEditing = () => {
  isEditing.value = true;
};

// Cancel editing profile
const cancelEditing = () => {
  // Reset to original values
  Object.assign(profile, originalProfile);
  const parsed = parsePhoneNumber(originalProfile.phone);
  profile.countryCode = parsed.countryCode;
  profile.phoneNumber = parsed.phoneNumber;
  isEditing.value = false;
};

// Save profile changes
const saveProfile = () => {
  // In a real app, you would send these changes to an API
  // For this demo, we'll just update the original profile
  originalProfile.firstName = profile.firstName;
  originalProfile.lastName = profile.lastName;
  originalProfile.address = profile.address;
  originalProfile.phone = `${profile.countryCode} ${profile.phoneNumber}`;
  isEditing.value = false;
  // Show success notification
  alert('Profile updated successfully!');
};

// Start editing mode for payment details
const startEditingPayment = () => {
  isEditingPayment.value = true;
};

// Cancel editing and revert changes for payment details
const cancelEditingPayment = () => {
  // Reset form to original values
  Object.assign(paymentDetails, originalPaymentDetails);
  isEditingPayment.value = false;
};

// Save payment details changes
const savePaymentDetails = () => {
  // In a real app, this would send the updated payment details to the backend
  // For now, just update our local original copy
  Object.assign(originalPaymentDetails, paymentDetails);
  isEditingPayment.value = false;
  
  // Show success message (would be toast notification in real app)
  alert('Payment details updated successfully!');
};

// Set a payment method as default
const setAsDefault = (id) => {
  paymentMethods.value.forEach(method => {
    method.isDefault = method.id === id;
  });
  // In a real app, you would send this change to an API
  alert('Default payment method updated!');
};

// Remove a payment method
const removePaymentMethod = (id) => {
  if (confirm('Are you sure you want to remove this payment method?')) {
    const index = paymentMethods.value.findIndex(method => method.id === id);
    if (index !== -1) {
      paymentMethods.value.splice(index, 1);
      // In a real app, you would send this deletion to an API
      alert('Payment method removed successfully!');
    }
  }
};

// Open edit billing address modal
const editBillingAddress = (id) => {
  selectedPaymentMethodId.value = id;
  const method = paymentMethods.value.find(m => m.id === id);
  
  if (method && method.billingAddress) {
    // Populate the form with existing billing address data
    billingAddress.street = method.billingAddress.street || '';
    billingAddress.city = method.billingAddress.city || '';
    billingAddress.state = method.billingAddress.state || '';
    billingAddress.postalCode = method.billingAddress.postalCode || '';
    billingAddress.country = method.billingAddress.country || 'United States';
  } else {
    // Reset form if no billing address exists
    billingAddress.street = '';
    billingAddress.city = '';
    billingAddress.state = '';
    billingAddress.postalCode = '';
    billingAddress.country = 'United States';
  }
  
  showBillingAddressModal.value = true;
};

// Close billing address modal
const closeBillingAddressModal = () => {
  showBillingAddressModal.value = false;
  selectedPaymentMethodId.value = null;
};

// Save billing address
const saveBillingAddress = () => {
  if (selectedPaymentMethodId.value) {
    const methodIndex = paymentMethods.value.findIndex(m => m.id === selectedPaymentMethodId.value);
    
    if (methodIndex !== -1) {
      // Update the billing address for the selected payment method
      paymentMethods.value[methodIndex].billingAddress = {
        street: billingAddress.street,
        city: billingAddress.city,
        state: billingAddress.state,
        postalCode: billingAddress.postalCode,
        country: billingAddress.country
      };
      
      // In a real app, you would send this update to an API
      alert('Billing address updated successfully!');
    }
  }
  
  // Close the modal
  closeBillingAddressModal();
};

// View receipt
const viewReceipt = (payment) => {
  selectedPayment.value = payment;
  showReceiptModal.value = true;
};

// Confirm delete account
const confirmDeleteAccount = () => {
  showDeleteModal.value = true;
  confirmDelete.value = false;
};

// Delete account
const deleteAccount = () => {
  if (confirmDelete.value) {
    // In a real app, you would send this deletion request to an API
    alert('Account deleted successfully!');
    // Redirect to home/login page
    router.push('/auth/login');
  }
};

// Logout
const logout = () => {
  // In a real app, you would clear session/tokens
  router.push('/auth/login');
};
</script>