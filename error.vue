<template>
    <NuxtLayout>
        <div claas="flex flex-col">
        <div v-if= "error.statusCode=='404'" class=  "prose">
            <h1>404</h1>
            <p>I guss that page doesn't exist</p> 
            </div>
        <div v-else class="prose">
            <h1>Dang</h1>
            <p>It looks like something broke</p>
            <p>Sorry about that</p>
            
            </div>
            <div class="prose mt-5">
                <p><strong>{{ error.message }}</strong></p>
                <p>
                    Go to the
                
                <a class="hover:cursor-pointer" @click="handleErrors">First Lesson</a>
            </p>
            </div>
        </div>
    </NuxtLayout>
</template>
<script setup>
import { handleError } from 'vue';

const error = useError();
const handleErrors = ()=> {
    clearError({
    redirect:
    '/course/chapter/1-chapter-1/lesson/1-introduction-to-typescript-with-vue-js-3'
    });
};
</script>