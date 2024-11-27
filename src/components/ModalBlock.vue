<script lang="ts" setup>
import { defineProps, defineEmits } from 'vue'

defineProps({
  isOpen: Boolean,
  title: {
    type: String,
    required: true,
  },
})

const emit = defineEmits(['close', 'confirm'])

const close = () => emit('close')
const confirm = () => emit('confirm')
</script>

<template>
  <div v-if="isOpen" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center">
    <div class="bg-white w-96 p-4 rounded-md shadow-lg">
      <header class="flex justify-between items-center">
        <h2 class="text-lg font-semibold">{{ title }}</h2>
        <button @click="close" class="text-gray-500 hover:text-gray-800">✕</button>
      </header>
      <main class="mt-4">
        <slot></slot>
      </main>
      <footer class="mt-4 flex justify-end gap-2">
        <button @click="close" class="px-4 py-2 bg-gray-300 rounded">Закрыть</button>
        <button @click="confirm" class="px-4 py-2 bg-blue-500 text-white rounded">Ок</button>
      </footer>
    </div>
  </div>
</template>

<style scoped></style>
