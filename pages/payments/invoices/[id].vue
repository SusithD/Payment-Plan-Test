<template>
  <div class="fade-in bg-gray-50 min-h-screen">
    <!-- Header Section -->
    <section class="bg-gradient-to-r from-primary-600 to-primary-800 text-white">
      <div class="container-custom py-12">
        <div class="max-w-4xl mx-auto">
          <!-- Navigation -->
          <div class="flex items-center mb-6">
            <NuxtLink 
              to="/payments/invoices" 
              class="text-primary-100 hover:text-white flex items-center text-sm font-medium"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
              </svg>
              Back to Invoices
            </NuxtLink>
          </div>
          
          <div class="flex flex-col lg:flex-row lg:items-center lg:justify-between">
            <div>
              <div class="inline-block mb-4">
                <span class="bg-primary-800 text-primary-100 text-sm font-medium py-1 px-3 rounded-full">
                  {{ invoice?.type || 'Payment Receipt' }}
                </span>
              </div>
              <h1 class="text-3xl md:text-4xl font-bold mb-2 text-white">
                Invoice #{{ invoice?.number || route.params.id }}
              </h1>
              <p class="text-lg text-primary-100">
                {{ invoice?.description || 'Invoice details and receipt information' }}
              </p>
            </div>
            
            <!-- Actions -->
            <div class="flex gap-3 mt-6 lg:mt-0">
              <button 
                @click="downloadPDF"
                class="btn btn-white"
                :disabled="downloading"
              >
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-4-4m4 4l4-4m-6 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
                {{ downloading ? 'Downloading...' : 'Download PDF' }}
              </button>
              
              <button 
                @click="emailInvoice"
                class="btn btn-outline-white"
                :disabled="emailing"
              >
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                </svg>
                {{ emailing ? 'Sending...' : 'Email Copy' }}
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Content Section -->
    <section class="py-16">
      <div class="container-custom">
        <div class="max-w-4xl mx-auto">
          <!-- Invoice Details Card -->
          <div class="bg-white rounded-xl shadow-lg border border-gray-100 overflow-hidden mb-8">
            <!-- Status Banner -->
            <div 
              class="px-6 py-3 text-center"
              :class="{
                'bg-success-50 border-b border-success-200': invoice?.status === 'paid',
                'bg-warning-50 border-b border-warning-200': invoice?.status === 'pending',
                'bg-error-50 border-b border-error-200': invoice?.status === 'overdue'
              }"
            >
              <span 
                class="inline-flex items-center px-3 py-1 text-sm font-semibold rounded-full"
                :class="{
                  'bg-success-100 text-success-800': invoice?.status === 'paid',
                  'bg-warning-100 text-warning-800': invoice?.status === 'pending',
                  'bg-error-100 text-error-800': invoice?.status === 'overdue'
                }"
              >
                <div 
                  class="h-2 w-2 rounded-full mr-2"
                  :class="{
                    'bg-success-400': invoice?.status === 'paid',
                    'bg-warning-400': invoice?.status === 'pending',
                    'bg-error-400': invoice?.status === 'overdue'
                  }"
                ></div>
                {{ invoice?.status?.charAt(0).toUpperCase() + invoice?.status?.slice(1) || 'Paid' }}
              </span>
            </div>

            <!-- Invoice Header -->
            <div class="px-8 py-6 border-b border-gray-100">
              <div class="flex flex-col lg:flex-row lg:justify-between lg:items-start gap-6">
                <!-- Company Info -->
                <div>
                  <img src="" alt="CoverageX" class="h-8 mb-4" />
                  <h2 class="text-2xl font-bold text-gray-900 mb-2">CoverageX Payment Solutions</h2>
                  <div class="text-sm text-gray-600 space-y-1">
                    <p>123 Business Avenue</p>
                    <p>Suite 500</p>
                    <p>New York, NY 10001</p>
                    <p>Phone: (555) 123-4567</p>
                    <p>Email: billing@coveragex.com</p>
                  </div>
                </div>
                
                <!-- Invoice Info -->
                <div class="text-right">
                  <h3 class="text-lg font-semibold text-gray-900 mb-4">Invoice Details</h3>
                  <div class="text-sm space-y-2">
                    <div class="flex justify-between min-w-0">
                      <span class="text-gray-600 mr-4">Invoice Number:</span>
                      <span class="font-medium text-gray-900">#{{ invoice?.number || route.params.id }}</span>
                    </div>
                    <div class="flex justify-between">
                      <span class="text-gray-600 mr-4">Issue Date:</span>
                      <span class="font-medium text-gray-900">{{ formatDate(invoice?.date) }}</span>
                    </div>
                    <div class="flex justify-between">
                      <span class="text-gray-600 mr-4">Due Date:</span>
                      <span class="font-medium text-gray-900">{{ formatDate(invoice?.dueDate) }}</span>
                    </div>
                    <div v-if="invoice?.status === 'paid'" class="flex justify-between">
                      <span class="text-gray-600 mr-4">Paid Date:</span>
                      <span class="font-medium text-success-600">{{ formatDate(invoice?.paidDate) }}</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Billing Information -->
            <div class="px-8 py-6 border-b border-gray-100">
              <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                <!-- Bill To -->
                <div>
                  <h3 class="text-lg font-semibold text-gray-900 mb-4">Bill To</h3>
                  <div class="text-sm text-gray-600 space-y-1">
                    <p class="font-medium text-gray-900">{{ customerInfo.name }}</p>
                    <p>{{ customerInfo.address }}</p>
                    <p>{{ customerInfo.city }}, {{ customerInfo.state }} {{ customerInfo.zip }}</p>
                    <p>{{ customerInfo.email }}</p>
                    <p>{{ customerInfo.phone }}</p>
                  </div>
                </div>
                
                <!-- Payment Method -->
                <div>
                  <h3 class="text-lg font-semibold text-gray-900 mb-4">Payment Method</h3>
                  <div class="flex items-center mb-3">
                    <div class="h-8 w-8 bg-primary-100 text-primary-600 rounded mr-3 flex items-center justify-center">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
                      </svg>
                    </div>
                    <div>
                      <div class="text-sm font-medium text-gray-900">{{ paymentMethod.type }}</div>
                      <div class="text-sm text-gray-600">**** **** **** {{ paymentMethod.last4 }}</div>
                    </div>
                  </div>
                  <div class="text-sm text-gray-600 space-y-1">
                    <p>Transaction ID: {{ paymentMethod.transactionId }}</p>
                    <p>Reference: {{ paymentMethod.reference }}</p>
                  </div>
                </div>
              </div>
            </div>

            <!-- Invoice Items -->
            <div class="px-8 py-6">
              <h3 class="text-lg font-semibold text-gray-900 mb-4">Invoice Items</h3>
              
              <!-- Items Table -->
              <div class="overflow-x-auto">
                <table class="w-full">
                  <thead class="border-b border-gray-200">
                    <tr>
                      <th class="text-left py-3 text-sm font-medium text-gray-600">Description</th>
                      <th class="text-center py-3 text-sm font-medium text-gray-600">Period</th>
                      <th class="text-center py-3 text-sm font-medium text-gray-600">Qty</th>
                      <th class="text-right py-3 text-sm font-medium text-gray-600">Rate</th>
                      <th class="text-right py-3 text-sm font-medium text-gray-600">Amount</th>
                    </tr>
                  </thead>
                  <tbody class="divide-y divide-gray-100">
                    <tr v-for="item in invoiceItems" :key="item.id" class="py-4">
                      <td class="py-4">
                        <div class="text-sm font-medium text-gray-900">{{ item.description }}</div>
                        <div class="text-sm text-gray-600">{{ item.details }}</div>
                      </td>
                      <td class="py-4 text-center text-sm text-gray-600">{{ item.period }}</td>
                      <td class="py-4 text-center text-sm text-gray-600">{{ item.quantity }}</td>
                      <td class="py-4 text-right text-sm text-gray-600">${{ item.rate }}</td>
                      <td class="py-4 text-right text-sm font-medium text-gray-900">${{ item.amount }}</td>
                    </tr>
                  </tbody>
                </table>
              </div>

              <!-- Totals -->
              <div class="mt-8 border-t border-gray-200 pt-6">
                <div class="flex justify-end">
                  <div class="w-64 space-y-3">
                    <div class="flex justify-between text-sm">
                      <span class="text-gray-600">Subtotal:</span>
                      <span class="font-medium text-gray-900">${{ totals.subtotal }}</span>
                    </div>
                    <div v-if="totals.discount > 0" class="flex justify-between text-sm">
                      <span class="text-gray-600">Discount:</span>
                      <span class="font-medium text-success-600">-${{ totals.discount }}</span>
                    </div>
                    <div v-if="totals.tax > 0" class="flex justify-between text-sm">
                      <span class="text-gray-600">Tax ({{ totals.taxRate }}%):</span>
                      <span class="font-medium text-gray-900">${{ totals.tax }}</span>
                    </div>
                    <div v-if="totals.fees > 0" class="flex justify-between text-sm">
                      <span class="text-gray-600">Processing Fee:</span>
                      <span class="font-medium text-gray-900">${{ totals.fees }}</span>
                    </div>
                    <div class="border-t border-gray-200 pt-3">
                      <div class="flex justify-between">
                        <span class="text-lg font-semibold text-gray-900">Total:</span>
                        <span class="text-lg font-bold text-primary-600">${{ totals.total }}</span>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Payment History -->
            <div v-if="paymentHistory.length > 0" class="px-8 py-6 border-t border-gray-100 bg-gray-50">
              <h3 class="text-lg font-semibold text-gray-900 mb-4">Payment History</h3>
              <div class="space-y-3">
                <div v-for="payment in paymentHistory" :key="payment.id" class="flex items-center justify-between bg-white rounded-lg p-4 border border-gray-100">
                  <div class="flex items-center">
                    <div class="h-8 w-8 bg-success-100 text-success-600 rounded-full flex items-center justify-center mr-3">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                      </svg>
                    </div>
                    <div>
                      <div class="text-sm font-medium text-gray-900">{{ payment.description }}</div>
                      <div class="text-sm text-gray-600">{{ formatDate(payment.date) }} • {{ payment.method }}</div>
                    </div>
                  </div>
                  <div class="text-sm font-medium text-gray-900">${{ payment.amount }}</div>
                </div>
              </div>
            </div>

            <!-- Footer -->
            <div class="px-8 py-6 border-t border-gray-100 bg-gray-50">
              <div class="text-sm text-gray-600 space-y-2">
                <p><strong>Payment Terms:</strong> {{ terms.payment }}</p>
                <p><strong>Notes:</strong> {{ terms.notes }}</p>
                <div class="flex items-center pt-2">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-gray-400 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
                  </svg>
                  <span class="text-xs">This invoice is secured and verified by CoverageX Payment Solutions</span>
                </div>
              </div>
            </div>
          </div>

          <!-- Related Actions -->
          <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 text-center">
              <div class="h-12 w-12 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mx-auto mb-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7v8a2 2 0 002 2h6M8 7V5a2 2 0 012-2h4.586a1 1 0 01.707.293l4.414 4.414a1 1 0 01.293.707V15a2 2 0 01-2 2v0a2 2 0 01-2-2v-4a2 2 0 00-2-2H8z" />
                </svg>
              </div>
              <h3 class="text-lg font-semibold text-gray-900 mb-2">Duplicate Invoice</h3>
              <p class="text-sm text-gray-600 mb-4">Create a copy of this invoice for your records</p>
              <button class="btn btn-outline-primary w-full">
                Create Copy
              </button>
            </div>
            
            <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 text-center">
              <div class="h-12 w-12 bg-secondary-100 text-secondary-600 rounded-full flex items-center justify-center mx-auto mb-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 17h2a2 2 0 002-2v-4a2 2 0 00-2-2H5a2 2 0 00-2 2v4a2 2 0 002 2h2m2 4h6a2 2 0 002-2v-4a2 2 0 00-2-2H9a2 2 0 00-2 2v4a2 2 0 002 2zm8-12V5a2 2 0 00-2-2H9a2 2 0 00-2 2v4h10z" />
                </svg>
              </div>
              <h3 class="text-lg font-semibold text-gray-900 mb-2">Print Invoice</h3>
              <p class="text-sm text-gray-600 mb-4">Print a physical copy of this invoice</p>
              <button @click="printInvoice" class="btn btn-outline-secondary w-full">
                Print
              </button>
            </div>
            
            <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 text-center">
              <div class="h-12 w-12 bg-accent-100 text-accent-600 rounded-full flex items-center justify-center mx-auto mb-4">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18.364 5.636l-3.536 3.536m0 5.656l3.536 3.536M9.172 9.172L5.636 5.636m3.536 9.192L5.636 18.364M12 2.18l.09-.012a10 10 0 017.274 7.274.657.657 0 01-.372.59L12 12l-.09-.012a10 10 0 01-7.274-7.274.657.657 0 01.372-.59L12 2.18z" />
                </svg>
              </div>
              <h3 class="text-lg font-semibold text-gray-900 mb-2">Get Support</h3>
              <p class="text-sm text-gray-600 mb-4">Have questions about this invoice?</p>
              <NuxtLink to="/support" class="btn btn-outline-accent w-full">
                Contact Support
              </NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

