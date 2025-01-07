<template>
  <div v-if="lesson">
    <p class="mt-0 font-bold text-slate-400 mb-1">
      Lesson {{ Chapter?.number }}-{{ lesson.number}}
    </p>
    <h2 class="text-2xl font-bold">{{ lesson.title }}</h2>
    <VideoPlayer v-if="lesson.videoId" :videoId="lesson.videoId" />
    <p>{{ lesson.text }}</p>
    <ClientOnly>
    <LessonCompleteButton
    :model-value="isLessonComplete"
    @update:model-value="throw createError('Could not update');" 
    ></LessonCompleteButton>
  </ClientOnly>
  </div>
  <p v-else>Loading lesson...</p>
</template>

<script setup>
import VideoPlayer from '~/components/videoPlayer.vue';

const course = useCourse();
const route = useRoute();
definePageMeta({
  validate({params}){
    const course = useCourse();
    const chapter = course.chapters.find(
      (chapter)=>chapter.slug=== params.chapterSlug
    );
    if(!chapter){
   throw createError({
    statusCode:404,
    message:'Chapter not found',
  });
}
const lesson = chapter.lessons.find(
      (lesson)=>lesson.slug=== params.lessonSlug
    );
    if(!lesson){
  throw createError({
    statusCode:404,
    message:'Lesson not found',
  });
}
return true;
  },
});

const Chapter = computed(() => {
  return course.chapters.find(
    (Chapter) => Chapter.slug === route.params.chapterSlug
  );
});


const lesson = computed(() => {
  return Chapter.value?.lessons.find(
    (lesson) => lesson.slug === route.params.lessonSlug
  );
});
 
const title = computed(()=> {
  return `${lesson.value.title}-${course.title}`;
});
 
const progress =  useLocalStorage('progress',[])
const isLessonComplete = computed(()=>{
  if(!progress.value[Chapter.value.number-1]){
    return false;
  }
  if(!progress.value[Chapter.value.number-1][lesson.value.number-1]){
    return false;
  }
  return progress.value[Chapter.value.number-1][lesson.value.number-1];
});
const toggleComplete= ()=>{
  if(!progress.value[Chapter.value.number-1]){
    progress.value[Chapter.value.number-1]=[]; 
  }
  progress.value[Chapter.value.number-1][lesson.value.number-1]=!isLessonComplete.value
};



console.log('Route params:', route.params);
console.log('Chapter:', Chapter.value);
console.log('Lesson:', lesson.value);
</script>
