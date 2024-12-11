<template>
  <div class="container mx-auto px-4 py-8">
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <template v-if="pending">
        <RecipeCardSkeleton v-for="n in 6" :key="n" />
      </template>
      <template v-else-if="error">
        <div class="col-span-full text-center text-red-600">
          {{ error.message }}
        </div>
      </template>
      <template v-else>
        <NuxtLink
          v-for="recipe in data?.recipes"
          :key="recipe.id"
          :to="`/recipe/${recipe.id}`"
        >
          <RecipeCard :recipe="recipe" />
        </NuxtLink>
      </template>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { Recipe, RecipesResponse } from '~/types/recipe';
import { recipeApi } from '~/api/recipe';

const { 
  data, 
  pending, 
  error,
  execute: fetchRecipes 
} = await useAsyncData<RecipesResponse>(
  'recipes',
  () => recipeApi.fetchRecipes(),
  {
    lazy: true,
    immediate: true
  }
);

useHead({
  title: 'Recipe App - Delicious Recipes',
  meta: [
    { name: 'description', content: 'Discover delicious recipes from around the world' }
  ]
});
</script> 
