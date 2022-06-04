<template>
  <div>
    <div class="backdrop" @click="handleBackdrop"></div>
    <div class="modal">
      <div class="modal-header">
        <h3>{{ titleModal }}</h3>
        <button class="btn-close" @click="closeModal">&times;</button>
      </div>
      <div class="modal-body">
        <slot name="body"></slot>
      </div>
      <div class="modal-footer">
        <slot name="footer"></slot>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import {} from 'vue'

// Declare Props
const props = defineProps({
  titleModal: {
    type: String,
    required: true,
  },
  isOpen: {
    type: Boolean,
    required: true,
  },
})

// Declare Emits
const emit = defineEmits(['close'])

const closeModal = () => {
  emit('close')
  document.body.style.removeProperty('overflow')
}

const handleBackdrop = () => {
  closeModal()
}

// Handle ESC
document.addEventListener('keydown', (e) => {
  if (e.key === 'Escape') {
    if (props.isOpen) {
      closeModal()
    }
  }
})
</script>

<style lang="scss" scoped>
.backdrop {
  @apply fixed inset-0 w-full h-full bg-black/50 z-10;
}

.modal {
  @apply absolute md:left-1/2 left-0 md:top-1/2 md:-translate-x-1/2 md:-translate-y-1/2 bg-white p-6 rounded-t-xl md:rounded-xl w-full md:w-[500px] z-20;
  @media screen and (max-width: 768px) {
    @apply bottom-0;
  }
  .modal-header {
    @apply flex items-center justify-between pb-3 mb-3 border-b border-slate-300;
    h3 {
      @apply font-bold text-2xl;
    }
    .btn-close {
      @apply text-3xl;
    }
  }
  .modal-body {
    @apply h-[300px] overflow-y-auto;
  }

  .modal-footer {
    @apply flex items-center justify-end pt-3 mt-3 border-t border-slate-300;
  }
}
</style>
