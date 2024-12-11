<template>
  <div class="container mx-auto px-4 py-8">
    <template v-if="pending">
      <RecipeDetailSkeleton />
    </template>
    <template v-else-if="error">
      <div class="text-center text-red-600 dark:text-red-400">
        {{ error.message }}
      </div>
    </template>
    <template v-else>
      <div class="max-w-4xl mx-auto">
        <img :src="data?.image" :alt="data?.name" class="w-full h-96 object-cover rounded-lg mb-6" loading="lazy" width="800" height="400" />
        <h1 class="text-4xl font-bold mb-4 text-gray-900 dark:text-gray-100">{{ data?.name }}</h1>
        
        <div class="flex items-center mb-4">
          <span class="text-yellow-400 text-xl">★</span>
          <span class="ml-1 text-xl text-gray-900 dark:text-gray-100">{{ data?.rating }}</span>
          <span class="text-gray-500 dark:text-gray-400 ml-2">({{ data?.reviewCount }} reviews)</span>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
          <div>
            <h2 class="text-2xl font-semibold mb-4 text-gray-900 dark:text-gray-100">Ingredients</h2>
            <ul class="list-disc list-inside space-y-2 text-gray-800 dark:text-gray-200">
              <li v-for="ingredient in data?.ingredients" :key="ingredient">
                {{ ingredient }}
              </li>
            </ul>
          </div>

          <div>
            <h2 class="text-2xl font-semibold mb-4 text-gray-900 dark:text-gray-100">Instructions</h2>
            <ol class="list-decimal list-inside space-y-2 text-gray-800 dark:text-gray-200">
              <li v-for="instruction in data?.instructions" :key="instruction">
                {{ instruction }}
              </li>
            </ol>
          </div>
        </div>
      </div>
    </template>
  </div>
</template>

<script setup lang="ts">
import type { Recipe } from '~/types/recipe';
import { recipeApi } from '~/api/recipe';

const route = useRoute();
const { 
  data, 
  pending, 
  error,
  execute: fetchRecipe 
} = await useAsyncData<Recipe>(
  `recipe-${route.params.id}`,
  () => recipeApi.fetchRecipe(route.params.id as string),
  {
    lazy: true,
    immediate: true
  }
);

useHead({
  title: computed(() => `${data.value?.name ?? 'Loading...'} - Recipe App`),
  meta: [
    { 
      name: 'description', 
      content: computed(() => `Learn how to make ${data.value?.name ?? 'this recipe'}`)
    }
  ]
});
</script> 
