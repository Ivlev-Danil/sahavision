<script lang="ts" setup>
import { ref, defineProps, defineEmits } from 'vue'

interface Folder {
  id: number
  name: string
  children: Folder[]
}

defineProps({
  folders: {
    type: Array as () => Folder[],
    required: true,
  },
  selectedFolder: Number,
})

const emit = defineEmits(['select'])

const expanded = ref<number[]>([])

const toggle = (id: number) => {
  if (expanded.value.includes(id)) {
    expanded.value = expanded.value.filter((folderId) => folderId !== id)
  } else {
    expanded.value.push(id)
  }
}

const select = (id: number) => {
  emit('select', id)
}
</script>

<template>
  <ul>
    <li v-for="folder in folders" :key="folder.id">
      <div class="flex items-center gap-2">
        <button @click="toggle(folder.id)" v-if="folder.children.length">
          {{ expanded.includes(folder.id) ? '▼' : '▶' }}
        </button>
        <span
          :class="{ 'font-bold': selectedFolder === folder.id }"
          @click="select(folder.id)"
          class="cursor-pointer"
        >
          {{ folder.name }}
        </span>
      </div>
      <FolderTree
        v-if="folder.children.length && expanded.includes(folder.id)"
        :folders="folder.children"
        @select="select"
        :selectedFolder="selectedFolder"
      />
    </li>
  </ul>
</template>

<style scoped></style>