const route = useRoute();

definePageMeta({
  title: 'Invoice Details - CoverageX Payment Solutions',
  description: 'View detailed invoice information and payment receipt.'
});

// Reactive state
const downloading = ref(false);
const emailing = ref(false);

// Sample data - in a real app this would come from an API
const invoice = ref({
  id: route.params.id,
  number: '2025-0001',
  type: 'Payment Receipt',
  date: '2025-08-01',
  dueDate: '2025-08-15',
  paidDate: '2025-08-01',
  description: 'Monthly Payment - August 2025',
  status: 'paid'
});

const customerInfo = ref({
  name: 'John Smith',
  address: '456 Customer Street',
  city: 'Los Angeles',
  state: 'CA',
  zip: '90210',
  email: 'john.smith@email.com',
  phone: '(555) 987-6543'
});

const paymentMethod = ref({
  type: 'Visa Credit Card',
  last4: '4242',
  transactionId: 'TXN_2025080100123',
  reference: 'REF_AUG2025_001'
});

const invoiceItems = ref([
  {
    id: 1,
    description: 'Monthly Insurance Payment',
    details: 'Premium payment for policy coverage',
    period: 'Aug 2025',
    quantity: 1,
    rate: '250.00',
    amount: '250.00'
  }
]);

const totals = ref({
  subtotal: '250.00',
  discount: '0.00',
  tax: '0.00',
  taxRate: '0',
  fees: '0.00',
  total: '250.00'
});

