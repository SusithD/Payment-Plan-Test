<template>
  <header class="bg-white/95 backdrop-blur-md shadow-sm border-b border-gray-100 sticky top-0 z-50">
    <div class="container-custom">
      <div class="flex justify-between items-center h-16">
        <!-- Logo with enhanced styling -->
        <NuxtLink to="/" class="flex items-center space-x-3 group">
          <div class="relative">
            <div class="h-8 w-8 bg-gradient-to-br from-primary-500 to-primary-700 rounded-lg flex items-center justify-center group-hover:scale-105 transition-transform duration-200">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            </div>
            <div class="absolute -inset-0.5 bg-gradient-to-br from-primary-500 to-primary-700 rounded-lg opacity-0 group-hover:opacity-20 transition-opacity duration-200"></div>
          </div>
          <span class="text-[#2C4880] text-xl font-bold bg-gradient-to-r from-[#2C4880] to-[#1e3563] bg-clip-text text-transparent group-hover:from-primary-600 group-hover:to-primary-800 transition-all duration-200">PaymentPlan</span>
        </NuxtLink>
        
        <!-- Enhanced Navigation -->
        <nav class="hidden md:flex items-center space-x-1">
          <NuxtLink 
            v-for="item in navigationItems" 
            :key="item.name" 
            :to="item.href" 
            class="relative px-4 py-2 rounded-lg font-medium transition-all duration-200 group"
            :class="getNavLinkClass(item.href)"
          >
            <span class="relative z-10">{{ item.name }}</span>
            <!-- Active indicator -->
            <div 
              v-if="route.path === item.href" 
              class="absolute inset-0 bg-gradient-to-r from-primary-50 to-primary-100 rounded-lg"
            ></div>
            <!-- Hover effect -->
            <div class="absolute inset-0 bg-gray-50 rounded-lg opacity-0 group-hover:opacity-100 transition-opacity duration-200"></div>
            <!-- Icon for each nav item -->
            <div class="absolute -bottom-1 left-1/2 transform -translate-x-1/2 w-1 h-1 bg-primary-500 rounded-full opacity-0 transition-opacity duration-200" :class="{ 'opacity-100': route.path === item.href }"></div>
          </NuxtLink>
        </nav>
        
        <!-- Search Bar (Desktop) -->
        <div class="hidden lg:flex items-center flex-1 max-w-lg mx-8">
          <div class="relative w-full">
            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
              </svg>
            </div>
            <input 
              type="text" 
              v-model="searchQuery"
              @keyup.enter="performSearch"
              @focus="showSearchSuggestions = true"
              @blur="hideSearchSuggestions"
              placeholder="Search payments, invoices, help..."
              class="w-full pl-10 pr-4 py-2 text-sm border border-gray-200 rounded-lg focus:border-primary-500 focus:ring-1 focus:ring-primary-500 transition-all duration-200 bg-gray-50 focus:bg-white"
            />
            <div class="absolute inset-y-0 right-0 pr-3 flex items-center">
              <kbd class="hidden sm:inline-flex items-center px-1.5 py-0.5 border border-gray-200 rounded text-xs text-gray-500 bg-white">
                ⌘K
              </kbd>
            </div>
            
            <!-- Search Suggestions Dropdown -->
            <div 
              v-if="showSearchSuggestions && (searchQuery.length > 0 || popularSearches.length > 0)"
              class="absolute top-full left-0 right-0 mt-1 bg-white rounded-lg shadow-lg border border-gray-200 z-50 max-h-80 overflow-y-auto"
            >
              <!-- Quick Results -->
              <div v-if="searchQuery.length > 2 && quickResults.length > 0" class="border-b border-gray-100 p-2">
                <div class="text-xs font-medium text-gray-500 uppercase tracking-wide px-2 py-1">Quick Results</div>
                <div 
                  v-for="result in quickResults.slice(0, 3)" 
                  :key="result.id"
                  @mousedown="navigateToResult(result)"
                  class="flex items-center px-2 py-2 hover:bg-gray-50 rounded cursor-pointer"
                >
                  <div class="h-6 w-6 rounded-full flex items-center justify-center mr-2"
                       :class="getResultIconClass(result.type)">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-3 w-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path v-if="result.type === 'payment'" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                      <path v-else-if="result.type === 'invoice'" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                      <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                    </svg>
                  </div>
                  <div class="flex-1 min-w-0">
                    <div class="text-sm font-medium text-gray-900 truncate">{{ result.title }}</div>
                    <div class="text-xs text-gray-500 truncate">{{ result.description }}</div>
                  </div>
                  <div v-if="result.amount" class="text-xs font-medium text-gray-700">${{ result.amount }}</div>
                </div>
              </div>
              
              <!-- Popular Searches -->
              <div v-if="searchQuery.length === 0" class="p-2">
                <div class="text-xs font-medium text-gray-500 uppercase tracking-wide px-2 py-1">Popular Searches</div>
                <div 
                  v-for="search in popularSearches.slice(0, 4)" 
                  :key="search.query"
                  @mousedown="performPopularSearch(search.query)"
                  class="flex items-center px-2 py-2 hover:bg-gray-50 rounded cursor-pointer"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-gray-400 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                  </svg>
                  <div class="flex-1">
                    <div class="text-sm text-gray-900">{{ search.query }}</div>
                  </div>
                </div>
              </div>
              
              <!-- View All Results -->
              <div v-if="searchQuery.length > 0" class="border-t border-gray-100 p-2">
                <button 
                  @mousedown="viewAllResults"
                  class="w-full flex items-center justify-center px-2 py-2 text-sm text-primary-600 hover:text-primary-700 hover:bg-primary-50 rounded"
                >
                  View all results for "{{ searchQuery }}"
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                  </svg>
                </button>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Enhanced User Menu (Desktop) -->
        <div class="hidden md:flex items-center space-x-3">
          <!-- Notifications Bell -->
          <div class="relative">
            <button class="p-2 rounded-lg text-gray-500 hover:text-gray-700 hover:bg-gray-100 transition-all duration-200 relative group">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
              </svg>
              <!-- Notification dot -->
              <div class="absolute -top-0.5 -right-0.5 h-3 w-3 bg-red-500 rounded-full flex items-center justify-center">
                <div class="h-1.5 w-1.5 bg-white rounded-full"></div>
              </div>
            </button>
          </div>

          <template v-if="isAuthenticated">
            <ProfileDropdown />
          </template>
          <template v-else>
            <NuxtLink 
              to="/auth/login" 
              class="px-4 py-2 text-gray-700 hover:text-[#2C4880] font-medium rounded-lg transition-all duration-200 hover:bg-gray-50"
            >
              Log in
            </NuxtLink>
            <NuxtLink 
              to="/auth/signup" 
              class="btn-primary group relative overflow-hidden"
            >
              <span class="relative z-10">Sign up</span>
              <div class="absolute inset-0 bg-gradient-to-r from-primary-600 to-primary-700 opacity-0 group-hover:opacity-100 transition-opacity duration-200"></div>
            </NuxtLink>
          </template>
        </div>
        
        <!-- Enhanced Mobile Menu Button -->
        <button 
          @click="mobileMenuOpen = !mobileMenuOpen" 
          class="md:hidden p-2 rounded-lg text-gray-600 hover:text-gray-900 hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-primary-500 focus:ring-offset-2 transition-all duration-200 relative group"
        >
          <div class="relative w-6 h-6">
            <!-- Hamburger to X animation -->
            <span 
              class="absolute h-0.5 w-6 bg-current transform transition-all duration-300 ease-in-out"
              :class="mobileMenuOpen ? 'rotate-45 translate-y-2.5' : 'translate-y-1'"
            ></span>
            <span 
              class="absolute h-0.5 w-6 bg-current transform transition-all duration-300 ease-in-out translate-y-2.5"
              :class="mobileMenuOpen ? 'opacity-0' : 'opacity-100'"
            ></span>
            <span 
              class="absolute h-0.5 w-6 bg-current transform transition-all duration-300 ease-in-out"
              :class="mobileMenuOpen ? '-rotate-45 translate-y-2.5' : 'translate-y-4'"
            ></span>
          </div>
        </button>
      </div>
    </div>
    
    <!-- Enhanced Mobile Menu -->
    <div 
      v-if="mobileMenuOpen" 
      class="md:hidden bg-white/95 backdrop-blur-md border-t border-gray-100 slide-down"
    >
      <div class="container-custom py-4 space-y-2">
        <!-- Mobile Navigation Items -->
        <div class="space-y-1">
          <NuxtLink 
            v-for="(item, index) in navigationItems" 
            :key="item.name" 
            :to="item.href" 
            class="flex items-center px-4 py-3 rounded-xl text-base font-medium transition-all duration-200 group"
            :class="getMobileNavLinkClass(item.href)"
            :style="{ animationDelay: `${index * 50}ms` }"
            @click="mobileMenuOpen = false"
          >
            <div class="flex items-center space-x-3">
              <!-- Icon for each nav item -->
              <div class="flex-shrink-0 w-6 h-6 rounded-md flex items-center justify-center" :class="item.href === route.path ? 'bg-primary-100' : 'bg-gray-100'">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" :class="item.href === route.path ? 'text-primary-600' : 'text-gray-500'" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path v-if="item.name === 'Dashboard'" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z" />
                  <path v-else-if="item.name === 'Payments'" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                  <path v-else-if="item.name === 'History'" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                  <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18.364 5.636l-3.536 3.536m0 5.656l3.536 3.536M9.172 9.172L5.636 5.636m3.536 9.192L5.636 18.364M21 12a9 9 0 11-18 0 9 9 0 0118 0zm-5 0a4 4 0 11-8 0 4 4 0 018 0z" />
                </svg>
              </div>
              <span>{{ item.name }}</span>
            </div>
            <!-- Arrow indicator for active item -->
            <svg v-if="item.href === route.path" xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-auto text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
            </svg>
          </NuxtLink>
        </div>
        
        <!-- Mobile User Menu -->
        <div class="pt-4 mt-4 border-t border-gray-200">
          <template v-if="isAuthenticated">
            <div class="space-y-1">
              <NuxtLink 
                to="/profile" 
                class="flex items-center px-4 py-3 rounded-xl text-base font-medium text-gray-700 hover:text-[#2C4880] hover:bg-gray-50 transition-all duration-200"
                @click="mobileMenuOpen = false"
              >
                <div class="flex items-center space-x-3">
                  <div class="w-6 h-6 bg-gray-100 rounded-md flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                    </svg>
                  </div>
                  <span>Your Profile</span>
                </div>
              </NuxtLink>
              <NuxtLink 
                to="/settings" 
                class="flex items-center px-4 py-3 rounded-xl text-base font-medium text-gray-700 hover:text-[#2C4880] hover:bg-gray-50 transition-all duration-200"
                @click="mobileMenuOpen = false"
              >
                <div class="flex items-center space-x-3">
                  <div class="w-6 h-6 bg-gray-100 rounded-md flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-gray-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                    </svg>
                  </div>
                  <span>Settings</span>
                </div>
              </NuxtLink>
              <button 
                @click="logout" 
                class="flex items-center w-full px-4 py-3 rounded-xl text-base font-medium text-red-600 hover:text-red-700 hover:bg-red-50 transition-all duration-200"
              >
                <div class="flex items-center space-x-3">
                  <div class="w-6 h-6 bg-red-100 rounded-md flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-red-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1" />
                    </svg>
                  </div>
                  <span>Sign out</span>
                </div>
              </button>
            </div>
          </template>
          <template v-else>
            <div class="space-y-2">
              <NuxtLink 
                to="/auth/login" 
                class="flex items-center justify-center px-4 py-3 rounded-xl text-base font-medium text-gray-700 hover:text-[#2C4880] hover:bg-gray-50 border border-gray-200 transition-all duration-200"
                @click="mobileMenuOpen = false"
              >
                Log in
              </NuxtLink>
              <NuxtLink 
                to="/auth/signup" 
                class="flex items-center justify-center px-4 py-3 rounded-xl text-base font-medium bg-gradient-to-r from-[#2C4880] to-[#1e3563] text-white hover:from-[#1e3563] hover:to-[#2C4880] transition-all duration-200"
                @click="mobileMenuOpen = false"
              >
                Sign up
              </NuxtLink>
            </div>
          </template>
        </div>
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref, computed, watch, onMounted } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();
const mobileMenuOpen = ref(false);

