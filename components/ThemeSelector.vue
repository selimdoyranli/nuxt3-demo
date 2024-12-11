<template>
  <div class="relative">
    <select
      v-model="selectedTheme"
      class="appearance-none bg-white dark:bg-gray-800 border border-gray-300 dark:border-gray-700 rounded-md py-2 pl-3 pr-8 text-gray-700 dark:text-gray-200 cursor-pointer focus:outline-none focus:ring-2 focus:ring-emerald-500"
    >
      <option value="">Choose a theme 🎨</option>
      <option value="system">System</option>
      <option value="light">Light</option>
      <option value="dark">Dark</option>
    </select>
    <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700 dark:text-gray-200">
      <svg class="h-4 w-4 fill-current" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
        <path d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" />
      </svg>
    </div>
  </div>
</template>

<script setup lang="ts">
const colorMode = useColorMode();

const selectedTheme = ref('');

watch(selectedTheme, (newValue) => {
  if (newValue) {
    colorMode.preference = newValue;
  }
  // Her değişiklikten sonra seçimi sıfırla
  nextTick(() => {
    selectedTheme.value = '';
  });
});
</script> 
