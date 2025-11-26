<script setup lang="ts">
import BaseIcon from '@/components/atomos/BaseIcon.vue'
/*
 * BarraBusqueda Component: Componente de barra de búsqueda reutilizable.
 * Permite a los usuarios ingresar términos de búsqueda y emitir eventos para manejar la búsqueda.
 */
const props = defineProps<{
  modelValue?: string
  placeholder?: string
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', value: string): void
  (e: 'buscar', value: string): void
}>()

/**
 * Maneja el evento de entrada en el campo de búsqueda.
 * Emite el valor actualizado al componente padre.
 */
const onInput = (event: Event) => {
  const target = event.target as HTMLInputElement
  emit('update:modelValue', target.value)
}

/**
 * Maneja el evento de tecla presionada.
 * Si se presiona "Enter", emite el evento de búsqueda con el valor actual.
 */
const onEnter = (event: KeyboardEvent) => {
  if (event.key === 'Enter') {
    emit('buscar', props.modelValue ?? '')
  }
}
</script>

<template>
  <div class="buscador">
    <span class="buscador__icono">
      <BaseIcon nombre="buscar" tamaño="md" />
    </span>
    <input
      class="buscador__input"
      type="text"
      :value="modelValue"
      :placeholder="placeholder ?? 'Buscar'"
      @input="onInput"
      @keyup="onEnter"
    />
  </div>
</template>

<style scoped>
.buscador {
  background-color: var(--c-white);
  color: var(--color-text);
  border-radius: var(--radius-md);
  padding: 0.75rem 1.4rem;
  min-width: 800px;
  max-width: 900px;
  height: 52px;
  display: flex;
  align-items: center;
  box-shadow: var(--shadow-sm);
}

.buscador__icono {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  margin-right: 0.4rem;
  color: var(--color-text-muted);
}

.buscador__input {
  border: none;
  outline: none;
  font-size: var(--fs-md);
  flex: 1;
  background: transparent;
}
</style>
