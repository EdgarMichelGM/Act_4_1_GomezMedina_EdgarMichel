<script setup lang="ts">
import TarjetaMateria from '@/components/moleculas/TarjetaMateria.vue'

interface Materia {
  id: string
  nombre: string
  fecha: string
  horario: string
  grupo: string
}

// eslint-disable-next-line @typescript-eslint/no-unused-vars
const props = defineProps<{
  materias: Materia[]
}>()

const emit = defineEmits<{
  (e: 'consultar-materia', materia: Materia): void
}>()

/**
 * Maneja el evento de consulta de una materia.
 * Emite el evento al componente padre con la materia seleccionada.
 * @param materia - La materia que se desea consultar.
 */
const onConsultar = (materia: Materia) => {
  emit('consultar-materia', materia)
}
</script>

<template>
  <section class="ficha-tutorias">
    <div class="ficha-tutorias__lista">
      <TarjetaMateria
        v-for="materia in materias"
        :key="materia.id"
        :materia="materia"
        @consultar="onConsultar(materia)"
      />
    </div>
  </section>
</template>

<style scoped>
.ficha-tutorias {
  border-radius: var(--radius-lg);
  border: 1px solid var(--color-border-subtle);
  background: var(--color-surface);
  padding: 1.25rem 1.5rem;
}

/* lista con scroll vertical */
.ficha-tutorias__lista {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  min-height: 320px;
  max-height: 390px;
  overflow-y: auto;
  padding-right: 0.25rem;
}
</style>
