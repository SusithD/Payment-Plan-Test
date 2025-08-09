<template>
  <div class="fade-in bg-gray-50 min-h-screen">
    <!-- Header Section -->
    <section class="bg-gradient-to-r from-primary-600 to-primary-800 text-white">
      <div class="container-custom py-16">
        <div class="max-w-3xl mx-auto text-center">
          <div class="inline-block mb-4">
            <span class="bg-primary-800 text-primary-100 text-sm font-medium py-1 px-3 rounded-full">
              Find Everything
            </span>
          </div>
          <h1 class="text-4xl md:text-5xl font-bold mb-4 text-white">Search</h1>
          <p class="text-xl text-primary-100 leading-relaxed">
            Search across payments, transactions, invoices, and support articles.
          </p>
        </div>
      </div>
    </section>

    <!-- Search Section -->
    <section class="py-16">
      <div class="container-custom">
        <div class="max-w-4xl mx-auto">
          <!-- Search Bar -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 mb-8">
            <div class="relative">
              <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                </svg>
              </div>
              <input 
                type="text" 
                v-model="searchQuery"
                @input="handleSearch"
                @keyup.enter="performSearch"
                placeholder="Search payments, transactions, invoices, help articles..."
                class="w-full pl-12 pr-4 py-4 text-lg border-2 border-gray-200 rounded-lg focus:border-primary-500 focus:ring-2 focus:ring-primary-500 focus:ring-opacity-20 transition-all duration-200"
              />
              <div class="absolute inset-y-0 right-0 pr-3 flex items-center">
                <kbd class="hidden sm:inline-flex items-center px-2 py-1 border border-gray-200 rounded text-xs text-gray-500">
                  Enter
                </kbd>
              </div>
            </div>
            
            <!-- Quick Filters -->
            <div class="flex flex-wrap gap-2 mt-4">
              <button 
                v-for="filter in quickFilters" 
                :key="filter.key"
                @click="applyQuickFilter(filter)"
                class="px-3 py-1 text-sm border border-gray-200 rounded-full hover:border-primary-300 hover:bg-primary-50 transition-colors"
                :class="{ 'bg-primary-50 border-primary-300 text-primary-700': selectedFilters.includes(filter.key) }"
              >
                {{ filter.label }}
              </button>
            </div>
          </div>

          <!-- Search Results -->
          <div v-if="searchQuery || hasSearched">
            <!-- Search Stats -->
            <div class="mb-6">
              <p class="text-gray-600">
                <span v-if="searchResults.length > 0">
                  Found {{ searchResults.length }} result{{ searchResults.length !== 1 ? 's' : '' }}
                  <span v-if="searchQuery">for "<strong>{{ searchQuery }}</strong>"</span>
                  <span v-if="searchTime"> in {{ searchTime }}ms</span>
                </span>
                <span v-else-if="hasSearched">
                  No results found
                  <span v-if="searchQuery">for "<strong>{{ searchQuery }}</strong>"</span>
                </span>
              </p>
            </div>

            <!-- Filter Tabs -->
            <div class="bg-white rounded-xl shadow-sm border border-gray-100 mb-6">
              <div class="flex overflow-x-auto">
                <button 
                  v-for="tab in searchTabs" 
                  :key="tab.key"
                  @click="activeTab = tab.key"
                  class="flex-shrink-0 px-6 py-4 text-sm font-medium border-b-2 transition-colors"
                  :class="activeTab === tab.key 
                    ? 'border-primary-500 text-primary-600' 
                    : 'border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300'"
                >
                  {{ tab.label }}
                  <span 
                    v-if="tab.count > 0"
                    class="ml-2 px-2 py-1 text-xs rounded-full"
                    :class="activeTab === tab.key 
                      ? 'bg-primary-100 text-primary-600' 
                      : 'bg-gray-100 text-gray-600'"
                  >
                    {{ tab.count }}
                  </span>
                </button>
              </div>
            </div>

            <!-- Results Content -->
            <div class="space-y-4">
              <div v-for="result in filteredResults" :key="result.id" class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 hover:shadow-md transition-shadow">
                <!-- Payment Results -->
                <div v-if="result.type === 'payment'" class="flex items-start justify-between">
                  <div class="flex items-start flex-1">
                    <div class="h-10 w-10 bg-success-100 text-success-600 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                      </svg>
                    </div>
                    <div class="flex-1">
                      <div class="flex items-center gap-2 mb-2">
                        <h3 class="font-semibold text-gray-900">{{ result.title }}</h3>
                        <span class="text-xs bg-success-100 text-success-800 px-2 py-1 rounded-full">Payment</span>
                      </div>
                      <p class="text-gray-600 text-sm mb-2">{{ result.description }}</p>
                      <div class="flex items-center gap-4 text-xs text-gray-500">
                        <span>{{ result.date }}</span>
                        <span>Transaction ID: {{ result.transactionId }}</span>
                      </div>
                    </div>
                  </div>
                  <div class="text-right">
                    <div class="text-lg font-semibold text-gray-900">${{ result.amount }}</div>
                    <NuxtLink to="/history" class="text-primary-600 hover:text-primary-700 text-sm">View Details</NuxtLink>
                  </div>
                </div>

                <!-- Invoice Results -->
                <div v-else-if="result.type === 'invoice'" class="flex items-start justify-between">
                  <div class="flex items-start flex-1">
                    <div class="h-10 w-10 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                      </svg>
                    </div>
                    <div class="flex-1">
                      <div class="flex items-center gap-2 mb-2">
                        <h3 class="font-semibold text-gray-900">{{ result.title }}</h3>
                        <span class="text-xs bg-primary-100 text-primary-800 px-2 py-1 rounded-full">Invoice</span>
                      </div>
                      <p class="text-gray-600 text-sm mb-2">{{ result.description }}</p>
                      <div class="flex items-center gap-4 text-xs text-gray-500">
                        <span>{{ result.date }}</span>
                        <span>Invoice #{{ result.invoiceNumber }}</span>
                      </div>
                    </div>
                  </div>
                  <div class="text-right">
                    <div class="text-lg font-semibold text-gray-900">${{ result.amount }}</div>
                    <NuxtLink to="/payments/invoices" class="text-primary-600 hover:text-primary-700 text-sm">View Invoice</NuxtLink>
                  </div>
                </div>

                <!-- Article Results -->
                <div v-else-if="result.type === 'article'" class="flex items-start">
                  <div class="h-10 w-10 bg-accent-100 text-accent-600 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                    </svg>
                  </div>
                  <div class="flex-1">
                    <div class="flex items-center gap-2 mb-2">
                      <h3 class="font-semibold text-gray-900">{{ result.title }}</h3>
                      <span class="text-xs bg-accent-100 text-accent-800 px-2 py-1 rounded-full">Help Article</span>
                    </div>
                    <p class="text-gray-600 text-sm mb-2">{{ result.description }}</p>
                    <div class="flex items-center justify-between">
                      <div class="flex items-center gap-4 text-xs text-gray-500">
                        <span>{{ result.category }}</span>
                        <span>{{ result.readTime }} min read</span>
                      </div>
                      <NuxtLink to="/support" class="text-primary-600 hover:text-primary-700 text-sm">Read Article</NuxtLink>
                    </div>
                  </div>
                </div>

                <!-- Transaction Results -->
                <div v-else-if="result.type === 'transaction'" class="flex items-start justify-between">
                  <div class="flex items-start flex-1">
                    <div class="h-10 w-10 bg-secondary-100 text-secondary-600 rounded-full flex items-center justify-center mr-4 flex-shrink-0">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7h12m0 0l-4-4m4 4l-4 4m0 6H4m0 0l4 4m-4-4l4-4" />
                      </svg>
                    </div>
                    <div class="flex-1">
                      <div class="flex items-center gap-2 mb-2">
                        <h3 class="font-semibold text-gray-900">{{ result.title }}</h3>
                        <span class="text-xs bg-secondary-100 text-secondary-800 px-2 py-1 rounded-full">Transaction</span>
                      </div>
                      <p class="text-gray-600 text-sm mb-2">{{ result.description }}</p>
                      <div class="flex items-center gap-4 text-xs text-gray-500">
                        <span>{{ result.date }}</span>
                        <span>{{ result.status }}</span>
                      </div>
                    </div>
                  </div>
                  <div class="text-right">
                    <div class="text-lg font-semibold text-gray-900">${{ result.amount }}</div>
                    <NuxtLink to="/history" class="text-primary-600 hover:text-primary-700 text-sm">View Details</NuxtLink>
                  </div>
                </div>
              </div>
            </div>

            <!-- No Results -->
            <div v-if="searchResults.length === 0 && hasSearched" class="text-center py-12">
              <div class="h-16 w-16 bg-gray-100 text-gray-400 rounded-full flex items-center justify-center mx-auto mb-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                </svg>
              </div>
              <h3 class="text-lg font-semibold text-gray-900 mb-2">No results found</h3>
              <p class="text-gray-600 mb-6">Try adjusting your search terms or filters.</p>
              
              <div class="bg-gray-50 rounded-lg p-4 max-w-md mx-auto">
                <h4 class="font-semibold text-gray-900 mb-2">Search Tips:</h4>
                <ul class="text-sm text-gray-600 space-y-1 text-left">
                  <li>• Try different keywords or synonyms</li>
                  <li>• Check your spelling</li>
                  <li>• Use less specific terms</li>
                  <li>• Try searching by amount or date</li>
                </ul>
              </div>
            </div>
          </div>

          <!-- Popular Searches -->
          <div v-else class="space-y-8">
            <!-- Popular Searches -->
            <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-8">
              <h2 class="text-xl font-bold text-gray-900 mb-6">Popular Searches</h2>
              <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <button 
                  v-for="search in popularSearches" 
                  :key="search.query"
                  @click="performPopularSearch(search.query)"
                  class="flex items-center p-4 text-left border border-gray-200 rounded-lg hover:border-primary-300 hover:bg-primary-50 transition-all"
                >
                  <div class="mr-3">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                    </svg>
                  </div>
                  <div>
                    <div class="font-medium text-gray-900">{{ search.query }}</div>
                    <div class="text-sm text-gray-500">{{ search.description }}</div>
                  </div>
                </button>
              </div>
            </div>

            <!-- Quick Actions -->
            <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-8">
              <h2 class="text-xl font-bold text-gray-900 mb-6">Quick Actions</h2>
              <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <NuxtLink to="/payments" class="flex items-center p-4 border border-gray-200 rounded-lg hover:border-primary-300 hover:bg-primary-50 transition-all">
                  <div class="h-10 w-10 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mr-3">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z" />
                    </svg>
                  </div>
                  <div>
                    <div class="font-semibold text-gray-900">Make Payment</div>
                    <div class="text-sm text-gray-600">Process a new payment</div>
                  </div>
                </NuxtLink>
                
                <NuxtLink to="/history" class="flex items-center p-4 border border-gray-200 rounded-lg hover:border-primary-300 hover:bg-primary-50 transition-all">
                  <div class="h-10 w-10 bg-secondary-100 text-secondary-600 rounded-full flex items-center justify-center mr-3">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
                    </svg>
                  </div>
                  <div>
                    <div class="font-semibold text-gray-900">View History</div>
                    <div class="text-sm text-gray-600">Browse past transactions</div>
                  </div>
                </NuxtLink>
                
                <NuxtLink to="/support" class="flex items-center p-4 border border-gray-200 rounded-lg hover:border-primary-300 hover:bg-primary-50 transition-all">
                  <div class="h-10 w-10 bg-accent-100 text-accent-600 rounded-full flex items-center justify-center mr-3">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                    </svg>
                  </div>
                  <div>
                    <div class="font-semibold text-gray-900">Get Help</div>
                    <div class="text-sm text-gray-600">Browse help articles</div>
                  </div>
                </NuxtLink>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue';

