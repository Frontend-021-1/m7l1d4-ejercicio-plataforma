<script setup>
import { Icon } from '@iconify/vue';
import { ref, computed } from 'vue'
import Padre from './components/Padre.vue';

const mostrar = ref(true)

const textoBtn = computed(() => {
  return mostrar.value ? 'Desmontar Componente' : 'Montar Componente'
})

const iconValues = computed(() => {
  if (mostrar.value) {
    return 'ic:baseline-auto-fix-off'

  } else {
    return 'ic:baseline-auto-fix-normal'
  }
})

</script>

<template>
  <main class="container my-5">
    <button class="btn" :class="mostrar ? 'btn-outline-danger' : 'btn-outline-success'" @click="mostrar = !mostrar">
      <Icon width="24" height="24" :icon="iconValues" /> {{
        textoBtn }}
    </button>
    <Transition>
      <Padre v-if="mostrar" />
    </Transition>
  </main>
</template>

<style scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
