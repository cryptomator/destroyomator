<script setup lang="ts">
import { Dialog, DialogPanel, DialogTitle, TransitionChild, TransitionRoot } from '@headlessui/vue';
import { ref } from 'vue';

const dragging = ref(false);
const deleting = ref(false);

function chooseFile() {
  const fileInput = document.getElementById('filechooser') as HTMLInputElement;
  if (fileInput) {
    fileInput.click();
  }
}

function handleDrop(event: DragEvent) {
  const files = event.dataTransfer?.files;
  if (files && files.length > 0) {
    deleting.value = true;
  }
}
</script>

<template>
  <div class="container mx-auto">
    <!-- Header -->
    <header class="relative px-6 lg:px-8">
      <div class="mx-auto max-w-2xl py-12 lg:py-24 text-center">
          <img src="/logo.svg" alt="Destroyomator Logo" class="mx-auto size-40" />
          <h1 class="text-4xl font-semibold tracking-tight text-balance text-gray-900 sm:text-7xl">DESTROYOMATOR</h1>
          <p class="mt-8 text-lg font-medium text-pretty text-gray-500 sm:text-xl/8">Securely destroy sensitive data</p>
        </div>
    </header>

    <main class="px-4 py-8">
      <!-- File Upload Area -->
      <section class="max-w-5xl mx-auto mb-12 lg:mb-24">
        <form class="cursor-pointer p-12 flex justify-center border border-dashed rounded-xl"
        @dragenter="dragging = true" @dragleave="dragging = false" :class="[dragging ? 'border-primary-dark' : 'border-primary', dragging ? 'bg-gray-50' : 'bg-white']"
        @dragover.prevent @drop.prevent="handleDrop">
          <div class="text-center">
            <svg class="w-16 text-gray-400 mx-auto dark:text-neutral-400" width="70" height="46" viewBox="0 0 70 46" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M6.05172 9.36853L17.2131 7.5083V41.3608L12.3018 42.3947C9.01306 43.0871 5.79705 40.9434 5.17081 37.6414L1.14319 16.4049C0.515988 13.0978 2.73148 9.92191 6.05172 9.36853Z" fill="currentColor" stroke="currentColor" stroke-width="2" class="fill-white stroke-gray-400 dark:fill-neutral-800 dark:stroke-neutral-500"></path>
              <path d="M63.9483 9.36853L52.7869 7.5083V41.3608L57.6982 42.3947C60.9869 43.0871 64.203 40.9434 64.8292 37.6414L68.8568 16.4049C69.484 13.0978 67.2685 9.92191 63.9483 9.36853Z" fill="currentColor" stroke="currentColor" stroke-width="2" class="fill-white stroke-gray-400 dark:fill-neutral-800 dark:stroke-neutral-500"></path>
              <rect x="17.0656" y="1.62305" width="35.8689" height="42.7541" rx="5" fill="currentColor" stroke="currentColor" stroke-width="2" class="fill-white stroke-gray-400 dark:fill-neutral-800 dark:stroke-neutral-500"></rect>
              <path d="M47.9344 44.3772H22.0655C19.3041 44.3772 17.0656 42.1386 17.0656 39.3772L17.0656 35.9161L29.4724 22.7682L38.9825 33.7121C39.7832 34.6335 41.2154 34.629 42.0102 33.7025L47.2456 27.5996L52.9344 33.7209V39.3772C52.9344 42.1386 50.6958 44.3772 47.9344 44.3772Z" stroke="currentColor" stroke-width="2" class="stroke-gray-400 dark:stroke-neutral-500"></path>
              <circle cx="39.5902" cy="14.9672" r="4.16393" stroke="currentColor" stroke-width="2" class="stroke-gray-400 dark:stroke-neutral-500"></circle>
            </svg>

            <div class="mt-4 flex flex-wrap justify-center text-sm/6 text-gray-600">
              <span class="pe-1 font-medium text-gray-800 dark:text-neutral-200">
                Drop your file here or
              </span>
              <input type="file" id="filechooser" class="hidden" @change="deleting = true" />
              <span class="font-semibold text-primary hover:text-primary-dark rounded-lg decoration-2 focus-within:outline-hidden focus-within:ring-2 focus-within:ring-primary focus-within:ring-offset-2" @click="chooseFile()">browse</span>
            </div>
          </div>
        </form>
      </section>

      <!-- How It Works Section -->
      <section class="mb-12 lg:mb-24 max-w-5xl mx-auto">
        <h2 class="text-2xl font-semibold text-center mb-6">How It Works</h2>
        <p class="md:text-center mb-3">Destroyomator uses advanced destruction techniques to ensure that your sensitive data is irretrievable. Our process includes:</p>
        <ul class="list-disc list-inside text-left mx-auto max-w-2xl">
          <li>Data Shredding: We overwrite your data multiple times to prevent recovery.</li>
          <li>Secure Deletion: We ensure that deleted files are not recoverable by any means.</li>
          <li>Verification: We provide a verification report to confirm the destruction of your data.</li>
        </ul>
      </section>

      <!-- License Options Section -->
      <section class="max-w-5xl mx-auto">
        <h2 class="text-2xl font-semibold text-center mb-6">License Options</h2>

        <div class="isolate mx-auto mt-10 grid max-w-md grid-cols-1 gap-8 lg:mx-0 lg:max-w-none lg:grid-cols-3">
          <!-- Free Tier -->
          <div class="rounded-3xl p-6 ring-1 ring-gray-200 xl:p-8">
            <h3 id="tier-freelancer" class="text-lg/8 font-semibold text-gray-900">Free</h3>
            <p class="mt-6 flex items-baseline gap-x-1">
              <span class="text-4xl font-semibold tracking-tight text-gray-900">free</span>
            </p>
            <button aria-describedby="tier-freelancer" class="mt-6 block rounded-md bg-primary px-3 py-2 text-center text-sm/6 font-semibold text-white shadow-xs hover:bg-primary-dark focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-primary" @click="deleting = true">Get started</button>
            <ul role="list" class="list-disc list-inside mt-8 space-y-3 text-sm/6 text-gray-600 xl:mt-10">
              <li>Unlimited amount of data</li>
              <li>No support</li>
            </ul>
          </div>

          <!-- Pro Tier -->
          <div class="rounded-3xl p-6 ring-1 ring-gray-200 xl:p-8">
            <h3 id="tier-freelancer" class="text-lg/8 font-semibold text-gray-900">Pro</h3>
            <p class="mt-6 flex items-baseline gap-x-1">
              <span class="text-4xl font-semibold tracking-tight text-gray-900">$19</span>
              <span class="text-sm/6 font-semibold text-gray-600">/month</span>
            </p>
            <button aria-describedby="tier-pro" class="mt-6 block rounded-md bg-primary px-3 py-2 text-center text-sm/6 font-semibold text-white shadow-xs hover:bg-primary-dark focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-primary" @click="deleting = true">Buy plan</button>
            <ul role="list" class="list-disc list-inside mt-8 space-y-3 text-sm/6 text-gray-600 xl:mt-10">
              <li>All from Free tier</li>
              <li>Delete deleted bytes twice</li>
              <li>48-hour support response time</li>
            </ul>
          </div>

          <!-- Enterprise Tier -->
          <div class="rounded-3xl p-6 ring-1 ring-gray-200 xl:p-8">
            <h3 id="tier-freelancer" class="text-lg/8 font-semibold text-gray-900">Enterprise</h3>
            <p class="mt-6 flex items-baseline gap-x-1">
              <span class="text-4xl font-semibold tracking-tight text-gray-900">$99</span>
              <span class="text-sm/6 font-semibold text-gray-600">/month</span>
            </p>
            <button aria-describedby="tier-enterprise" class="mt-6 block rounded-md bg-primary px-3 py-2 text-center text-sm/6 font-semibold text-white shadow-xs hover:bg-primary-dark focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-primary" @click="deleting = true">Buy plan</button>
            <ul role="list" class="list-disc list-inside mt-8 space-y-3 text-sm/6 text-gray-600 xl:mt-10">
              <li>All from Pro tier</li>
              <li>Pipes deleted bytes into a black hole</li>
              <li>Get detailed usage stats</li>
              <li>24-hour support response time</li>
            </ul>
          </div>
        </div>
      </section>
    </main>

    <!-- File Deletion Dialog -->
    <TransitionRoot as="template" :show="deleting">
      <Dialog class="relative z-10" @close="deleting = false">
        <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="ease-in duration-200" leave-from="opacity-100" leave-to="opacity-0">
          <div class="fixed inset-0 bg-gray-500/75 transition-opacity" />
        </TransitionChild>

        <div class="fixed inset-0 z-10 w-screen overflow-y-auto">
          <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
            <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95" enter-to="opacity-100 translate-y-0 sm:scale-100" leave="ease-in duration-200" leave-from="opacity-100 translate-y-0 sm:scale-100" leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95">
              <DialogPanel class="relative transform overflow-hidden rounded-lg bg-white px-4 pt-5 pb-4 text-left shadow-xl transition-all sm:my-8 w-xl sm:p-6">
                <div>
                  <div class="mx-auto flex size-24 items-center justify-center rounded-full">
                    <img src="https://cryptomator.org/img/logo.svg" alt="Cryptomator Logo" class="mx-auto mb-4" />
                  </div>
                  <div class="mt-3 text-center sm:mt-5">
                    <DialogTitle as="h3" class="text-base font-semibold text-gray-900">This is a joke</DialogTitle>
                    <div class="mt-2">
                      <p class="text-sm text-gray-500 mb-2">Once sensitive data is uploaded, you can't be sure how it is processed. Better use Cryptomator to encrypt files before they leave your device!</p>
                      <p class="text-sm text-gray-500 mb-2">No worries, no actual data has been transferred.</p>
                    </div>
                  </div>
                </div>
                <div class="mt-5 sm:mt-6">
                  <a role="button" class="inline-flex w-full justify-center rounded-md bg-cryptomator px-3 py-2 text-sm font-semibold text-white shadow-xs hover:bg-cryptomator-dark focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-cryptomator" href="https://cryptomator.org?utm_source=destroyomator&utm_medium=referral&utm_campaign=aprilsfool" target="_self" rel="noopener">Check out Cryptomator</a>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>

    <!-- Footer -->
    <footer class="text-gray-500 py-4 text-center">
      <a class="px-3 py-2 font-semibold" href="https://cryptomator.org/impressum/" target="_self" rel="noopener">Impressum</a>
      <a class="px-3 py-2 font-semibold" href="https://cryptomator.org/privacy/" target="_self" rel="noopener">Privacy Policy</a>
      <p>&copy; 2025 DESTROYOMATOR. All rights reserved.</p>
    </footer>
  </div>
</template>