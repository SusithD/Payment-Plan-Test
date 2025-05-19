<template>
  <div class="min-h-screen flex flex-col">
    <div class="absolute top-0 left-0 m-6">
      <NuxtLink to="/" class="flex items-center space-x-2">
        <div class="text-primary-600 text-xl font-bold">PaymentPlan</div>
      </NuxtLink>
    </div>
    <main class="flex-grow flex items-center justify-center p-4">
      <slot />
    </main>
    <footer class="w-full py-3 text-center text-gray-500 text-sm">
      <p>&copy; {{ new Date().getFullYear() }} Payment Plan Portal. All rights reserved.</p>
    </footer>
  </div>
</template>

<script setup>
// Auth layout component for login, signup, etc.
</script>