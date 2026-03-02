<script setup>
import { ref, onMounted, onUpdated, onBeforeUnmount } from 'vue'
import { Icon } from '@iconify/vue';
import Hijo from './Hijo.vue';

const mensajeHijo = ref('')
const tareas = ref([
  { id: 1, texto: 'Aprender sobre las Props', urgente: true },
  { id: 2, texto: 'Dominar los Emits (Events)', urgente: false }
])

const handleRespuesta = (msg) => {
  mensajeHijo.value = msg
}

// Hooks ciclo de vida
onMounted(() => {
  console.log('Componente Padre ha sido montado')
})

onUpdated(() => {
  console.log('Componente Padre ha sido actualizado')
})

onBeforeUnmount(() => {
  console.log('Componente Padre ha sido desmontado')
})
</script>

<template>
  <div class="bg-info-subtle border rounded-3 p-4 my-5">
    <h1>Componente padre</h1>
    <Transition>
      <h2 class="display-4" v-if="mensajeHijo">Mensaje: {{ mensajeHijo }}</h2>
    </Transition>
    <button class="btn btn-warning btn-sm mb-3" @click="mensajeHijo = ''" aria-label="Limpiar mensaje">
      <Icon icon="ic:outline-cleaning-services" width="24" height="24" />
    </button>
    <div class="row row-cols-1 row-cols-md-2 g-3">
      <div class="col" v-for="tarea in tareas" :key="tarea.id">
        <Hijo mensaje="Msj desde el padre: Soy tu padre" @respuesta-hijo="handleRespuesta" :nombreTarea="tarea.texto"
          :urgente="tarea.urgente" :id="tarea.id" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.v-enter-active {
  transition: all 0.3s ease-out;
}

.v-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}

.v-enter-from,
.v-leave-to {
  transform: translateX(-50px);
  opacity: 0;
}
</style>