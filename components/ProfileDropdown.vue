<template>
  <div class="relative">
    <button 
      @click="isOpen = !isOpen" 
      type="button" 
      class="flex items-center space-x-3 focus:outline-none"
    >
      <span class="text-gray-700">John Doe</span>
      <div class="h-8 w-8 rounded-full bg-primary-500 text-white flex items-center justify-center">
        JD
      </div>
      <svg 
        xmlns="http://www.w3.org/2000/svg" 
        class="h-5 w-5 text-gray-500" 
        :class="{ 'transform rotate-180': isOpen }"
        fill="none" 
        viewBox="0 0 24 24" 
        stroke="currentColor"
      >
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
      </svg>
    </button>
    
    <!-- Dropdown menu -->
    <div 
      v-if="isOpen"
      class="absolute right-0 mt-2 w-48 rounded-md shadow-lg py-1 bg-white ring-1 ring-black ring-opacity-5 focus:outline-none z-10 fade-in"
    >
      <NuxtLink 
        to="/profile" 
        class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
        @click="isOpen = false"
      >
        Your Profile
      </NuxtLink>
      <NuxtLink 
        to="/settings" 
        class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
        @click="isOpen = false"
      >
        Settings
      </NuxtLink>
      <div class="border-t border-gray-100 my-1"></div>
      <button 
        @click="logout" 
        class="block w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 hover:text-error-600"
      >
        Sign out
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();
const isOpen = ref(false);

// Close dropdown when clicking outside
const handleOutsideClick = (event) => {
  if (isOpen.value && !event.target.closest('.relative')) {
    isOpen.value = false;
  }
};

// Add/remove event listeners
onMounted(() => {
  document.addEventListener('click', handleOutsideClick);
});

onBeforeUnmount(() => {
  document.removeEventListener('click', handleOutsideClick);
});

// Logout function
const logout = () => {
  isOpen.value = false;
  // Would connect to auth store in real app
  router.push('/auth/login');
};
</script>