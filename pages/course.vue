<template>
  <div class="p-12 bg-gray-100 w-full h-full min-h-screen flex flex-col items-center">
    <div class="prose mb-8 text-center">
      <h1 class="text-3xl font-bold">
        Course: <span class="text-indigo-600">Mastering Nuxt 3</span>
      </h1>
    </div>
    <div class="flex flex-col md:flex-row justify-center gap-8 flex-grow w-full max-w-screen-lg"> 
      <div class="prose bg-white shadow-md rounded-lg p-6 w-full md:w-1/3">
        <h2 class="text-lg font-semibold mb-4">Chapters</h2>
        <ul class="space-y-2">
          <li 
            v-for="chapter in chapters" 
            :key="chapter.slug" 
            class="border-b border-gray-200 pb-2">
            <h4 class="text-base font-medium">{{ chapter.title }}</h4>
            <NuxtLink
              v-for="(lesson, index) in chapter.lessons"
              :key="lesson.slug"
              :to="`/course/chapter/${chapter.slug}/lesson/${lesson.slug}`"
              class="flex flex-row space-x-1 no-underline prose-sm font-normal py-1"
            >
              <span class="text-gray-500">{{ index + 1 }}.</span>
              <span>{{ lesson.title }}</span>
            </NuxtLink>
          </li>
        </ul>
      </div> 
      <div class="bg-white shadow-md rounded-lg p-8 w-full md:w-2/3">
        <NuxtErrorBoundary>
        <NuxtPage /> 
        <template #error="{error}">
          <p>
            oh no something Broke!
            <code>{{ error }}</code>
          </p>
          <p>
            <button class="hover:cursor-pointer bg-gray-500 text-white font-bold" @click="resetError(error)">
              Reset
            </button>
          </p>
        </template>
      </NuxtErrorBoundary>
      </div>
    </div>
  </div>
</template>

<script setup>
const { chapters } = useCourse();

const resetError= async (error)=>{
  await navigateTo('/course/chapter/1-chapter-1/lesson/1-introduction-to-typescript-with-vue-js-3');
  error.value =null;
};
</script>
