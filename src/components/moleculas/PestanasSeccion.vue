<script setup lang="ts">
import { ref } from 'vue'
import BaseIcon from '@/components/atomos/BaseIcon.vue'

type OpcionTab = 'material' | 'retroalimentacion' | 'avisos'

const props = defineProps<{
  activaInicial?: OpcionTab
}>()

const pestañaActiva = ref<OpcionTab>(props.activaInicial ?? 'material')

const emit = defineEmits<{
  (e: 'cambiar', valor: OpcionTab): void
}>()

const seleccionar = (valor: OpcionTab) => {
  pestañaActiva.value = valor
  emit('cambiar', valor)
}
</script>

<template>
  <nav class="pestanas">
    <!-- Material -->
    <button
      type="button"
      class="pestana"
      :class="{ 'pestana--activa': pestañaActiva === 'material' }"
      @click="seleccionar('material')"
    >
      <BaseIcon nombre="carpeta" tamaño="md" />
      <span>Material</span>
    </button>

    <!-- Retroalimentación -->
    <button
      type="button"
      class="pestana"
      :class="{ 'pestana--activa': pestañaActiva === 'retroalimentacion' }"
      @click="seleccionar('retroalimentacion')"
    >
      <BaseIcon nombre="estrella" tamaño="md" />
      <span>Retroalimentación</span>
    </button>

    <!-- AVISOS -->
    <button
      type="button"
      class="pestana"
      :class="{ 'pestana--activa': pestañaActiva === 'avisos' }"
      @click="seleccionar('avisos')"
    >
      <BaseIcon nombre="avisos" tamaño="md" />
      <span>Avisos</span>
    </button>
  </nav>
</template>

<style scoped>
.pestanas {
  display: inline-flex;
  align-items: stretch;
  border-radius: var(--radius-md);
  overflow: hidden;
  box-shadow: var(--shadow-sm);
}

.pestana {
  border: none;
  background: var(--color-surface-soft); /* gris clarito */
  color: var(--color-text);
  padding: 0.55rem 1.25rem;
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  font-size: var(--fs-sm);
  font-weight: var(--fw-medium);
  cursor: pointer;
  transition:
    background-color 0.15s ease,
    color 0.15s ease,
    transform 0.1s ease;
}

.pestana:hover:not(.pestana--activa) {
  background: var(--c-gray-200);
}

.pestana--activa {
  background: var(--color-primary);
  color: var(--c-white);
  transform: translateY(-1px);
}
.pestana:first-child {
  border-top-left-radius: var(--radius-md);
  border-bottom-left-radius: var(--radius-md);
}

.pestana:last-child {
  border-top-right-radius: var(--radius-md);
  border-bottom-right-radius: var(--radius-md);
}
</style>
