<script setup lang="ts">
import BaseText from '@/components/atomos/BaseText.vue'
import BaseButton from '@/components/atomos/BaseButton.vue'
import BaseIcon from '@/components/atomos/BaseIcon.vue'

interface RecursoMaterial {
  id: string
  nombre: string
  mentor: string
}

// eslint-disable-next-line @typescript-eslint/no-unused-vars
const props = defineProps<{
  nombreMateria: string
  recursos: RecursoMaterial[]
}>()

const emit = defineEmits<{
  (e: 'volver'): void
  (e: 'ver', recurso: RecursoMaterial): void
  (e: 'descargar', recurso: RecursoMaterial): void
  (e: 'eliminar', recurso: RecursoMaterial): void
  (e: 'subir'): void
}>()

/**
 * Maneja los eventos de ver, descargar, eliminar y subir recursos.
 * Emite los eventos correspondientes al componente padre con los datos necesarios.
 */
const onVer = (r: RecursoMaterial) => emit('ver', r)
const onDescargar = (r: RecursoMaterial) => emit('descargar', r)
const onEliminar = (r: RecursoMaterial) => emit('eliminar', r)
const onSubir = () => emit('subir')
</script>

<template>
  <section class="ficha-material">
    <!-- Encabezado -->
    <header class="ficha-material__header">
      <button type="button" class="ficha-material__volver" @click="emit('volver')">
        <BaseIcon nombre="flecha-izquierda" tamaño="md" />
      </button>

      <BaseText as="h2" size="md" weight="semibold">
        {{ nombreMateria }}
      </BaseText>
    </header>

    <!-- Lista de recursos -->
    <div class="ficha-material__contenido">
      <article v-for="recurso in recursos" :key="recurso.id" class="item-material">
        <div class="item-material__info">
          <BaseText size="sm" weight="semibold">
            {{ recurso.nombre }}
          </BaseText>
          <BaseText as="span" size="xs" muted>
            {{ recurso.mentor }}
          </BaseText>
        </div>

        <div class="item-material__acciones">
          <button type="button" class="item-material__eliminar" @click="onEliminar(recurso)">
            Eliminar <span class="item-material__eliminar-x">✕</span>
          </button>

          <BaseButton variant="primary" size="sm" @click="onVer(recurso)"> Ver </BaseButton>

          <BaseButton variant="primary" size="sm" @click="onDescargar(recurso)">
            Descargar
          </BaseButton>
        </div>
      </article>
    </div>

    <!-- Pie: botón subir material -->
    <footer class="ficha-material__footer">
      <BaseButton variant="primary" size="sm" @click="onSubir">
        <BaseIcon nombre="mas" tamaño="sm" />
        <span>Subir Material</span>
      </BaseButton>
    </footer>
  </section>
</template>

<style scoped>
.ficha-material {
  border-radius: var(--radius-lg);
  border: 2px solid var(--color-primary);
  background: var(--color-surface);
  box-shadow: var(--shadow-md);
  padding: 1rem 1.25rem 1.25rem;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

/* Header */
.ficha-material__header {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding-bottom: 0.5rem;
  border-bottom: 1px solid var(--color-border-subtle);
}

.ficha-material__volver {
  border: none;
  background: transparent;
  cursor: pointer;
  border-radius: 999px;
  padding: 0;
  color: var(--color-primary);
}

/* Contenido */
.ficha-material__contenido {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.item-material {
  background: var(--c-gray-200); /* gris como en tu mock */
  border-radius: var(--radius-md);
  padding: 0.6rem 0.9rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
}

.item-material__info {
  display: flex;
  flex-direction: column;
  gap: 0.1rem;
}

.item-material__acciones {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.item-material__eliminar {
  border: none;
  background: transparent;
  color: #b91c1c; /* rojo, similar al mock */
  font-size: var(--fs-xs);
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  gap: 0.25rem;
}

.item-material__eliminar-x {
  font-weight: var(--fw-bold);
}

/* Footer */
.ficha-material__footer {
  margin-top: 0.5rem;
  display: flex;
  justify-content: flex-end;
}
</style>
