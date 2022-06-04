<template>
  <div class="h-screen w-full flex items-center justify-center">
    <!-- Button Open Modal -->
    <button class="btn-primary" @click="openModal">Open Modal</button>
    <!-- Modal -->
    <Modal
      v-if="showModal"
      :title-modal="titleModal"
      :is-open="showModal"
      @close="handleClose"
    >
      <template #body>
        <div>
          <p class="my-1 text-justify mr-2">
            {{ text }}
          </p>
        </div>
      </template>
      <template #footer>
        <button class="btn-success" @click="handleSubmit">Oke!</button>
      </template>
    </Modal>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import { Modal } from './components/index'

const showModal = ref<boolean>(false)
const text = ref<string>(
  'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean fringilla congue sem sed aliquam. Cras gravida sed eros velinterdum. Pellentesque hendrerit mi massa, id iaculis sapien aliquetquis. Donec id enim ac odio condimentum vestibulum. In mauris ipsum,finibus in elit a, pellentesque eleifend sem. Sed sit amet portaaugue, at sagittis turpis. Ut justo dui, bibendum sed convallis sitamet, pharetra ac velit. Donec ultrices quis ligula a pretium.Phasellus mollis lorem quam, ut convallis eros fringilla sed.Pellentesque ut nisi consectetur, tincidunt dolor eu, semper risus.Duis vitae faucibus odio. Sed feugiat, eros et egestas tincidunt,purus sapien malesuada tortor, in porttitor eros mi quis quam.'
)
const titleModal = ref<string>('Modal')

const openModal = () => {
  showModal.value = true
  document.body.style.overflow = 'hidden'
}

const handleSubmit = () => {
  showModal.value = false
  document.body.style.removeProperty('overflow')
}

const handleClose = (value: boolean) => {
  showModal.value = value
}
</script>

<style lang="scss" scoped>
.btn-primary {
  @apply px-3 py-2 rounded-lg font-bold bg-blue-600 text-white hover:bg-white hover:text-blue-600 hover:border-blue-600 hover:border-2;
}

.btn-success {
  @apply px-3 py-2 rounded-lg font-bold bg-green-600 text-white hover:bg-white hover:text-green-600 hover:border-green-600 hover:border-2;
}
</style>
