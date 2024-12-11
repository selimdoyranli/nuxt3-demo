<template>
  <div class="container mx-auto px-4 py-8">
    <h1 class="text-3xl font-bold mb-6 text-gray-900 dark:text-gray-100">{{ category }} Recipes</h1>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <template v-if="pending">
        <RecipeCardSkeleton v-for="n in 6" :key="n" />
      </template>
      <template v-else-if="error">
        <div class="col-span-full text-center text-red-600 dark:text-red-400">
          {{ error.message }}
        </div>
      </template>
      <template v-else>
        <NuxtLink
          v-for="recipe in filteredRecipes"
          :key="recipe.id"
          :to="`/recipe/${recipe.id}`"
          class="transition-transform hover:scale-105"
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

const route = useRoute();
const category = route.params.category as string;

const { 
  data, 
  pending, 
  error,
  execute: fetchCategoryRecipes 
} = await useAsyncData<RecipesResponse>(
  `recipes-${category}`,
  () => recipeApi.fetchRecipesByCategory(category),
  {
    lazy: true,
    immediate: true
  }
);

const filteredRecipes = computed(() => {
  return data.value?.recipes ?? [];
});

useHead({
  title: `${category} Recipes - Recipe App`,
  meta: [
    { name: 'description', content: `Discover delicious ${category} recipes` }
  ]
});
</script> 
