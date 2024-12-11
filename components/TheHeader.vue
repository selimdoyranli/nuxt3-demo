<template>
  <header class="bg-white dark:bg-gray-800 shadow-md sticky top-0 z-50">
    <nav class="container mx-auto px-4 py-4">
      <div class="flex items-center justify-between">
        <NuxtLink to="/" class="text-2xl font-bold text-emerald-600 dark:text-emerald-400">
          Recipe App
        </NuxtLink>
        
        <div class="flex items-center space-x-6">
          <NuxtLink
            v-for="category in categories"
            :key="category"
            :to="`/category/${category.toLowerCase()}`"
            class="px-3 py-2 rounded-md text-gray-600 dark:text-gray-300 hover:text-emerald-600 dark:hover:text-emerald-400 hover:bg-emerald-50 dark:hover:bg-emerald-900/20 transition-colors duration-200"
          >
            {{ category }}
          </NuxtLink>
          <ThemeSelector />
        </div>
      </div>
    </nav>
  </header>
</template>

<script setup lang="ts">
const categories = [
  'Italian',
  'Asian',
  'American',
  'Mexican',
  'Indian',
  'Mediterranean'
];
</script> 