const paymentHistory = ref([
  {
    id: 1,
    description: 'Payment Received',
    date: '2025-08-01',
    method: 'Visa *4242',
    amount: '250.00'
  }
]);

const terms = ref({
  payment: 'Payment is due within 15 days of invoice date.',
  notes: 'Thank you for your business! If you have any questions about this invoice, please contact our support team.'
});

// Methods
function formatDate(dateString) {
  if (!dateString) return 'N/A';
  const date = new Date(dateString);
  return date.toLocaleDateString('en-US', {
    year: 'numeric',
    month: 'long',
    day: 'numeric'
  });
}

async function downloadPDF() {
  downloading.value = true;
  
  try {
    // Simulate PDF generation and download
    await new Promise(resolve => setTimeout(resolve, 2000));
    
    // In a real app, this would trigger a PDF download
    console.log(`Downloading PDF for invoice ${invoice.value.number}`);
    
  } catch (error) {
    console.error('Error downloading PDF:', error);
  } finally {
    downloading.value = false;
  }
}

async function emailInvoice() {
  emailing.value = true;
  
  try {
    // Simulate email sending
    await new Promise(resolve => setTimeout(resolve, 1500));
    
    console.log(`Emailing invoice ${invoice.value.number}`);
    
  } catch (error) {
    console.error('Error emailing invoice:', error);
  } finally {
    emailing.value = false;
  }
}

