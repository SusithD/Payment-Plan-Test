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
                    <input 
                      type="tel" 
                      name="phone" 
                      id="phone" 
                      autocomplete="tel" 
                      v-model="profile.phone"
                      class="form-input"
                      :disabled="!isEditing"
                    />
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
              <h2 class="text-xl font-bold">View/Update Payment Details</h2>
              <button 
                v-if="!isEditingPayment" 
                @click="startEditingPayment" 
                class="btn-outline py-1.5 px-3 text-sm"
              >
                Edit
              </button>
            </div>
            
            <form @submit.prevent="savePaymentDetails">
              <div class="space-y-6">
                <div class="grid grid-cols-1 gap-y-6 gap-x-4 sm:grid-cols-6">
                  <div class="sm:col-span-6">
                    <label for="card-holder" class="form-label">Card Holder Name</label>
                    <input 
                      type="text" 
                      name="card-holder" 
                      id="card-holder" 
                      v-model="paymentDetails.cardHolder"
                      class="form-input"
                      :disabled="!isEditingPayment"
                    />
                  </div>
                  
                  <div class="sm:col-span-6">
                    <label for="card-number" class="form-label">Card Number</label>
                    <input 
                      type="text" 
                      name="card-number" 
                      id="card-number" 
                      v-model="paymentDetails.cardNumber"
                      class="form-input"
                      :disabled="!isEditingPayment"
                      placeholder="•••• •••• •••• ••••"
                      maxlength="19"
                    />
                  </div>
                  
                  <div class="sm:col-span-3">
                    <label for="expiry-date" class="form-label">Expiry Date</label>
                    <input 
                      type="text" 
                      name="expiry-date" 
                      id="expiry-date" 
                      v-model="paymentDetails.expiryDate"
                      class="form-input"
                      :disabled="!isEditingPayment"
                      placeholder="MM/YY"
                    />
                  </div>
                  
                  <div class="sm:col-span-3">
                    <label for="cvv" class="form-label">CVV</label>
                    <input 
                      type="password" 
                      name="cvv" 
                      id="cvv" 
                      v-model="paymentDetails.cvv"
                      class="form-input"
                      :disabled="!isEditingPayment"
                      placeholder="•••"
                      maxlength="3"
                    />
                  </div>
                  
                  <div class="sm:col-span-6">
                    <label for="billing-address" class="form-label">Billing Address</label>
                    <input 
                      type="text" 
                      name="billing-address" 
                      id="billing-address" 
                      v-model="paymentDetails.billingAddress"
                      class="form-input"
                      :disabled="!isEditingPayment"
                    />
                  </div>
                </div>
              </div>
              
              <div v-if="isEditingPayment" class="mt-6 flex justify-end space-x-3">
                <button 
                  type="button" 
                  @click="cancelEditingPayment" 
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

// Profile editing state
const isEditing = ref(false);
const isEditingPayment = ref(false);

// Personal details
const originalProfile = reactive({
  firstName: 'John',
  lastName: 'Doe',
  email: 'john.doe@example.com',
  phone: '+1 (555) 123-4567',
  address: '123 Main Street'
});

// Create a copy of the profile that we can edit
const profile = reactive({ ...originalProfile });

// Payment details
const originalPaymentDetails = reactive({
  cardHolder: 'John Doe',
  cardNumber: '•••• •••• •••• 4242',
  expiryDate: '12/25',
  cvv: '•••',
  billingAddress: '123 Main Street, New York, NY 10001'
});

const paymentDetails = reactive({ ...originalPaymentDetails });

// Sample data for pending payments
const pendingPayments = ref([
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
  }
]);

// Sample data for completed payments
const completedPayments = ref([
  {
    date: 'April 15, 2025',
    transactionId: 'TXN-2025-0415',
    description: 'Monthly Instalment',
    amount: 250.00,
    last4: '4242'
  },
  {
    date: 'March 15, 2025',
    transactionId: 'TXN-2025-0315',
    description: 'Monthly Instalment',
    amount: 250.00,
    last4: '4242'
  },
  {
    date: 'February 15, 2025',
    transactionId: 'TXN-2025-0215',
    description: 'Monthly Instalment',
    amount: 250.00,
    last4: '4242'
  }
]);

// Start editing mode for personal details
const startEditing = () => {
  isEditing.value = true;
};

// Cancel editing and revert changes for personal details
const cancelEditing = () => {
  // Reset form to original values
  Object.assign(profile, originalProfile);
  isEditing.value = false;
};

// Save profile changes
const saveProfile = () => {
  // In a real app, this would send the updated profile to the backend
  // For now, just update our local original copy
  Object.assign(originalProfile, profile);
  isEditing.value = false;
  
  // Show success message (would be toast notification in real app)
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

// Show delete account confirmation modal
const confirmDeleteAccount = () => {
  showDeleteModal.value = true;
  confirmDelete.value = false;
};

// Delete account
const deleteAccount = () => {
  if (confirmDelete.value) {
    // In a real app, this would call an API to delete the account
    alert('Account has been deleted. You will be redirected to the homepage.');
    router.push('/');
  }
};

// View receipt for a transaction
const viewReceipt = (payment) => {
  selectedPayment.value = payment;
  showReceiptModal.value = true;
};

// Log out user
const logout = () => {
  // In a real app, this would clear auth tokens, etc.
  router.push('/auth/login');
};
</script>