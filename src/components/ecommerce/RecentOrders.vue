<template>
  <div
    class="overflow-hidden rounded-2xl border border-gray-200 bg-white px-4 pb-3 pt-4 dark:border-gray-800 dark:bg-white/[0.03] sm:px-6"
  >
    <div class="flex flex-col gap-2 mb-4 sm:flex-row sm:items-center sm:justify-between">
      <div>
        <h3 class="text-lg font-semibold text-gray-800 dark:text-white/90">Recent Orders</h3>
      </div>

      <div class="flex items-center gap-3">
        <button
          class="inline-flex items-center gap-2 rounded-lg border border-gray-300 bg-white px-4 py-2.5 text-theme-sm font-medium text-gray-700 shadow-theme-xs hover:bg-gray-50 hover:text-gray-800 dark:border-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:hover:bg-white/[0.03] dark:hover:text-gray-200"
        >
          <ControlsIcon />

          Filter
        </button>

        <button
          class="inline-flex items-center gap-2 rounded-lg border border-gray-300 bg-white px-4 py-2.5 text-theme-sm font-medium text-gray-700 shadow-theme-xs hover:bg-gray-50 hover:text-gray-800 dark:border-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:hover:bg-white/[0.03] dark:hover:text-gray-200"
        >
          See all
        </button>
      </div>
    </div>

    <div class="max-w-full overflow-x-auto custom-scrollbar">
      <table class="min-w-full">
        <thead>
          <tr class="border-t border-gray-100 dark:border-gray-800">
            <th class="py-3 text-left">
              <p class="font-medium text-gray-500 text-theme-xs dark:text-gray-400">Products</p>
            </th>
            <th class="py-3 text-left">
              <p class="font-medium text-gray-500 text-theme-xs dark:text-gray-400">Category</p>
            </th>
            <th class="py-3 text-left">
              <p class="font-medium text-gray-500 text-theme-xs dark:text-gray-400">Price</p>
            </th>
            <th class="py-3 text-left">
              <p class="font-medium text-gray-500 text-theme-xs dark:text-gray-400">Status</p>
            </th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(product, index) in products"
            :key="index"
            class="border-t border-gray-100 dark:border-gray-800"
          >
            <td class="py-3 whitespace-nowrap">
              <div class="flex items-center gap-3">
                <div class="h-[50px] w-[50px] overflow-hidden rounded-md">
                  <img :src="product.image" :alt="product.name" />
                </div>
                <div>
                  <p class="font-medium text-gray-800 text-theme-sm dark:text-white/90">
                    {{ product.name }}
                  </p>
                  <span class="text-gray-500 text-theme-xs dark:text-gray-400"
                    >{{ product.variants }} Variants</span
                  >
                </div>
              </div>
            </td>
            <td class="py-3 whitespace-nowrap">
              <p class="text-gray-500 text-theme-sm dark:text-gray-400">{{ product.category }}</p>
            </td>
            <td class="py-3 whitespace-nowrap">
              <p class="text-gray-500 text-theme-sm dark:text-gray-400">{{ product.price }}</p>
            </td>
            <td class="py-3 whitespace-nowrap">
              <span
                :class="{
                  'rounded-full px-2 py-0.5 text-theme-xs font-medium': true,
                  'bg-success-50 text-success-600 dark:bg-success-500/15 dark:text-success-500':
                    product.status === 'Delivered',
                  'bg-warning-50 text-warning-600 dark:bg-warning-500/15 dark:text-orange-400':
                    product.status === 'Pending',
                  'bg-error-50 text-error-600 dark:bg-error-500/15 dark:text-error-500':
                    product.status === 'Canceled',
                }"
              >
                {{ product.status }}
              </span>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import ControlsIcon from '@/icons/ControlsIcon.vue';
import { ref } from 'vue'

const products = ref([
  {
    name: 'Macbook pro 13"',
    variants: 2,
    image: '/images/product/product-01.jpg',
    category: 'Laptop',
    price: '$2399.00',
    status: 'Delivered',
  },
  {
    name: 'Apple Watch Ultra',
    variants: 1,
    image: '/images/product/product-02.jpg',
    category: 'Watch',
    price: '$879.00',
    status: 'Pending',
  },
  {
    name: 'iPhone 15 Pro Max',
    variants: 2,
    image: '/images/product/product-03.jpg',
    category: 'SmartPhone',
    price: '$1869.00',
    status: 'Delivered',
  },
  {
    name: 'iPad Pro 3rd Gen',
    variants: 2,
    image: '/images/product/product-04.jpg',
    category: 'Electronics',
    price: '$1699.00',
    status: 'Canceled',
  },
  {
    name: 'Airpods Pro 2nd Gen',
    variants: 1,
    image: '/images/product/product-05.jpg',
    category: 'Accessories',
    price: '$240.00',
    status: 'Delivered',
  },
])
</script>