// Mock authentication state - would connect to auth store in real app
const isAuthenticated = ref(false);

// Navigation items with analytics addition
const navigationItems = [
  { name: 'Dashboard', href: '/dashboard' },
  { name: 'Payments', href: '/payments' },
  { name: 'History', href: '/history' },
  { name: 'Analytics', href: '/analytics' },
  { name: 'Support', href: '/support' },
];

// Enhanced nav link styling
const getNavLinkClass = (href) => {
  return route.path === href 
    ? 'text-[#2C4880] bg-gradient-to-r from-primary-50 to-primary-100' 
    : 'text-gray-700 hover:text-[#2C4880] hover:bg-gray-50';
};

const getMobileNavLinkClass = (href) => {
  return route.path === href 
    ? 'text-[#2C4880] bg-gradient-to-r from-primary-50 to-primary-100 border-l-4 border-primary-500' 
    : 'text-gray-700 hover:text-[#2C4880] hover:bg-gray-50';
};

// Search functionality
const searchQuery = ref('');
const showSearchSuggestions = ref(false);
const quickResults = ref([]);
const popularSearches = ref([
  { query: 'payment history', description: 'View your payment transactions' },
  { query: 'make payment', description: 'Process a new payment' },
  { query: 'invoice download', description: 'Download payment receipts' },
  { query: 'payment methods', description: 'Manage payment options' }
]);

