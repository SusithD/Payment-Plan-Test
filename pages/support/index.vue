<template>
  <div class="fade-in bg-gray-50">
    <!-- Top Stats Bar -->
    <div class="bg-white shadow-sm">
      <div class="container-custom py-4">
        <div class="flex flex-wrap items-center justify-between">
          <div>
            <h1 class="text-xl font-bold text-gray-900">Support Center</h1>
            <div class="flex items-center">
              <span class="text-sm text-gray-600">Get help and support for your payment plans</span>
              <span class="mx-2 text-gray-300">•</span>
              <span class="text-sm text-gray-600">{{ currentDate }}</span>
            </div>
          </div>
          <div class="flex space-x-3">
            <NuxtLink to="/dashboard" class="btn-outline flex items-center py-1.5 px-3 text-sm">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7m-7-7v14" />
              </svg>
              Back to Dashboard
            </NuxtLink>
            <a href="tel:+18001234567" class="btn-primary flex items-center py-1.5 px-3 text-sm">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
              </svg>
              Call Support
            </a>
          </div>
        </div>
      </div>
    </div>
    
    <div class="container-custom py-8">
      <!-- Tab Navigation -->
      <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 mb-8">
        <div class="px-6 py-4 border-b border-gray-100">
          <div class="flex justify-between items-center">
            <h2 class="font-bold text-lg text-gray-900">How Can We Help You?</h2>
          </div>
        </div>
        
        <div class="p-6">
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-6">
            <button 
              @click="activeTab = 'contact'" 
              class="flex items-center justify-center rounded-lg p-4 transition-colors" 
              :class="activeTab === 'contact' ? 'bg-primary-50 hover:bg-primary-100' : 'bg-gray-50 hover:bg-gray-100'"
            >
              <div class="h-10 w-10 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mr-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                </svg>
              </div>
              <div class="text-left">
                <span class="text-base font-medium text-gray-900">Contact Information</span>
                <p class="text-sm text-gray-600">Find our contact details and office locations</p>
              </div>
            </button>
            
            <button 
              @click="activeTab = 'form'" 
              class="flex items-center justify-center rounded-lg p-4 transition-colors" 
              :class="activeTab === 'form' ? 'bg-blue-50 hover:bg-blue-100' : 'bg-gray-50 hover:bg-gray-100'"
            >
              <div class="h-10 w-10 bg-blue-100 text-blue-600 rounded-full flex items-center justify-center mr-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                </svg>
              </div>
              <div class="text-left">
                <span class="text-base font-medium text-gray-900">Support Request</span>
                <p class="text-sm text-gray-600">Submit a support request or inquiry</p>
              </div>
            </button>
          </div>
        </div>
      </div>
      
      <!-- Tab Content -->
      <div v-if="activeTab === 'contact'" class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 mb-8">
        <div class="px-6 py-4 border-b border-gray-100">
          <div class="flex justify-between items-center">
            <h2 class="font-bold text-lg text-gray-900">Contact Information</h2>
          </div>
        </div>
        
        <div class="p-6">
          <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <div>
              <h3 class="text-lg font-semibold text-gray-900 mb-4">Our Offices</h3>
              
              <div class="space-y-6">
                <div class="bg-gray-50 rounded-lg p-4 border border-gray-100">
                  <h4 class="font-semibold text-gray-900 mb-2">Headquarters</h4>
                  <p class="text-gray-600 mb-1">123 Payment Street</p>
                  <p class="text-gray-600 mb-1">Suite 400</p>
                  <p class="text-gray-600 mb-3">San Francisco, CA 94103</p>
                  <p class="text-gray-600 mb-1">
                    <span class="font-medium">Phone:</span> (800) 123-4567
                  </p>
                  <p class="text-gray-600">
                    <span class="font-medium">Email:</span> support@paymentplan.com
                  </p>
                </div>
                
                <div class="bg-gray-50 rounded-lg p-4 border border-gray-100">
                  <h4 class="font-semibold text-gray-900 mb-2">East Coast Office</h4>
                  <p class="text-gray-600 mb-1">456 Finance Avenue</p>
                  <p class="text-gray-600 mb-1">Floor 12</p>
                  <p class="text-gray-600 mb-3">New York, NY 10001</p>
                  <p class="text-gray-600 mb-1">
                    <span class="font-medium">Phone:</span> (877) 765-4321
                  </p>
                  <p class="text-gray-600">
                    <span class="font-medium">Email:</span> nyc@paymentplan.com
                  </p>
                </div>
              </div>
            </div>
            
            <div>
              <h3 class="text-lg font-semibold text-gray-900 mb-4">Support Hours</h3>
              
              <div class="bg-gray-50 rounded-lg p-4 border border-gray-100 mb-6">
                <div class="flex justify-between mb-2">
                  <span class="font-medium text-gray-900">Monday - Friday</span>
                  <span class="text-gray-600">8:00 AM - 8:00 PM EST</span>
                </div>
                <div class="flex justify-between mb-2">
                  <span class="font-medium text-gray-900">Saturday</span>
                  <span class="text-gray-600">9:00 AM - 5:00 PM EST</span>
                </div>
                <div class="flex justify-between">
                  <span class="font-medium text-gray-900">Sunday</span>
                  <span class="text-gray-600">Closed</span>
                </div>
              </div>
              
              <h3 class="text-lg font-semibold text-gray-900 mb-4">Connect With Us</h3>
              
              <div class="flex space-x-4 mb-6">
                <a href="#" class="text-gray-500 hover:text-primary-600 transition-colors">
                  <span class="sr-only">Facebook</span>
                  <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                    <path fill-rule="evenodd" d="M22 12c0-5.523-4.477-10-10-10S2 6.477 2 12c0 4.991 3.657 9.128 8.438 9.878v-6.987h-2.54V12h2.54V9.797c0-2.506 1.492-3.89 3.777-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.988C18.343 21.128 22 16.991 22 12z" clip-rule="evenodd" />
                  </svg>
                </a>
                <a href="#" class="text-gray-500 hover:text-primary-600 transition-colors">
                  <span class="sr-only">Twitter</span>
                  <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                    <path d="M8.29 20.251c7.547 0 11.675-6.253 11.675-11.675 0-.178 0-.355-.012-.53A8.348 8.348 0 0022 5.92a8.19 8.19 0 01-2.357.646 4.118 4.118 0 001.804-2.27 8.224 8.224 0 01-2.605.996 4.107 4.107 0 00-6.993 3.743 11.65 11.65 0 01-8.457-4.287 4.106 4.106 0 001.27 5.477A4.072 4.072 0 012.8 9.713v.052a4.105 4.105 0 003.292 4.022 4.095 4.095 0 01-1.853.07 4.108 4.108 0 003.834 2.85A8.233 8.233 0 012 18.407a11.616 11.616 0 006.29 1.84" />
                  </svg>
                </a>
                <a href="#" class="text-gray-500 hover:text-primary-600 transition-colors">
                  <span class="sr-only">LinkedIn</span>
                  <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                    <path fill-rule="evenodd" d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z" clip-rule="evenodd" />
                  </svg>
                </a>
              </div>
              
              <div class="bg-primary-50 rounded-lg p-4 border border-primary-100">
                <h4 class="font-semibold text-primary-800 mb-2">24/7 Emergency Support</h4>
                <p class="text-primary-700 mb-3">
                  For urgent payment issues outside of regular business hours, please call our emergency support line.
                </p>
                <p class="text-primary-800 font-medium">
                  (888) 999-8888
                </p>
              </div>
            </div>
          </div>
          
          <!-- Map Placeholder -->
          <div class="mt-8 bg-gray-100 rounded-lg h-64 flex items-center justify-center border border-gray-200">
            <div class="text-center">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12 text-gray-400 mx-auto mb-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
              </svg>
              <p class="text-gray-600">Interactive map would be displayed here</p>
            </div>
          </div>
        </div>
      </div>
      
      <div v-else-if="activeTab === 'form'" class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 mb-8">
        <div class="px-6 py-4 border-b border-gray-100">
          <div class="flex justify-between items-center">
            <h2 class="font-bold text-lg text-gray-900">Submit a Support Request</h2>
          </div>
        </div>
        
        <div class="p-6">
          <form @submit.prevent="submitSupportRequest">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
              <div>
                <label for="name" class="block text-sm font-medium text-gray-700 mb-1">Full Name</label>
                <input 
                  type="text" 
                  id="name" 
                  v-model="supportForm.name" 
                  class="form-input w-full" 
                  placeholder="Your full name"
                  required
                />
                <p v-if="formErrors.name" class="mt-1 text-sm text-red-600">{{ formErrors.name }}</p>
              </div>
              
              <div>
                <label for="email" class="block text-sm font-medium text-gray-700 mb-1">Email Address</label>
                <input 
                  type="email" 
                  id="email" 
                  v-model="supportForm.email" 
                  class="form-input w-full" 
                  placeholder="your.email@example.com"
                  required
                />
                <p v-if="formErrors.email" class="mt-1 text-sm text-red-600">{{ formErrors.email }}</p>
              </div>
              
              <div>
                <label for="phone" class="block text-sm font-medium text-gray-700 mb-1">Phone Number</label>
                <input 
                  type="tel" 
                  id="phone" 
                  v-model="supportForm.phone" 
                  class="form-input w-full" 
                  placeholder="(123) 456-7890"
                />
                <p v-if="formErrors.phone" class="mt-1 text-sm text-red-600">{{ formErrors.phone }}</p>
              </div>
              
              <div>
                <label for="subject" class="block text-sm font-medium text-gray-700 mb-1">Subject</label>
                <select 
                  id="subject" 
                  v-model="supportForm.subject" 
                  class="form-input w-full"
                  required
                >
                  <option value="">Select a subject</option>
                  <option value="payment-issue">Payment Issue</option>
                  <option value="account-access">Account Access</option>
                  <option value="billing-question">Billing Question</option>
                  <option value="technical-support">Technical Support</option>
                  <option value="feedback">Feedback</option>
                  <option value="other">Other</option>
                </select>
                <p v-if="formErrors.subject" class="mt-1 text-sm text-red-600">{{ formErrors.subject }}</p>
              </div>
            </div>
            
            <div class="mb-6">
              <label for="message" class="block text-sm font-medium text-gray-700 mb-1">Message</label>
              <textarea 
                id="message" 
                v-model="supportForm.message" 
                rows="6" 
                class="form-input w-full" 
                placeholder="Please describe your issue or question in detail..."
                required
              ></textarea>
              <p v-if="formErrors.message" class="mt-1 text-sm text-red-600">{{ formErrors.message }}</p>
            </div>
            
            <div class="mb-6">
              <label for="attachment" class="block text-sm font-medium text-gray-700 mb-1">Attachment (Optional)</label>
              <div class="mt-1 flex justify-center px-6 pt-5 pb-6 border-2 border-gray-300 border-dashed rounded-md">
                <div class="space-y-1 text-center">
                  <svg class="mx-auto h-12 w-12 text-gray-400" stroke="currentColor" fill="none" viewBox="0 0 48 48" aria-hidden="true">
                    <path d="M28 8H12a4 4 0 00-4 4v20m32-12v8m0 0v8a4 4 0 01-4 4H12a4 4 0 01-4-4v-4m32-4l-3.172-3.172a4 4 0 00-5.656 0L28 28M8 32l9.172-9.172a4 4 0 015.656 0L28 28m0 0l4 4m4-24h8m-4-4v8m-12 4h.02" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                  </svg>
                  <div class="flex text-sm text-gray-600">
                    <label for="file-upload" class="relative cursor-pointer bg-white rounded-md font-medium text-primary-600 hover:text-primary-500 focus-within:outline-none focus-within:ring-2 focus-within:ring-offset-2 focus-within:ring-primary-500">
                      <span>Upload a file</span>
                      <input id="file-upload" name="file-upload" type="file" class="sr-only" @change="handleFileUpload" />
                    </label>
                    <p class="pl-1">or drag and drop</p>
                  </div>
                  <p class="text-xs text-gray-500">
                    PNG, JPG, GIF, PDF up to 10MB
                  </p>
                </div>
              </div>
              <p v-if="supportForm.attachment" class="mt-2 text-sm text-gray-600">
                Selected file: {{ supportForm.attachment.name }}
              </p>
            </div>
            
            <div class="mb-6">
              <div class="flex items-start">
                <div class="flex items-center h-5">
                  <input 
                    id="terms" 
                    type="checkbox" 
                    v-model="supportForm.agreeToTerms"
                    class="h-4 w-4 text-primary-600 focus:ring-primary-500 border-gray-300 rounded"
                    required
                  />
                </div>
                <div class="ml-3 text-sm">
                  <label for="terms" class="font-medium text-gray-700">I agree to the privacy policy</label>
                  <p class="text-gray-500">Your information will be used only to address your support request.</p>
                  <p v-if="formErrors.agreeToTerms" class="mt-1 text-sm text-red-600">{{ formErrors.agreeToTerms }}</p>
                </div>
              </div>
            </div>
            
            <div class="flex justify-end">
              <button 
                type="button" 
                class="btn-outline mr-3"
                @click="resetForm"
              >
                Reset Form
              </button>
              <button 
                type="submit" 
                class="btn-primary"
                :disabled="isSubmitting"
              >
                <svg v-if="isSubmitting" class="animate-spin -ml-1 mr-2 h-4 w-4 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                  <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                  <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                </svg>
                {{ isSubmitting ? 'Submitting...' : 'Submit Request' }}
              </button>
            </div>
          </form>
          
          <!-- Success Message (shown after form submission) -->
          <div v-if="formSubmitted" class="mt-6 bg-green-50 border border-green-200 rounded-lg p-4">
            <div class="flex">
              <div class="flex-shrink-0">
                <svg class="h-5 w-5 text-green-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
                </svg>
              </div>
              <div class="ml-3">
                <h3 class="text-sm font-medium text-green-800">Support request submitted successfully</h3>
                <div class="mt-2 text-sm text-green-700">
                  <p>Thank you for contacting us. Your support request has been received. We'll respond to you shortly at {{ supportForm.email }}.</p>
                </div>
                <div class="mt-4">
                  <div class="-mx-2 -my-1.5 flex">
                    <button @click="resetForm" class="bg-green-50 px-2 py-1.5 rounded-md text-sm font-medium text-green-800 hover:bg-green-100 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-green-500">
                      Submit another request
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- FAQ Section -->
      <div class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100">
        <div class="px-6 py-4 border-b border-gray-100">
          <div class="flex justify-between items-center">
            <h2 class="font-bold text-lg text-gray-900">Frequently Asked Questions</h2>
          </div>
        </div>
        
        <div class="p-6">
          <div class="space-y-4">
            <div v-for="(faq, index) in faqs" :key="index" class="border border-gray-200 rounded-lg overflow-hidden">
              <button 
                @click="toggleFaq(index)" 
                class="w-full flex justify-between items-center p-4 text-left focus:outline-none"
                :class="openFaq === index ? 'bg-gray-50' : ''"
              >
                <span class="font-medium text-gray-900">{{ faq.question }}</span>
                <svg 
                  xmlns="http://www.w3.org/2000/svg" 
                  class="h-5 w-5 text-gray-500 transition-transform" 
                  :class="openFaq === index ? 'transform rotate-180' : ''"
                  fill="none" 
                  viewBox="0 0 24 24" 
                  stroke="currentColor"
                >
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                </svg>
              </button>
              <div v-if="openFaq === index" class="p-4 bg-gray-50 border-t border-gray-200">
                <p class="text-gray-600">{{ faq.answer }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

// Tab state
const activeTab = ref('contact');

// Current date
const currentDate = computed(() => {
  const date = new Date();
  return date.toLocaleDateString('en-US', { 
    year: 'numeric', 
    month: 'long', 
    day: 'numeric' 
  });
});

// Support form state
const supportForm = ref({
  name: '',
  email: '',
  phone: '',
  subject: '',
  message: '',
  attachment: null,
  agreeToTerms: false
});

const formErrors = ref({});
const isSubmitting = ref(false);
const formSubmitted = ref(false);
const openFaq = ref(null);

// Handle file upload
const handleFileUpload = (event) => {
  const file = event.target.files[0];
  if (file) {
    supportForm.value.attachment = file;
  }
};

// Form validation
const validateForm = () => {
  const errors = {};
  
  if (!supportForm.value.name.trim()) {
    errors.name = 'Name is required';
  }
  
  if (!supportForm.value.email.trim()) {
    errors.email = 'Email is required';
  } else if (!/^\S+@\S+\.\S+$/.test(supportForm.value.email)) {
    errors.email = 'Please enter a valid email address';
  }
  
  if (supportForm.value.phone && !/^[\d\s\-\(\)]+$/.test(supportForm.value.phone)) {
    errors.phone = 'Please enter a valid phone number';
  }
  
  if (!supportForm.value.subject) {
    errors.subject = 'Please select a subject';
  }
  
  if (!supportForm.value.message.trim()) {
    errors.message = 'Message is required';
  }
  
  if (!supportForm.value.agreeToTerms) {
    errors.agreeToTerms = 'You must agree to the privacy policy';
  }
  
  formErrors.value = errors;
  return Object.keys(errors).length === 0;
};

// Submit form
const submitSupportRequest = async () => {
  if (!validateForm()) {
    return;
  }
  
  isSubmitting.value = true;
  
  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1500));
    
    // Success
    formSubmitted.value = true;
    console.log('Form submitted:', supportForm.value);
  } catch (error) {
    console.error('Error submitting form:', error);
    alert('There was an error submitting your request. Please try again.');
  } finally {
    isSubmitting.value = false;
  }
};

