<template>
  <div class="fade-in bg-gray-50 min-h-screen">
    <!-- Header Section -->
    <section class="bg-gradient-to-r from-primary-600 to-primary-800 text-white">
      <div class="container-custom py-16">
        <div class="max-w-3xl mx-auto text-center">
          <div class="inline-block mb-4">
            <span class="bg-primary-800 text-primary-100 text-sm font-medium py-1 px-3 rounded-full">
              Payment Records
            </span>
          </div>
          <h1 class="text-4xl md:text-5xl font-bold mb-4 text-white">Invoices & Receipts</h1>
          <p class="text-xl text-primary-100 leading-relaxed">
            Access, download, and manage all your payment receipts and tax documents.
          </p>
        </div>
      </div>
    </section>

    <!-- Content Section -->
    <section class="py-16">
      <div class="container-custom">
        <div class="max-w-6xl mx-auto">
          <!-- Filters and Search -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 mb-8">
            <div class="flex flex-col lg:flex-row lg:items-center lg:justify-between gap-4">
              <div class="flex flex-col sm:flex-row gap-4 flex-1">
                <!-- Search -->
                <div class="relative flex-1 max-w-md">
                  <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                    </svg>
                  </div>
                  <input 
                    type="text" 
                    v-model="searchQuery"
                    placeholder="Search invoices..."
                    class="form-input pl-10"
                  />
                </div>
                
                <!-- Date Range Filter -->
                <select v-model="selectedDateRange" class="form-input">
                  <option value="all">All Time</option>
                  <option value="30days">Last 30 Days</option>
                  <option value="90days">Last 3 Months</option>
                  <option value="year">This Year</option>
                  <option value="custom">Custom Range</option>
                </select>
                
                <!-- Status Filter -->
                <select v-model="selectedStatus" class="form-input">
                  <option value="all">All Status</option>
                  <option value="paid">Paid</option>
                  <option value="pending">Pending</option>
                  <option value="overdue">Overdue</option>
                </select>
              </div>
              
              <!-- Actions -->
              <div class="flex gap-3">
                <button 
                  @click="exportInvoices"
                  class="btn btn-outline-primary"
                  :disabled="exporting"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-4-4m4 4l4-4m-6 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                  </svg>
                  {{ exporting ? 'Exporting...' : 'Export' }}
                </button>
                
                <button 
                  @click="generateTaxDocument"
                  class="btn btn-primary"
                  :disabled="generating"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                  </svg>
                  {{ generating ? 'Generating...' : 'Tax Summary' }}
                </button>
              </div>
            </div>
          </div>

          <!-- Statistics Cards -->
          <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-8">
            <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6">
              <div class="flex items-center justify-between">
                <div>
                  <p class="text-sm text-gray-600 mb-1">Total Invoices</p>
                  <p class="text-2xl font-bold text-gray-900">{{ statistics.totalInvoices }}</p>
                </div>
                <div class="h-12 w-12 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                  </svg>
                </div>
              </div>
            </div>
            
            <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6">
              <div class="flex items-center justify-between">
                <div>
                  <p class="text-sm text-gray-600 mb-1">Total Amount</p>
                  <p class="text-2xl font-bold text-gray-900">${{ statistics.totalAmount }}</p>
                </div>
                <div class="h-12 w-12 bg-success-100 text-success-600 rounded-full flex items-center justify-center">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1" />
                  </svg>
                </div>
              </div>
            </div>
            
            <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6">
              <div class="flex items-center justify-between">
                <div>
                  <p class="text-sm text-gray-600 mb-1">This Year</p>
                  <p class="text-2xl font-bold text-gray-900">${{ statistics.thisYear }}</p>
                </div>
                <div class="h-12 w-12 bg-accent-100 text-accent-600 rounded-full flex items-center justify-center">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
                  </svg>
                </div>
              </div>
            </div>
            
            <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6">
              <div class="flex items-center justify-between">
                <div>
                  <p class="text-sm text-gray-600 mb-1">Avg. Payment</p>
                  <p class="text-2xl font-bold text-gray-900">${{ statistics.averagePayment }}</p>
                </div>
                <div class="h-12 w-12 bg-secondary-100 text-secondary-600 rounded-full flex items-center justify-center">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6" />
                  </svg>
                </div>
              </div>
            </div>
          </div>

          <!-- Invoices List -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-100">
            <!-- Table Header -->
            <div class="px-6 py-4 border-b border-gray-100">
              <h2 class="text-xl font-bold text-gray-900">Recent Invoices</h2>
            </div>
            
            <!-- Table Content -->
            <div class="overflow-x-auto">
              <table class="w-full">
                <thead class="bg-gray-50">
                  <tr>
                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Invoice</th>
                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Date</th>
                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Description</th>
                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Amount</th>
                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
                    <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Actions</th>
                  </tr>
                </thead>
                <tbody class="bg-white divide-y divide-gray-200">
                  <tr v-for="invoice in filteredInvoices" :key="invoice.id" class="hover:bg-gray-50">
                    <td class="px-6 py-4 whitespace-nowrap">
                      <div class="flex items-center">
                        <div class="h-8 w-8 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mr-3">
                          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                          </svg>
                        </div>
                        <div>
                          <div class="text-sm font-medium text-gray-900">#{{ invoice.number }}</div>
                          <div class="text-sm text-gray-500">{{ invoice.type }}</div>
                        </div>
                      </div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                      {{ formatDate(invoice.date) }}
                    </td>
                    <td class="px-6 py-4">
                      <div class="text-sm text-gray-900">{{ invoice.description }}</div>
                      <div class="text-sm text-gray-500">{{ invoice.period }}</div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                      <div class="text-sm font-medium text-gray-900">${{ invoice.amount }}</div>
                      <div v-if="invoice.tax" class="text-xs text-gray-500">Tax: ${{ invoice.tax }}</div>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap">
                      <span 
                        class="inline-flex px-2 py-1 text-xs font-semibold rounded-full"
                        :class="{
                          'bg-success-100 text-success-800': invoice.status === 'paid',
                          'bg-warning-100 text-warning-800': invoice.status === 'pending',
                          'bg-error-100 text-error-800': invoice.status === 'overdue'
                        }"
                      >
                        {{ invoice.status.charAt(0).toUpperCase() + invoice.status.slice(1) }}
                      </span>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                      <div class="flex items-center space-x-2">
                        <NuxtLink 
                          :to="`/payments/invoices/${invoice.id}`"
                          class="text-primary-600 hover:text-primary-700 font-medium"
                        >
                          View
                        </NuxtLink>
                        <button 
                          @click="downloadInvoice(invoice)"
                          class="text-secondary-600 hover:text-secondary-700 font-medium"
                          :disabled="downloading === invoice.id"
                        >
                          {{ downloading === invoice.id ? 'Downloading...' : 'Download' }}
                        </button>
                        <button 
                          @click="emailInvoice(invoice)"
                          class="text-accent-600 hover:text-accent-700 font-medium"
                          :disabled="emailing === invoice.id"
                        >
                          {{ emailing === invoice.id ? 'Sending...' : 'Email' }}
                        </button>
                      </div>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
            
            <!-- Pagination -->
            <div class="px-6 py-4 border-t border-gray-100">
              <div class="flex items-center justify-between">
                <div class="text-sm text-gray-700">
                  Showing {{ (currentPage - 1) * itemsPerPage + 1 }} to {{ Math.min(currentPage * itemsPerPage, filteredInvoices.length) }} of {{ filteredInvoices.length }} results
                </div>
                <div class="flex space-x-2">
                  <button 
                    @click="previousPage"
                    :disabled="currentPage === 1"
                    class="px-3 py-1 border border-gray-300 rounded text-sm disabled:opacity-50 disabled:cursor-not-allowed hover:bg-gray-50"
                  >
                    Previous
                  </button>
                  <button 
                    @click="nextPage"
                    :disabled="currentPage >= totalPages"
                    class="px-3 py-1 border border-gray-300 rounded text-sm disabled:opacity-50 disabled:cursor-not-allowed hover:bg-gray-50"
                  >
                    Next
                  </button>
                </div>
              </div>
            </div>
          </div>

          <!-- Tax Information -->
          <div class="mt-8 bg-gradient-to-r from-accent-50 to-accent-100 rounded-xl p-8">
            <div class="flex items-start">
              <div class="h-12 w-12 bg-accent-200 text-accent-700 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                </svg>
              </div>
              <div>
                <h3 class="text-xl font-bold text-accent-900 mb-2">Tax Documentation</h3>
                <p class="text-accent-800 mb-4">All your payment receipts include detailed tax information and can be used for tax filing purposes. Download your annual tax summary for easy filing.</p>
                <div class="flex gap-3">
                  <button 
                    @click="generateTaxDocument"
                    class="btn btn-accent"
                    :disabled="generating"
                  >
                    Generate Tax Summary
                  </button>
                  <NuxtLink to="/support" class="btn btn-outline-accent">
                    Tax Questions?
                  </NuxtLink>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

