<script setup>
import { onMounted as montado, onUpdated, onBeforeUnmount } from 'vue'
import { Icon } from '@iconify/vue'
const props = defineProps({
  mensaje: {
    type: String,
    required: true
  },
  nombreTarea: {
    type: String,
    required: true
  },
  id: {
    type: Number,
    required: true
  },
  urgente: {
    type: Boolean,
    required: true
  }
})

const emit = defineEmits(['respuestaHijo'])

const handleClick = () => {
  emit('respuestaHijo', `NOOOOOOO! id: ${props.id}`)
}

montado(() => {
  console.log('El componente hijo ha sido montado')
})

onUpdated(() => {
  console.log('El componente hijo ha sido actualizado')
})

onBeforeUnmount(() => {
  console.log('El componente hijo ha sido desmontado')
})
</script>

<template>
  <div :class="['card', { 'border-danger': urgente }]">
    <div class="card-body">
      <h5 class="card-title">Componente hijo</h5>
      <h6 class="card-subtitle">{{ nombreTarea }}</h6>
      <p class="card-text">{{ mensaje }}</p>
      <button class="btn btn-primary" @click="handleClick">
        <Icon icon="ic:baseline-send" width="24" height="24" rotate="12" /> Enviar mensaje al padre
      </button>
    </div>
  </div>

</template>

<style scoped></style>