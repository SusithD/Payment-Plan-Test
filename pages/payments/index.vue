<template>
  <div class="fade-in">
    <div class="bg-white shadow">
      <div class="container-custom py-6">
        <h1 class="text-2xl font-bold text-gray-900">Make a Payment</h1>
      </div>
    </div>
    
    <div class="container-custom py-8">
      <!-- Pending Instalments Section -->
      <div class="card mb-8">
        <div class="flex flex-col md:flex-row md:justify-between md:items-center mb-6">
          <h2 class="text-xl font-bold mb-2 md:mb-0">Pending Instalments</h2>
          <div class="flex flex-col sm:flex-row space-y-2 sm:space-y-0 sm:space-x-3">
            <div class="relative">
              <select 
                v-model="sortBy" 
                class="form-input pr-10 py-2 text-sm"
              >
                <option value="dueDate">Sort by Due Date</option>
                <option value="amount">Sort by Amount</option>
                <option value="status">Sort by Status</option>
              </select>
              <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
                <svg class="h-4 w-4" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd"></path>
                </svg>
              </div>
            </div>
            <div class="relative">
              <select 
                v-model="filterStatus" 
                class="form-input pr-10 py-2 text-sm"
              >
                <option value="all">All Statuses</option>
                <option value="dueSoon">Due Soon</option>
                <option value="upcoming">Upcoming</option>
                <option value="overdue">Overdue</option>
              </select>
              <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
                <svg class="h-4 w-4" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd"></path>
                </svg>
              </div>
            </div>
          </div>
        </div>
        
        <div class="overflow-x-auto">
          <table class="min-w-full divide-y divide-gray-200">
            <thead class="bg-gray-50">
              <tr>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  <div class="flex items-center">
                    <input 
                      type="checkbox" 
                      :checked="selectAll" 
                      @change="toggleSelectAll" 
                      class="h-4 w-4 text-primary-600 border-gray-300 rounded focus:ring-primary-500" 
                    />
                  </div>
                </th>
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
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Actions
                </th>
              </tr>
            </thead>
            <tbody class="bg-white divide-y divide-gray-200">
              <tr v-for="(instalment, index) in filteredInstalments" :key="index">
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="flex items-center">
                    <input 
                      type="checkbox" 
                      v-model="instalment.selected" 
                      @change="updateSelectedInstalments" 
                      class="h-4 w-4 text-primary-600 border-gray-300 rounded focus:ring-primary-500" 
                    />
                  </div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                  {{ instalment.dueDate }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                  {{ instalment.description }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">
                  ${{ instalment.amount.toFixed(2) }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <span 
                    class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full" 
                    :class="{
                      'bg-warning-100 text-warning-800': instalment.status === 'Due Soon',
                      'bg-error-100 text-error-800': instalment.status === 'Overdue',
                      'bg-gray-100 text-gray-800': instalment.status === 'Upcoming'
                    }"
                  >
                    {{ instalment.status }}
                  </span>
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-sm">
                  <button 
                    @click="viewDetails(instalment)" 
                    class="text-primary-600 hover:text-primary-900 mr-3"
                  >
                    View Details
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      
      <!-- Payment Summary Section -->
      <div class="card bg-gray-50">
        <h2 class="text-xl font-bold mb-6">Payment Summary</h2>
        
        <div class="space-y-4 mb-6">
          <div class="flex justify-between">
            <span class="text-gray-600">Selected Instalments:</span>
            <span class="font-medium">{{ selectedInstalments.length }}</span>
          </div>
          <div class="flex justify-between">
            <span class="text-gray-600">Total Amount:</span>
            <span class="font-bold">${{ getTotalAmount.toFixed(2) }}</span>
          </div>
        </div>
        
        <div class="text-right">
          <button 
            @click="proceedToPayment" 
            class="btn-primary px-6"
            :disabled="!hasSelectedInstalments"
            :class="{'opacity-50 cursor-not-allowed': !hasSelectedInstalments}"
          >
            Proceed to Payment
          </button>
        </div>
      </div>
    </div>
    
    <!-- Instalment Details Modal -->
    <div 
      v-if="showDetailsModal" 
      class="fixed inset-0 bg-gray-900 bg-opacity-50 flex items-center justify-center z-50 fade-in"
    >
      <div class="bg-white rounded-xl p-6 shadow-xl w-full max-w-md mx-4">
        <div class="flex justify-between items-center mb-4">
          <h3 class="text-lg font-bold">Instalment Details</h3>
          <button @click="showDetailsModal = false" class="text-gray-400 hover:text-gray-500">
            <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
        
        <div class="space-y-4">
          <div>
            <p class="text-sm text-gray-500">Description</p>
            <p class="font-medium">{{ selectedInstalment.description }}</p>
          </div>
          <div>
            <p class="text-sm text-gray-500">Due Date</p>
            <p class="font-medium">{{ selectedInstalment.dueDate }}</p>
          </div>
          <div>
            <p class="text-sm text-gray-500">Amount</p>
            <p class="font-medium">${{ selectedInstalment.amount?.toFixed(2) }}</p>
          </div>
          <div>
            <p class="text-sm text-gray-500">Status</p>
            <span 
              class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full" 
              :class="{
                'bg-warning-100 text-warning-800': selectedInstalment.status === 'Due Soon',
                'bg-error-100 text-error-800': selectedInstalment.status === 'Overdue',
                'bg-gray-100 text-gray-800': selectedInstalment.status === 'Upcoming'
              }"
            >
              {{ selectedInstalment.status }}
            </span>
          </div>
          <div>
            <p class="text-sm text-gray-500">Payment Reference</p>
            <p class="font-medium">{{ selectedInstalment.reference }}</p>
          </div>
        </div>
        
        <div class="mt-6 flex justify-end space-x-3">
          <button @click="showDetailsModal = false" class="btn-outline">
            Close
          </button>
          <button 
            @click="payInstalment(selectedInstalment)"
            class="btn-primary"
          >
            Pay Now
          </button>
        </div>
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
const sortBy = ref('dueDate');
const filterStatus = ref('all');
const showDetailsModal = ref(false);
const selectedInstalment = ref({});
const selectAll = ref(false);

// Mock data - would be fetched from an API in a real application
const instalments = ref([
  {
    id: 1,
    dueDate: 'May 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Due Soon',
    reference: 'INS-2025-0501',
    selected: false
  },
  {
    id: 2,
    dueDate: 'June 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Upcoming',
    reference: 'INS-2025-0601',
    selected: false
  },
  {
    id: 3,
    dueDate: 'July 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Upcoming',
    reference: 'INS-2025-0701',
    selected: false
  },
  {
    id: 4,
    dueDate: 'August 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Upcoming',
    reference: 'INS-2025-0801',
    selected: false
  },
  {
    id: 5,
    dueDate: 'September 15, 2025',
    description: 'Monthly Instalment',
    amount: 250.00,
    status: 'Upcoming',
    reference: 'INS-2025-0901',
    selected: false
  }
]);

// Computed for filtered and sorted instalments
const filteredInstalments = computed(() => {
  let result = [...instalments.value];
  
  // Apply status filter
  if (filterStatus.value !== 'all') {
    const statusMap = {
      'dueSoon': 'Due Soon',
      'upcoming': 'Upcoming',
      'overdue': 'Overdue'
    };
    result = result.filter(item => item.status === statusMap[filterStatus.value]);
  }
  
  // Apply sorting
  result.sort((a, b) => {
    if (sortBy.value === 'dueDate') {
      return new Date(a.dueDate) - new Date(b.dueDate);
    } else if (sortBy.value === 'amount') {
      return a.amount - b.amount;
    } else if (sortBy.value === 'status') {
      return a.status.localeCompare(b.status);
    }
    return 0;
  });
  
  return result;
});

// Computed for selected instalments
const selectedInstalments = computed(() => {
  return instalments.value.filter(item => item.selected);
});

// Computed for total amount
const getTotalAmount = computed(() => {
  return selectedInstalments.value.reduce((sum, item) => sum + item.amount, 0);
});

// Computed to check if any instalment is selected
const hasSelectedInstalments = computed(() => {
  return selectedInstalments.value.length > 0;
});

// Method to view details
const viewDetails = (instalment) => {
  selectedInstalment.value = instalment;
  showDetailsModal.value = true;
};

// Method to pay a single instalment
const payInstalment = (instalment) => {
  // Set this instalment as the only selected one
  instalments.value.forEach(item => {
    item.selected = item.id === instalment.id;
  });
  
  showDetailsModal.value = false;
  proceedToPayment();
};

// Method to toggle select all
const toggleSelectAll = () => {
  selectAll.value = !selectAll.value;
  instalments.value.forEach(item => {
    item.selected = selectAll.value;
  });
};

// Method to update selected instalments state
const updateSelectedInstalments = () => {
  const allSelected = instalments.value.every(item => item.selected);
  const someSelected = instalments.value.some(item => item.selected);
  
  selectAll.value = allSelected;
};

// Method to proceed to payment review
const proceedToPayment = () => {
  // Would store selected instalments in state management in a real app
  router.push('/payments/review');
};
</script>