definePageMeta({
  title: 'Invoices & Receipts - CoverageX Payment Solutions',
  description: 'Access, download, and manage all your payment receipts and tax documents.'
});

// Reactive state
const searchQuery = ref('');
const selectedDateRange = ref('all');
const selectedStatus = ref('all');
const currentPage = ref(1);
const itemsPerPage = ref(10);
const downloading = ref(null);
const emailing = ref(null);
const exporting = ref(false);
const generating = ref(false);

// Statistics
const statistics = ref({
  totalInvoices: 24,
  totalAmount: '6,000.00',
  thisYear: '3,000.00',
  averagePayment: '250.00'
});

// Sample invoices data
const invoices = ref([
  {
    id: 'INV-2025-0001',
    number: '2025-0001',
    type: 'Payment Receipt',
    date: '2025-08-01',
    description: 'Monthly Payment - August 2025',
    period: 'Aug 1 - Aug 31, 2025',
    amount: '250.00',
    tax: '0.00',
    status: 'paid'
  },
  {
    id: 'INV-2025-0002',
    number: '2025-0002',
    type: 'Payment Receipt',
    date: '2025-07-01',
    description: 'Monthly Payment - July 2025',
    period: 'Jul 1 - Jul 31, 2025',
    amount: '250.00',
    tax: '0.00',
    status: 'paid'
  },
  {
    id: 'INV-2025-0003',
    number: '2025-0003',
    type: 'Service Fee',
    date: '2025-07-01',
    description: 'Processing Fee',
    period: 'Jul 1, 2025',
    amount: '2.50',
    tax: '0.23',
    status: 'paid'
  },
  {
    id: 'INV-2025-0004',
    number: '2025-0004',
    type: 'Payment Receipt',
    date: '2025-06-01',
    description: 'Monthly Payment - June 2025',
    period: 'Jun 1 - Jun 30, 2025',
    amount: '250.00',
    tax: '0.00',
    status: 'paid'
  },
  {
    id: 'INV-2025-0005',
    number: '2025-0005',
    type: 'Payment Receipt',
    date: '2025-05-01',
    description: 'Monthly Payment - May 2025',
    period: 'May 1 - May 31, 2025',
    amount: '250.00',
    tax: '0.00',
    status: 'paid'
  }
]);