definePageMeta({
  title: 'Search - CoverageX Payment Solutions',
  description: 'Search across payments, transactions, invoices, and support articles.'
});

// Reactive state
const searchQuery = ref('');
const hasSearched = ref(false);
const activeTab = ref('all');
const selectedFilters = ref([]);
const searchTime = ref(null);

// Sample data
const quickFilters = [
  { key: 'recent', label: 'Recent' },
  { key: 'payments', label: 'Payments' },
  { key: 'invoices', label: 'Invoices' },
  { key: 'help', label: 'Help Articles' }
];

const popularSearches = [
  { query: 'payment history', description: 'View your payment transactions' },
  { query: 'make payment', description: 'Process a new payment' },
  { query: 'invoice download', description: 'Download payment receipts' },
  { query: 'payment methods', description: 'Manage payment options' },
  { query: 'account balance', description: 'Check current balance' },
  { query: 'payment schedule', description: 'View upcoming payments' }
];

// Sample search results
const searchResults = ref([]);

const sampleResults = [
  {
    id: 1,
    type: 'payment',
    title: 'Monthly Payment - July 2025',
    description: 'Successful payment for your July installment',
    amount: '250.00',
    date: 'July 15, 2025',
    transactionId: 'TXN-2025-0715-001'
  },
  {
    id: 2,
    type: 'invoice',
    title: 'Payment Receipt - July 2025',
    description: 'Receipt for your July payment installment',
    amount: '250.00',
    date: 'July 15, 2025',
    invoiceNumber: 'INV-2025-0715'
  },
  {
    id: 3,
    type: 'article',
    title: 'How to Set Up Automatic Payments',
    description: 'Learn how to configure automatic payments for your installments',
    category: 'Payment Setup',
    readTime: 3
  },
  {
    id: 4,
    type: 'transaction',
    title: 'Payment Processing Fee',
    description: 'Processing fee for July payment',
    amount: '2.50',
    date: 'July 15, 2025',
    status: 'Completed'
  },
  {
    id: 5,
    type: 'payment',
    title: 'Monthly Payment - June 2025',
    description: 'Successful payment for your June installment',
    amount: '250.00',
    date: 'June 15, 2025',
    transactionId: 'TXN-2025-0615-001'
  }
];

