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
import { ref, computed } from 'vue';
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

// Logout function
const logout = () => {
  isAuthenticated.value = false;
  mobileMenuOpen.value = false;
  router.push('/auth/login');
};
</script>

<style scoped>
.container-custom {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 1rem;
}

.btn-primary {
  @apply bg-gradient-to-r from-[#2C4880] to-[#1e3563] hover:from-[#1e3563] hover:to-[#2C4880] text-white font-medium py-2 px-4 rounded-lg transition-all duration-200 shadow-sm hover:shadow-md;
}

.slide-down {
  animation: slideDown 0.3s ease-out;
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Enhanced mobile menu item animation */
.md\:hidden .space-y-1 > * {
  animation: slideInLeft 0.4s ease-out forwards;
  opacity: 0;
  transform: translateX(-20px);
}

@keyframes slideInLeft {
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* Backdrop blur support check */
@supports (backdrop-filter: blur(12px)) {
  .backdrop-blur-md {
    backdrop-filter: blur(12px);
  }
}

/* Fallback for browsers without backdrop-filter support */
@supports not (backdrop-filter: blur(12px)) {
  .bg-white\/95 {
    background-color: rgba(255, 255, 255, 0.98);
  }
}
</style>