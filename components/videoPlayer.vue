<template>
  <iframe
  width="560"
  height="315"
    :src="`https://player.vimeo.com/video/${props.videoId}`"
    title="Video Player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media"
    allowfullscreen
  ></iframe>
</template>

<script setup>
const props = defineProps({
videoId: {
  type: String,
  required: true,
},
});
console.log('VideoPlayer props:', props.videoId);
</script>