// Reset form
const resetForm = () => {
  supportForm.value = {
    name: '',
    email: '',
    phone: '',
    subject: '',
    message: '',
    attachment: null,
    agreeToTerms: false
  };
  formErrors.value = {};
  formSubmitted.value = false;
};

// Toggle FAQ
const toggleFaq = (index) => {
  if (openFaq.value === index) {
    openFaq.value = null;
  } else {
    openFaq.value = index;
  }
};

// FAQ data
const faqs = [
  {
    question: 'How do I make a payment?',
    answer: 'You can make a payment through your dashboard by clicking on the "Make Payment" button. We accept all major credit cards, bank transfers, and PayPal.'
  },
  {
    question: 'What happens if I miss a payment?',
    answer: 'If you miss a payment, you\'ll receive a notification. A late fee may be applied depending on your payment plan terms. Please contact support as soon as possible to resolve the issue.'
  },
  {
    question: 'How can I change my payment method?',
    answer: 'You can update your payment method in the "Payment Methods" section of your account. Navigate to the Payments tab and select "Manage Payment Methods".'
  },
  {
    question: 'Is my payment information secure?',
    answer: 'Yes, we use industry-standard encryption and security measures to protect your payment information. We are PCI DSS compliant and never store your full credit card details on our servers.'
  },
  {
    question: 'How do I request a refund?',
    answer: 'To request a refund, please contact our support team with your order number and reason for the refund. Refund eligibility depends on your specific payment plan terms and conditions.'
  }
];
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

.btn-outline {
  @apply border border-gray-300 text-gray-700 hover:text-gray-900 hover:border-gray-400 font-medium py-2 px-4 rounded-lg transition-all duration-200;
}

.form-input {
  @apply block w-full rounded-md border-gray-300 shadow-sm focus:border-primary-500 focus:ring-primary-500;
}

.fade-in {
  animation: fadeIn 0.5s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>