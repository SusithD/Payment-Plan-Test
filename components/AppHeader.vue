<template>
  <header class="bg-white shadow-sm">
    <div class="container-custom">
      <div class="flex justify-between items-center h-16">
        <!-- Logo -->
        <NuxtLink to="/" class="flex items-center space-x-2">
          <span class="text-[#2C4880] text-xl font-bold">PaymentPlan</span>
        </NuxtLink>
        
        <!-- Navigation -->
        <nav class="hidden md:flex space-x-8">
          <NuxtLink 
            v-for="item in navigationItems" 
            :key="item.name" 
            :to="item.href" 
            class="text-gray-700 hover:text-[#2C4880] font-medium transition-colors duration-200"
            :class="{ 'text-[#2C4880]': route.path === item.href }"
          >
            {{ item.name }}
          </NuxtLink>
        </nav>
        
        <!-- User Menu (Desktop) -->
        <div class="hidden md:flex items-center space-x-4">
          <template v-if="isAuthenticated">
            <ProfileDropdown />
          </template>
          <template v-else>
            <NuxtLink to="/auth/login" class="text-gray-700 hover:text-[#2C4880] font-medium">
              Log in
            </NuxtLink>
            <NuxtLink to="/auth/signup" class="btn-primary">
              Sign up
            </NuxtLink>
          </template>
        </div>
        
        <!-- Mobile Menu Button -->
        <button 
          @click="mobileMenuOpen = !mobileMenuOpen" 
          class="md:hidden p-2 rounded-md text-gray-600 hover:text-gray-900 hover:bg-gray-100 focus:outline-none"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path v-if="mobileMenuOpen" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            <path v-else stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          </svg>
        </button>
      </div>
    </div>
    
    <!-- Mobile Menu -->
    <div 
      v-if="mobileMenuOpen" 
      class="md:hidden bg-white border-t border-gray-200 fade-in"
    >
      <div class="container-custom py-3 space-y-1">
        <NuxtLink 
          v-for="item in navigationItems" 
          :key="item.name" 
          :to="item.href" 
          class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-[#2C4880] hover:bg-gray-50"
          :class="{ 'bg-gray-50 text-[#2C4880]': route.path === item.href }"
          @click="mobileMenuOpen = false"
        >
          {{ item.name }}
        </NuxtLink>
        
        <div class="pt-4 pb-3 border-t border-gray-200">
          <template v-if="isAuthenticated">
            <NuxtLink 
              to="/profile" 
              class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-[#2C4880] hover:bg-gray-50"
              @click="mobileMenuOpen = false"
            >
              Your Profile
            </NuxtLink>
            <NuxtLink 
              to="/settings" 
              class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-[#2C4880] hover:bg-gray-50"
              @click="mobileMenuOpen = false"
            >
              Settings
            </NuxtLink>
            <button 
              @click="logout" 
              class="block w-full text-left px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-error-600 hover:bg-gray-50"
            >
              Sign out
            </button>
          </template>
          <template v-else>
            <NuxtLink 
              to="/auth/login" 
              class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-[#2C4880] hover:bg-gray-50"
              @click="mobileMenuOpen = false"
            >
              Log in
            </NuxtLink>
            <NuxtLink 
              to="/auth/signup" 
              class="block px-3 py-2 rounded-md text-base font-medium bg-[#2C4880] text-white hover:bg-[#1e3563]"
              @click="mobileMenuOpen = false"
            >
              Sign up
            </NuxtLink>
          </template>
        </div>
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref, computed } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();
const mobileMenuOpen = ref(false);

// Mock authentication state - would connect to auth store in real app
const isAuthenticated = ref(false);

// Navigation items
const navigationItems = [
  { name: 'Dashboard', href: '/dashboard' },
  { name: 'Payments', href: '/payments' },
  { name: 'History', href: '/history' },
  { name: 'Support', href: '/support' },
];

// Logout function
const logout = () => {
  isAuthenticated.value = false;
  mobileMenuOpen.value = false;
  router.push('/auth/login');
};
</script>

<style>
.btn-primary {
  @apply bg-[#2C4880] hover:bg-[#1e3563] text-white font-medium py-2 px-4 rounded-lg transition-colors duration-200;
}

.fade-in {
  animation: fadeIn 0.3s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>