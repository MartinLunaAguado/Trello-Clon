<script lang="ts" setup>
import { nextTick, ref, watch } from 'vue'
import { useFocusTrap } from '@vueuse/integrations/useFocusTrap'
import type { Card } from '@/types'

const props = defineProps<{
  isOpen: boolean
  card: Card | null
  mode: 'add' | 'edit'
}>()

const emit = defineEmits<{
  (e: 'close'): void
  (e: 'save', card: Card): void
}>()
const titleInput = ref<HTMLInputElement | null>(null)
const modalElement = ref<HTMLDivElement | null>(null)
const localCard = ref<Card>({
  id: 0,
  title: '',
  description: '',
})
const { activate, deactivate } = useFocusTrap(modalElement)

watch(
  () => props.card,
  (newCard) => {
    if (newCard) {
      localCard.value = { ...newCard }
    } else {
      localCard.value = { id: 0, title: '', description: '' }
    }
  },
  { immediate: true },
)

watch(
  () => props.isOpen,
  async (isOpen) => {
    if (isOpen) {
      await nextTick()
      activate()
      titleInput.value?.focus()
    } else {
      deactivate()
    }
  },
)

const handleKeydown = (event: KeyboardEvent) => {
  if (event.key === 'Enter') {
    emit('save', localCard.value)
  }
}

//ctrl + q para cerrar el Modal Dialog
</script>

<template>
  <div
    v-if="isOpen"
    @keydown.esc="emit('close')"
    @keydown="handleKeydown"
    class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center"
    role="dialog"
    aria-modal="true"
    ref="modalElement"
    @click.self="emit('close')"
  >
    <div class="bg-white p-6 rounded-lg shadow-lg max-w-md w-full">
      <h2 class="text-2xl font-bold text-emerald-800 mb-4">
        {{ mode === 'add' ? 'Add New Card' : 'Edit Card' }}
      </h2>
      <input
        v-model="localCard.title"
        type="text"
        placeholder="Card Title"
        aria-label="Card Title"
        class="w-full p-3 mb-4 border border-emerald-300 rounded focus:outline-none focus:ring-2 focus:ring-emerald-500"
        ref="titleInput"
      />

      <textarea
        v-model="localCard.description"
        class="w-full p-3 mb-4 border border-emerald-300 rounded focus:outline-none focus:ring-2 focus:ring-emerald-500"
        placeholder="Description"
        aria-label="Card Description"
      ></textarea>

      <div class="flex justify-end gap-3">
        <button
          class="bg-gray-300 hover:bg-gray-200 text-black px-4 py-2 rounded transition-colors"
          @click="emit('close')"
        >
          Cancel
        </button>

        <button
          class="bg-emerald-600 hover:bg-emerald-700 text-white px-4 py-2 rounded transition-colors"
          @click="emit('save', localCard)"
        >
          {{ mode === 'add' ? 'Add' : 'Save' }}
        </button>
      </div>
    </div>
  </div>
</template>
