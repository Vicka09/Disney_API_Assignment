<script setup>
import { useRoute } from 'vue-router'
import { onMounted, onUnmounted } from 'vue'
import useCharacters from '@/composables/useCharacters'

const route = useRoute()
const { fetchCharacter, currentCharacter } = useCharacters()

onMounted(async () => {
  await fetchCharacter(route.params.id)
})

onUnmounted(() => {
  currentCharacter.value = null
})
</script>

<template>
  <main 
  v-if="currentCharacter"
  class="flex min-h-screen flex-col items-center justify-center gap-6 bg-gradient-to-r from-lime-200 to-emerald-900">
    <div
      v-if="currentCharacter"
      class="flex flex-col items-center justify-center gap-6"
    >
      <img :src="currentCharacter.imageUrl" :alt="currentCharacter.name" />
      <h1 class="text-white-800 text-6xl font-bold">
        Hi, I'm {{ currentCharacter.name }}
      </h1>
      <pre>{{ currentCharacter }}</pre>
    </div>
  </main>
</template>
