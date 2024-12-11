<template>
  <div class="bg-white dark:bg-gray-800 rounded-lg shadow-md overflow-hidden hover:shadow-lg transition-shadow duration-300">
    <img :src="recipe.image" :alt="recipe.name" class="w-full h-48 object-cover" loading="lazy" width="300" height="200" />
    <div class="p-4">
      <h3 class="text-xl font-semibold mb-2 text-gray-900 dark:text-white">{{ recipe.name }}</h3>
      <div class="flex items-center mb-2">
        <span class="text-yellow-400">★</span>
        <span class="ml-1 dark:text-gray-200">{{ recipe.rating }}</span>
        <span class="text-gray-500 dark:text-gray-400 ml-2">({{ recipe.reviewCount }} reviews)</span>
      </div>
      <div class="flex flex-wrap gap-2 mb-2">
        <span 
          v-for="tag in recipe.tags" 
          :key="tag"
          class="px-2 py-1 bg-gray-100 dark:bg-gray-700 text-sm rounded-full dark:text-gray-300"
        >
          {{ tag }}
        </span>
      </div>
      <div class="flex justify-between text-sm text-gray-600 dark:text-gray-400">
        <span>{{ recipe.prepTimeMinutes + recipe.cookTimeMinutes }} mins</span>
        <span>{{ recipe.difficulty }}</span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { Recipe } from '~/types/recipe';

defineProps<{
  recipe: Recipe;
}>();
</script> 