// Computed properties
const filteredInvoices = computed(() => {
  let filtered = invoices.value;
  
  // Filter by search query
  if (searchQuery.value) {
    const query = searchQuery.value.toLowerCase();
    filtered = filtered.filter(invoice => 
      invoice.number.toLowerCase().includes(query) ||
      invoice.description.toLowerCase().includes(query)
    );
  }
  
  // Filter by status
  if (selectedStatus.value !== 'all') {
    filtered = filtered.filter(invoice => invoice.status === selectedStatus.value);
  }
  
  // Filter by date range
  if (selectedDateRange.value !== 'all') {
    const now = new Date();
    let startDate;
    
    switch (selectedDateRange.value) {
      case '30days':
        startDate = new Date(now.getTime() - 30 * 24 * 60 * 60 * 1000);
        break;
      case '90days':
        startDate = new Date(now.getTime() - 90 * 24 * 60 * 60 * 1000);
        break;
      case 'year':
        startDate = new Date(now.getFullYear(), 0, 1);
        break;
    }
    
    if (startDate) {
      filtered = filtered.filter(invoice => new Date(invoice.date) >= startDate);
    }
  }
  
  return filtered;
});

const totalPages = computed(() => {
  return Math.ceil(filteredInvoices.value.length / itemsPerPage.value);
});

