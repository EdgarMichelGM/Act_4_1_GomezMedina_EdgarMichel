<script setup lang="ts">
import BaseText from '@/components/atomos/BaseText.vue'
import BaseButton from '@/components/atomos/BaseButton.vue'
import BaseIcon from '@/components/atomos/BaseIcon.vue'

interface Materia {
  id: string
  nombre: string
  fecha: string
  horario: string
  grupo: string
}

// eslint-disable-next-line @typescript-eslint/no-unused-vars
const props = defineProps<{
  materia: Materia
}>()

const emit = defineEmits<{
  (e: 'consultar'): void
}>()

/**
 * Maneja el evento de clic en el botón "Consultar".
 * Emite un evento al componente padre para manejar la acción.
 */
const onConsultar = () => {
  emit('consultar')
}
</script>

<template>
  <article class="tarjeta-materia">
    <div class="tarjeta-materia__info">
      <!-- Nombre de la materia -->
      <BaseText size="sm" weight="semibold">
        {{ materia.nombre }}
      </BaseText>

      <!-- fila de metadatos: fecha / horario -->
      <div class="tarjeta-materia__meta">
        <div class="tarjeta-materia__col">
          <BaseText as="span" size="xs" muted> Fecha </BaseText>
          <BaseText as="span" size="sm">
            {{ materia.fecha }}
          </BaseText>

          <div class="tarjeta-materia__grupo">
            <BaseIcon nombre="grupo" tamaño="sm" />
            <BaseText as="span" size="xs">
              {{ materia.grupo }}
            </BaseText>
          </div>
        </div>

        <div class="tarjeta-materia__col tarjeta-materia__col--horario">
          <BaseText as="span" size="xs" muted> Horario </BaseText>
          <BaseText as="span" size="sm">
            {{ materia.horario }}
          </BaseText>
        </div>
      </div>
    </div>

    <!-- Botón de acción -->
    <div class="tarjeta-materia__accion">
      <BaseButton variant="primary" size="sm" @click="onConsultar"> Consultar </BaseButton>
    </div>
  </article>
</template>

<style scoped>
.tarjeta-materia {
  background: var(--c-gray-200);
  border-radius: var(--radius-md);
  padding: 0.75rem 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
}

.tarjeta-materia__info {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
  flex: 1;
}

.tarjeta-materia__meta {
  display: flex;
  justify-content: space-between;
  gap: 1.5rem;
}

.tarjeta-materia__col {
  display: flex;
  flex-direction: column;
  gap: 0.15rem;
}

.tarjeta-materia__col--horario {
  min-width: 120px;
}

.tarjeta-materia__grupo {
  margin-top: 0.15rem;
  display: inline-flex;
  align-items: center;
  gap: 0.25rem;
  font-size: var(--fs-xs);
}

.tarjeta-materia__accion {
  flex-shrink: 0;
}
</style>
