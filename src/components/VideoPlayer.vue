<template>
    <div class="video-wrapper">
      <video
        ref="video"
        :src="currentSrc"
        controls
        autoplay
        @ended="handleEnded"
        class="video-player"
      ></video>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue'
  
  const videoSources = [
    'https://www.w3schools.com/html/mov_bbb.mp4',
    'https://www.w3schools.com/html/movie.mp4',
    'https://www.w3schools.com/html/mov_bbb.mp4' // lại file đầu cho demo vòng lặp
  ]
  
  const currentIndex = ref(0)
  const currentSrc = computed(() => videoSources[currentIndex.value])
  
  const handleEnded = () => {
    if (currentIndex.value < videoSources.length - 1) {
      currentIndex.value++
    } else {
      currentIndex.value = 0 // lặp lại từ đầu nếu muốn
    }
  }
  </script>
  
  <style scoped>
  .video-wrapper {
    max-width: 800px;
    margin: auto;
    padding: 20px;
  }
  .video-player {
    width: 100%;
    border: 1px solid #ccc;
  }
  </style>
  