<template>
    <div class="video-wrapper">
        <video ref="video" playsinline :src="currentSrc" @ended="handleEnded" class="video-player"  ></video>
        <div class="controls">
            <button @click="togglePlay">
                {{ isPlaying ? 'Pause' : 'Play' }}
            </button>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'
import { nextTick } from 'vue'
const video = ref(null)
const isPlaying = ref(false)

const videoSources = [
    'https://media.sstorage.xyz/test-input/IELTS/support/TN8.mp4',
    'https://media.sstorage.xyz/test-input/IELTS/support/TN1.mp4',
    'https://media.sstorage.xyz/test-input/IELTS/support/C1.mp4'

]

const currentIndex = ref(0)
const currentSrc = computed(() => videoSources[currentIndex.value])

const handleEnded = async () => {
    isPlaying.value = false
    currentIndex.value = (currentIndex.value + 1) % videoSources.length
    await nextTick()
    await video.value.load()
    await video.value.play()
}

const togglePlay = async () => {
    await video.value.play()
}

// Tự động play khi video source thay đổi (nếu đang ở trạng thái playing)
watch(currentSrc, async () => {
    if (isPlaying.value && video.value) {
        await video.value.play()
    }
})
</script>

<style scoped>
.video-wrapper {
    max-width: 800px;
    margin: auto;
    padding: 20px;
    position: relative;
}

.video-player {
    width: 100%;
    border: 1px solid #ccc;
    cursor: pointer;
}

.controls {
    margin-top: 10px;
    text-align: center;
}

button {
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
}
</style>