// Computed properties
const searchTabs = computed(() => {
  const tabs = [
    { key: 'all', label: 'All Results', count: searchResults.value.length },
    { key: 'payment', label: 'Payments', count: searchResults.value.filter(r => r.type === 'payment').length },
    { key: 'invoice', label: 'Invoices', count: searchResults.value.filter(r => r.type === 'invoice').length },
    { key: 'article', label: 'Help Articles', count: searchResults.value.filter(r => r.type === 'article').length },
    { key: 'transaction', label: 'Transactions', count: searchResults.value.filter(r => r.type === 'transaction').length }
  ];
  return tabs.filter(tab => tab.key === 'all' || tab.count > 0);
});

const filteredResults = computed(() => {
  if (activeTab.value === 'all') {
    return searchResults.value;
  }
  return searchResults.value.filter(result => result.type === activeTab.value);
});

// Methods
function handleSearch() {
  if (searchQuery.value.length > 2) {
    performSearch();
  } else if (searchQuery.value.length === 0) {
    searchResults.value = [];
    hasSearched.value = false;
  }
}

function performSearch() {
  if (!searchQuery.value.trim()) return;
  
  const startTime = Date.now();
  hasSearched.value = true;
  
  // Simulate search delay
  setTimeout(() => {
    const query = searchQuery.value.toLowerCase();
    const filtered = sampleResults.filter(result => 
      result.title.toLowerCase().includes(query) ||
      result.description.toLowerCase().includes(query) ||
      (result.category && result.category.toLowerCase().includes(query))
    );
    
    searchResults.value = filtered;
    searchTime.value = Date.now() - startTime;
    activeTab.value = 'all';
  }, 300);
}

function performPopularSearch(query) {
  searchQuery.value = query;
  performSearch();
}

function applyQuickFilter(filter) {
  const index = selectedFilters.value.indexOf(filter.key);
  if (index > -1) {
    selectedFilters.value.splice(index, 1);
  } else {
    selectedFilters.value.push(filter.key);
  }
  
  // Apply filter logic here
  if (filter.key === 'payments') {
    activeTab.value = 'payment';
  } else if (filter.key === 'invoices') {
    activeTab.value = 'invoice';
  } else if (filter.key === 'help') {
    activeTab.value = 'article';
  }
}

// Watch for changes
watch(searchQuery, (newValue) => {
  if (newValue.length === 0) {
    searchResults.value = [];
    hasSearched.value = false;
    activeTab.value = 'all';
  }
});
</script>

<style scoped>
/* Custom focus styles for better accessibility */
input:focus {
  outline: none;
}

.form-input {
  @apply transition-all duration-200;
}
</style>