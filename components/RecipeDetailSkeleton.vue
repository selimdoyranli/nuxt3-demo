<template>
  <div class="max-w-4xl mx-auto">
    <div class="w-full h-96 bg-gray-200 dark:bg-gray-700 rounded-lg mb-6 animate-pulse"></div>
    <div class="h-10 bg-gray-200 dark:bg-gray-700 rounded w-3/4 mb-4 animate-pulse"></div>
    
    <div class="flex items-center mb-4">
      <div class="w-32 h-6 bg-gray-200 dark:bg-gray-700 rounded animate-pulse"></div>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
      <div>
        <div class="h-8 bg-gray-200 dark:bg-gray-700 rounded w-1/3 mb-4 animate-pulse"></div>
        <div class="space-y-2">
          <div v-for="n in 6" :key="n" class="h-4 bg-gray-200 dark:bg-gray-700 rounded w-full animate-pulse"></div>
        </div>
      </div>

      <div>
        <div class="h-8 bg-gray-200 dark:bg-gray-700 rounded w-1/3 mb-4 animate-pulse"></div>
        <div class="space-y-2">
          <div v-for="n in 8" :key="n" class="h-4 bg-gray-200 dark:bg-gray-700 rounded w-full animate-pulse"></div>
        </div>
      </div>
    </div>
  </div>
</template>