// Sample quick results data
const sampleResults = [
  {
    id: 1,
    type: 'payment',
    title: 'Monthly Payment - July 2025',
    description: 'Successful payment for July installment',
    amount: '250.00',
    url: '/history'
  },
  {
    id: 2,
    type: 'invoice',
    title: 'Payment Receipt - July 2025',
    description: 'Receipt for July payment',
    amount: '250.00',
    url: '/payments/invoices/INV-2025-0701'
  },
  {
    id: 3,
    type: 'article',
    title: 'How to Set Up AutoPay',
    description: 'Learn how to configure automatic payments',
    url: '/support'
  }
];

// Watch for search query changes to trigger quick search
watch(searchQuery, (newValue) => {
  if (newValue.length > 2) {
    performQuickSearch();
  } else {
    quickResults.value = [];
  }
});

// Get result icon class based on type
const getResultIconClass = (type) => {
  switch (type) {
    case 'payment':
      return 'bg-success-100 text-success-600';
    case 'invoice':
      return 'bg-primary-100 text-primary-600';
    case 'article':
      return 'bg-accent-100 text-accent-600';
    default:
      return 'bg-gray-100 text-gray-600';
  }
};

// Perform quick search for dropdown suggestions
const performQuickSearch = () => {
  const query = searchQuery.value.toLowerCase();
  quickResults.value = sampleResults.filter(result => 
    result.title.toLowerCase().includes(query) ||
    result.description.toLowerCase().includes(query)
  );
};

