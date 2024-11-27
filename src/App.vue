<script lang="ts" setup>
import { ref } from 'vue'
import ModalBlock from './components/ModalBlock.vue'
import FolderTree from './components/FolderTree.vue'

interface Folder {
  id: number
  name: string
  children: Folder[]
}

const mockFolders: Folder[] = [
  {
    id: 1,
    name: 'Папка 1',
    children: [
      {
        id: 2,
        name: 'Папка 1.1',
        children: [],
      },
      {
        id: 3,
        name: 'Папка 1.2',
        children: [
          {
            id: 4,
            name: 'Папка 1.2.1',
            children: [],
          },
        ],
      },
    ],
  },
  {
    id: 5,
    name: 'Папка 2',
    children: [],
  },
]

const isModalOpen = ref(false)
const selectedFolderId = ref<number | undefined>(undefined)

const openModal = () => {
  isModalOpen.value = true
}

const handleConfirm = () => {
  console.log('Выбранная папка:', selectedFolderId.value)
  isModalOpen.value = false
}
</script>

<template>
  <div class="p-4">
    <button @click="openModal" class="px-4 py-2 bg-blue-500 text-white rounded">Открыть</button>
    <ModalBlock
      :isOpen="isModalOpen"
      title="Выберите папку"
      @close="isModalOpen = false"
      @confirm="handleConfirm"
    >
      <FolderTree
        :folders="mockFolders"
        @select="selectedFolderId = $event"
        :selectedFolder="selectedFolderId"
      />
    </ModalBlock>
    <p v-if="selectedFolderId" class="mt-4">Выбрана папка с ID: {{ selectedFolderId }}</p>
  </div>
</template>