function printInvoice() {
  // Trigger browser print dialog
  window.print();
}

onMounted(() => {
  // In a real app, fetch invoice data based on route.params.id
  console.log('Loading invoice:', route.params.id);
});
</script>

<style scoped>
.btn {
  @apply inline-flex items-center justify-center px-4 py-2 border border-transparent text-sm font-medium rounded-lg shadow-sm transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-offset-2;
}

.btn-white {
  @apply text-primary-600 bg-white border-white hover:bg-gray-50 focus:ring-primary-500;
}

.btn-outline-white {
  @apply text-white bg-transparent border-white hover:bg-white hover:text-primary-600 focus:ring-white;
}

.btn-primary {
  @apply text-white bg-primary-600 hover:bg-primary-700 focus:ring-primary-500;
}

.btn-outline-primary {
  @apply text-primary-600 bg-white border-primary-600 hover:bg-primary-50 focus:ring-primary-500;
}

.btn-outline-secondary {
  @apply text-secondary-600 bg-white border-secondary-600 hover:bg-secondary-50 focus:ring-secondary-500;
}

.btn-outline-accent {
  @apply text-accent-600 bg-white border-accent-600 hover:bg-accent-50 focus:ring-accent-500;
}

/* Print styles */
@media print {
  .no-print {
    display: none !important;
  }
  
  .print-only {
    display: block !important;
  }
  
  body {
    background: white !important;
  }
  
  .shadow-lg,
  .shadow-sm {
    box-shadow: none !important;
  }
}
</style>