// Navigate to search result
const navigateToResult = (result) => {
  hideSearchSuggestions();
  router.push(result.url);
  searchQuery.value = '';
};

// Perform search action
const performSearch = () => {
  if (searchQuery.value.trim() === '') return;
  hideSearchSuggestions();
  router.push(`/search?q=${encodeURIComponent(searchQuery.value)}`);
};

// Perform popular search action
const performPopularSearch = (query) => {
  searchQuery.value = query;
  hideSearchSuggestions();
  router.push(`/search?q=${encodeURIComponent(query)}`);
};

// View all results action
const viewAllResults = () => {
  if (searchQuery.value.trim() === '') return;
  hideSearchSuggestions();
  router.push(`/search?q=${encodeURIComponent(searchQuery.value)}`);
};

// Hide search suggestions with delay for click events
const hideSearchSuggestions = () => {
  setTimeout(() => {
    showSearchSuggestions.value = false;
  }, 150);
};

// Keyboard shortcut for search (Cmd+K)
onMounted(() => {
  const handleKeydown = (e) => {
    if ((e.metaKey || e.ctrlKey) && e.key === 'k') {
      e.preventDefault();
      const searchInput = document.querySelector('input[placeholder*="Search"]');
      if (searchInput) {
        searchInput.focus();
      }
    }
  };
  
  document.addEventListener('keydown', handleKeydown);
  
  return () => {
    document.removeEventListener('keydown', handleKeydown);
  };
});

// Logout function
const logout = () => {
  isAuthenticated.value = false;
  mobileMenuOpen.value = false;
  router.push('/auth/login');
};
</script>