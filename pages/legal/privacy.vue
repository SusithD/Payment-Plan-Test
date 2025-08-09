<template>
  <div class="fade-in bg-gray-50 min-h-screen">
    <!-- Header Section -->
    <section class="bg-gradient-to-r from-primary-600 to-primary-800 text-white">
      <div class="container-custom py-16">
        <div class="max-w-3xl mx-auto text-center">
          <div class="inline-block mb-4">
            <span class="bg-primary-800 text-primary-100 text-sm font-medium py-1 px-3 rounded-full">
              Legal Documents
            </span>
          </div>
          <h1 class="text-4xl md:text-5xl font-bold mb-4 text-white">Privacy Policy</h1>
          <p class="text-xl text-primary-100 leading-relaxed">
            Your privacy is important to us. Learn how we collect, use, and protect your information.
          </p>
          <div class="mt-6 text-sm text-primary-200">
            Last updated: August 9, 2025
          </div>
        </div>
      </div>
    </section>

    <!-- Content Section -->
    <section class="py-16">
      <div class="container-custom">
        <div class="max-w-4xl mx-auto">
          <!-- Privacy Summary -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 mb-8">
            <h2 class="text-xl font-bold text-gray-900 mb-4">Privacy at a Glance</h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
              <div class="text-center">
                <div class="h-12 w-12 bg-success-100 text-success-600 rounded-full flex items-center justify-center mx-auto mb-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
                  </svg>
                </div>
                <h3 class="font-semibold text-gray-900 mb-1">Bank-Level Security</h3>
                <p class="text-sm text-gray-600">Your data is encrypted and protected with enterprise-grade security</p>
              </div>
              <div class="text-center">
                <div class="h-12 w-12 bg-primary-100 text-primary-600 rounded-full flex items-center justify-center mx-auto mb-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                  </svg>
                </div>
                <h3 class="font-semibold text-gray-900 mb-1">Transparency</h3>
                <p class="text-sm text-gray-600">Clear information about what data we collect and why</p>
              </div>
              <div class="text-center">
                <div class="h-12 w-12 bg-accent-100 text-accent-600 rounded-full flex items-center justify-center mx-auto mb-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                  </svg>
                </div>
                <h3 class="font-semibold text-gray-900 mb-1">Your Control</h3>
                <p class="text-sm text-gray-600">Manage your privacy settings and data preferences</p>
              </div>
            </div>
          </div>

          <!-- Table of Contents -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 mb-8">
            <h2 class="text-xl font-bold text-gray-900 mb-4">Table of Contents</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
              <a href="#collection" class="text-primary-600 hover:text-primary-700 text-sm">1. Information We Collect</a>
              <a href="#usage" class="text-primary-600 hover:text-primary-700 text-sm">2. How We Use Information</a>
              <a href="#sharing" class="text-primary-600 hover:text-primary-700 text-sm">3. Information Sharing</a>
              <a href="#security" class="text-primary-600 hover:text-primary-700 text-sm">4. Data Security</a>
              <a href="#cookies" class="text-primary-600 hover:text-primary-700 text-sm">5. Cookies and Tracking</a>
              <a href="#rights" class="text-primary-600 hover:text-primary-700 text-sm">6. Your Rights</a>
              <a href="#retention" class="text-primary-600 hover:text-primary-700 text-sm">7. Data Retention</a>
              <a href="#international" class="text-primary-600 hover:text-primary-700 text-sm">8. International Transfers</a>
              <a href="#children" class="text-primary-600 hover:text-primary-700 text-sm">9. Children's Privacy</a>
              <a href="#updates" class="text-primary-600 hover:text-primary-700 text-sm">10. Policy Updates</a>
            </div>
          </div>

          <!-- Privacy Content -->
          <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-8 space-y-8">
            <section id="collection">
              <h2 class="text-2xl font-bold text-gray-900 mb-4">1. Information We Collect</h2>
              <div class="prose prose-gray max-w-none">
                <p>We collect information you provide directly to us, such as when you create an account, make payments, or contact customer support.</p>
                
                <div class="bg-gray-50 rounded-lg p-4 my-4">
                  <h4 class="font-semibold text-gray-900 mb-2">Personal Information:</h4>
                  <ul class="list-disc pl-6 space-y-1">
                    <li>Name, email address, phone number</li>
                    <li>Billing and payment information</li>
                    <li>Account credentials and security information</li>
                    <li>Communication preferences</li>
                  </ul>
                </div>

                <div class="bg-gray-50 rounded-lg p-4 my-4">
                  <h4 class="font-semibold text-gray-900 mb-2">Automatically Collected Information:</h4>
                  <ul class="list-disc pl-6 space-y-1">
                    <li>Device information (IP address, browser type, operating system)</li>
                    <li>Usage data (pages visited, time spent, clicks)</li>
                    <li>Location information (if permitted)</li>
                    <li>Cookies and similar tracking technologies</li>
                  </ul>
                </div>
              </div>
            </section>

            <section id="usage">
              <h2 class="text-2xl font-bold text-gray-900 mb-4">2. How We Use Information</h2>
              <div class="prose prose-gray max-w-none">
                <p>We use the information we collect to provide, maintain, and improve our services. Specifically, we use your information to:</p>
                <ul class="list-disc pl-6 space-y-2">
                  <li>Process payments and manage your payment plans</li>
                  <li>Provide customer support and respond to inquiries</li>
                  <li>Send important account notifications and updates</li>
                  <li>Improve our platform security and prevent fraud</li>
                  <li>Analyze usage patterns to enhance user experience</li>
                  <li>Comply with legal obligations and regulatory requirements</li>
                </ul>
              </div>
            </section>

            <section id="sharing">
              <h2 class="text-2xl font-bold text-gray-900 mb-4">3. Information Sharing</h2>
              <div class="prose prose-gray max-w-none">
                <p>We do not sell your personal information. We may share your information in limited circumstances:</p>
                
                <div class="space-y-4">
                  <div class="border-l-4 border-primary-500 pl-4">
                    <h4 class="font-semibold text-gray-900">Service Providers</h4>
                    <p class="text-sm text-gray-600">We work with trusted third-party service providers who help us operate our platform and process payments.</p>
                  </div>
                  
                  <div class="border-l-4 border-secondary-500 pl-4">
                    <h4 class="font-semibold text-gray-900">Legal Requirements</h4>
                    <p class="text-sm text-gray-600">We may disclose information when required by law or to protect our rights and the safety of our users.</p>
                  </div>
                  
                  <div class="border-l-4 border-accent-500 pl-4">
                    <h4 class="font-semibold text-gray-900">Business Transfers</h4>
                    <p class="text-sm text-gray-600">In the event of a merger, acquisition, or sale of assets, your information may be transferred as part of that transaction.</p>
                  </div>
                </div>
              </div>
            </section>

            <section id="security">
              <h2 class="text-2xl font-bold text-gray-900 mb-4">4. Data Security</h2>
              <div class="prose prose-gray max-w-none">
                <p>We implement comprehensive security measures to protect your information:</p>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 my-6">
                  <div class="bg-success-50 border border-success-200 rounded-lg p-4">
                    <div class="flex items-center mb-2">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-success-600 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
                      </svg>
                      <h4 class="font-semibold text-gray-900">Encryption</h4>
                    </div>
                    <p class="text-sm text-gray-700">All data is encrypted in transit and at rest using industry-standard protocols.</p>
                  </div>
                  
                  <div class="bg-primary-50 border border-primary-200 rounded-lg p-4">
                    <div class="flex items-center mb-2">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-primary-600 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
                      </svg>
                      <h4 class="font-semibold text-gray-900">Access Controls</h4>
                    </div>
                    <p class="text-sm text-gray-700">Strict access controls ensure only authorized personnel can access your data.</p>
                  </div>
                  
                  <div class="bg-secondary-50 border border-secondary-200 rounded-lg p-4">
                    <div class="flex items-center mb-2">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-secondary-600 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
                      </svg>
                      <h4 class="font-semibold text-gray-900">Regular Audits</h4>
                    </div>
                    <p class="text-sm text-gray-700">We conduct regular security audits and penetration testing.</p>
                  </div>
                  
                  <div class="bg-accent-50 border border-accent-200 rounded-lg p-4">
                    <div class="flex items-center mb-2">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-accent-600 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 100 4m0-4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 100 4m0-4v2m0-6V4" />
                      </svg>
                      <h4 class="font-semibold text-gray-900">Monitoring</h4>
                    </div>
                    <p class="text-sm text-gray-700">24/7 security monitoring to detect and respond to threats.</p>
                  </div>
                </div>
              </div>
            </section>

            <section id="cookies">
              <h2 class="text-2xl font-bold text-gray-900 mb-4">5. Cookies and Tracking</h2>
              <div class="prose prose-gray max-w-none">
                <p>We use cookies and similar technologies to enhance your experience on our platform. You can manage your cookie preferences through our <NuxtLink to="/legal/cookie-preferences" class="text-primary-600 hover:text-primary-700 font-medium">Cookie Preferences Center</NuxtLink>.</p>
                
                <div class="my-4">
                  <NuxtLink to="/legal/cookies" class="inline-flex items-center px-4 py-2 bg-primary-50 text-primary-700 rounded-lg hover:bg-primary-100 transition-colors">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                    </svg>
                    Learn more about our Cookie Policy
                  </NuxtLink>
                </div>
              </div>
            </section>

            <section id="rights">
              <h2 class="text-2xl font-bold text-gray-900 mb-4">6. Your Rights</h2>
              <div class="prose prose-gray max-w-none">
                <p>You have several rights regarding your personal information:</p>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 my-6">
                  <div class="bg-gray-50 rounded-lg p-4">
                    <h4 class="font-semibold text-gray-900 mb-2">Access</h4>
                    <p class="text-sm text-gray-600">Request a copy of the personal information we hold about you.</p>
                  </div>
                  <div class="bg-gray-50 rounded-lg p-4">
                    <h4 class="font-semibold text-gray-900 mb-2">Correction</h4>
                    <p class="text-sm text-gray-600">Update or correct inaccurate personal information.</p>
                  </div>
                  <div class="bg-gray-50 rounded-lg p-4">
                    <h4 class="font-semibold text-gray-900 mb-2">Deletion</h4>
                    <p class="text-sm text-gray-600">Request deletion of your personal information in certain circumstances.</p>
                  </div>
                  <div class="bg-gray-50 rounded-lg p-4">
                    <h4 class="font-semibold text-gray-900 mb-2">Portability</h4>
                    <p class="text-sm text-gray-600">Obtain your data in a machine-readable format.</p>
                  </div>
                </div>
                
                <p>To exercise these rights, please contact us at <a href="mailto:privacy@coveragex.com" class="text-primary-600 hover:text-primary-700 font-medium">privacy@coveragex.com</a>.</p>
              </div>
            </section>

            <section id="retention">
              <h2 class="text-2xl font-bold text-gray-900 mb-4">7. Data Retention</h2>
              <div class="prose prose-gray max-w-none">
                <p>We retain your personal information for as long as necessary to provide our services and comply with legal obligations. Specific retention periods include:</p>
                <ul class="list-disc pl-6 space-y-2">
                  <li>Account information: Retained while your account is active plus 7 years after closure</li>
                  <li>Payment data: Retained for 7 years for tax and regulatory compliance</li>
                  <li>Communication records: Retained for 3 years</li>
                  <li>Usage logs: Retained for 1 year</li>
                </ul>
              </div>
            </section>

            <section id="international">
              <h2 class="text-2xl font-bold text-gray-900 mb-4">8. International Transfers</h2>
              <div class="prose prose-gray max-w-none">
                <p>Your information may be transferred to and processed in countries other than your country of residence. We ensure appropriate safeguards are in place for such transfers, including:</p>
                <ul class="list-disc pl-6 space-y-2">
                  <li>Standard contractual clauses approved by regulatory authorities</li>
                  <li>Adequacy decisions by relevant data protection authorities</li>
                  <li>Other legally recognized transfer mechanisms</li>
                </ul>
              </div>
            </section>

            <section id="children">
              <h2 class="text-2xl font-bold text-gray-900 mb-4">9. Children's Privacy</h2>
              <div class="prose prose-gray max-w-none">
                <p>Our services are not intended for children under 18 years of age. We do not knowingly collect personal information from children under 18. If you are a parent or guardian and believe your child has provided us with personal information, please contact us.</p>
              </div>
            </section>

            <section id="updates">
              <h2 class="text-2xl font-bold text-gray-900 mb-4">10. Policy Updates</h2>
              <div class="prose prose-gray max-w-none">
                <p>We may update this Privacy Policy from time to time. We will notify you of any material changes by posting the new policy on this page and updating the "Last updated" date.</p>
                <p>We encourage you to review this Privacy Policy periodically to stay informed about how we protect your information.</p>
              </div>
            </section>

            <!-- Contact Information -->
            <section class="bg-gray-50 rounded-lg p-6">
              <h3 class="text-lg font-bold text-gray-900 mb-4">Contact Our Privacy Team</h3>
              <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <div>
                  <p class="text-sm text-gray-600 mb-2">For privacy-related questions:</p>
                  <p class="font-medium text-gray-900">privacy@coveragex.com</p>
                </div>
                <div>
                  <p class="text-sm text-gray-600 mb-2">Data Protection Officer:</p>
                  <p class="font-medium text-gray-900">dpo@coveragex.com</p>
                </div>
              </div>
            </section>
          </div>

          <!-- Related Links -->
          <div class="mt-8 bg-white rounded-xl shadow-sm border border-gray-100 p-6">
            <h3 class="text-lg font-bold text-gray-900 mb-4">Related Documents</h3>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
              <NuxtLink to="/legal/terms" class="flex items-center p-4 rounded-lg border border-gray-200 hover:border-primary-300 hover:bg-primary-50 transition-all">
                <div class="mr-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
                  </svg>
                </div>
                <div>
                  <h4 class="font-semibold text-gray-900">Terms of Service</h4>
                  <p class="text-sm text-gray-600">Our platform usage terms</p>
                </div>
              </NuxtLink>
              
              <NuxtLink to="/legal/cookies" class="flex items-center p-4 rounded-lg border border-gray-200 hover:border-primary-300 hover:bg-primary-50 transition-all">
                <div class="mr-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 100 4m0-4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 100 4m0-4v2m0-6V4" />
                  </svg>
                </div>
                <div>
                  <h4 class="font-semibold text-gray-900">Cookie Policy</h4>
                  <p class="text-sm text-gray-600">How we use cookies</p>
                </div>
              </NuxtLink>
              
              <NuxtLink to="/legal/cookie-preferences" class="flex items-center p-4 rounded-lg border border-gray-200 hover:border-primary-300 hover:bg-primary-50 transition-all">
                <div class="mr-3">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-primary-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                  </svg>
                </div>
                <div>
                  <h4 class="font-semibold text-gray-900">Cookie Preferences</h4>
                  <p class="text-sm text-gray-600">Manage your settings</p>
                </div>
              </NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
definePageMeta({
  title: 'Privacy Policy - CoverageX Payment Solutions',
  description: 'Learn how we collect, use, and protect your personal information on our payment platform.'
});
</script>

<style scoped>
.prose {
  @apply text-gray-700 leading-relaxed;
}

.prose p {
  @apply mb-4;
}

.prose ul {
  @apply mb-4;
}

.prose li {
  @apply mb-1;
}
</style>