const paginatedInvoices = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage.value;
  const end = start + itemsPerPage.value;
  return filteredInvoices.value.slice(start, end);
});

// Methods
function formatDate(dateString) {
  const date = new Date(dateString);
  return date.toLocaleDateString('en-US', {
    year: 'numeric',
    month: 'short',
    day: 'numeric'
  });
}

async function downloadInvoice(invoice) {
  downloading.value = invoice.id;
  
  try {
    // Simulate download
    await new Promise(resolve => setTimeout(resolve, 1500));
    
    // In a real app, this would trigger a file download
    console.log(`Downloading invoice ${invoice.number}`);
    
  } catch (error) {
    console.error('Error downloading invoice:', error);
  } finally {
    downloading.value = null;
  }
}

async function emailInvoice(invoice) {
  emailing.value = invoice.id;
  
  try {
    // Simulate email sending
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    console.log(`Emailing invoice ${invoice.number}`);
    
  } catch (error) {
    console.error('Error emailing invoice:', error);
  } finally {
    emailing.value = null;
  }
}

async function exportInvoices() {
  exporting.value = true;
  
  try {
    // Simulate export
    await new Promise(resolve => setTimeout(resolve, 2000));
    
    console.log('Exporting invoices');
    
  } catch (error) {
    console.error('Error exporting invoices:', error);
  } finally {
    exporting.value = false;
  }
}

async function generateTaxDocument() {
  generating.value = true;
  
  try {
    // Simulate tax document generation
    await new Promise(resolve => setTimeout(resolve, 3000));
    
    console.log('Generating tax document');
    
  } catch (error) {
    console.error('Error generating tax document:', error);
  } finally {
    generating.value = false;
  }
}

function previousPage() {
  if (currentPage.value > 1) {
    currentPage.value--;
  }
}

function nextPage() {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
  }
}

onMounted(() => {
  // Any initialization logic
});
</script>

<style scoped>
.form-input {
  @apply w-full rounded-lg border-2 border-gray-200 bg-gray-50 shadow-sm focus:border-primary-500 focus:ring focus:ring-primary-500 focus:ring-opacity-50 transition-all duration-200 py-2 px-3;
}

.btn {
  @apply inline-flex items-center justify-center px-4 py-2 border border-transparent text-sm font-medium rounded-lg shadow-sm transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-offset-2;
}

.btn-primary {
  @apply text-white bg-primary-600 hover:bg-primary-700 focus:ring-primary-500;
}

.btn-outline-primary {
  @apply text-primary-600 bg-white border-primary-600 hover:bg-primary-50 focus:ring-primary-500;
}

.btn-accent {
  @apply text-white bg-accent-600 hover:bg-accent-700 focus:ring-accent-500;
}

.btn-outline-accent {
  @apply text-accent-600 bg-white border-accent-600 hover:bg-accent-50 focus:ring-accent-500;
}
</style>