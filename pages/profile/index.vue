<template>
  <div class="fade-in">
    <div class="bg-white shadow">
      <div class="container-custom py-6">
        <h1 class="text-2xl font-bold text-gray-900">Your Profile</h1>
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
                <NuxtLink 
                  to="/profile" 
                  class="flex items-center px-3 py-2 text-sm font-medium rounded-md bg-primary-50 text-primary-700"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                  </svg>
                  Personal Information
                </NuxtLink>
                <NuxtLink 
                  to="/profile/security" 
                  class="flex items-center px-3 py-2 text-sm font-medium rounded-md text-gray-700 hover:bg-gray-50 hover:text-gray-900"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
                  </svg>
                  Security
                </NuxtLink>
                <NuxtLink 
                  to="/profile/notifications" 
                  class="flex items-center px-3 py-2 text-sm font-medium rounded-md text-gray-700 hover:bg-gray-50 hover:text-gray-900"
                >
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
                  </svg>
                  Notifications
                </NuxtLink>
              </nav>
            </div>
          </div>
        </div>
        
        <!-- Profile content -->
        <div class="lg:col-span-2">
          <div class="card">
            <div class="flex justify-between items-center mb-6">
              <h2 class="text-xl font-bold">Personal Information</h2>
              <button 
                v-if="!isEditing" 
                @click="startEditing" 
                class="btn-outline py-1.5 px-3 text-sm"
              >
                Edit
              </button>
            </div>
            
            <form @submit.prevent="saveProfile">
              <div class="space-y-6">
                <div class="grid grid-cols-1 gap-y-6 gap-x-4 sm:grid-cols-6">
                  <div class="sm:col-span-3">
                    <label for="first-name" class="form-label">First name</label>
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
                    <label for="last-name" class="form-label">Last name</label>
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
                    <label for="email" class="form-label">Email address</label>
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
                    <label for="phone" class="form-label">Phone number</label>
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

                  <div class="sm:col-span-2">
                    <label for="city" class="form-label">City</label>
                    <input 
                      type="text" 
                      name="city" 
                      id="city" 
                      autocomplete="address-level2" 
                      v-model="profile.city"
                      class="form-input"
                      :disabled="!isEditing"
                    />
                  </div>

                  <div class="sm:col-span-2">
                    <label for="state" class="form-label">State / Province</label>
                    <input 
                      type="text" 
                      name="state" 
                      id="state" 
                      autocomplete="address-level1" 
                      v-model="profile.state"
                      class="form-input"
                      :disabled="!isEditing"
                    />
                  </div>

                  <div class="sm:col-span-2">
                    <label for="postal-code" class="form-label">ZIP / Postal code</label>
                    <input 
                      type="text" 
                      name="postal-code" 
                      id="postal-code" 
                      autocomplete="postal-code" 
                      v-model="profile.postalCode"
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
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue';

definePageMeta({
  layout: 'default',
});

// Profile editing state
const isEditing = ref(false);
const originalProfile = reactive({
  firstName: 'John',
  lastName: 'Doe',
  email: 'john.doe@example.com',
  phone: '+1 (555) 123-4567',
  address: '123 Main Street',
  city: 'New York',
  state: 'NY',
  postalCode: '10001'
});

// Create a copy of the profile that we can edit
const profile = reactive({ ...originalProfile });

// Start editing mode
const startEditing = () => {
  isEditing.value = true;
};

// Cancel editing and revert changes
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
</script>