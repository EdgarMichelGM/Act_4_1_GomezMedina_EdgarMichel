<script setup lang="ts">
import FilaIdentidadUsuario from '@/components/moleculas/FilaIdentidadUsuario.vue'
import BaseButton from '@/components/atomos/BaseButton.vue'
import BaseText from '@/components/atomos/BaseText.vue'
import BaseIcon from '@/components/atomos/BaseIcon.vue'

// eslint-disable-next-line @typescript-eslint/no-unused-vars
const props = defineProps<{
  nombreUsuario: string
  rolUsuario?: string
  avatar?: string
}>()

/**
 * Emite eventos para editar el perfil y cerrar sesión.
 */
const emit = defineEmits(['editar', 'cerrar'])
</script>

<template>
  <section class="tarjeta-perfil">
    <BaseText as="p" size="sm" weight="semibold"> User-Name </BaseText>

    <div class="tarjeta-perfil__contenido">
      <FilaIdentidadUsuario :nombre="nombreUsuario" :rol="rolUsuario" :avatar="avatar" />

      <div class="tarjeta-perfil__acciones">
        <BaseButton variant="primary" size="sm" @click="emit('editar')">
          <BaseIcon nombre="editar" tamaño="sm" />
          <span>Editar</span>
        </BaseButton>

        <BaseButton variant="neutral" size="sm" @click="emit('cerrar')">
          <span>Cerrar sesión</span>
        </BaseButton>
      </div>
    </div>
  </section>
</template>

<style scoped>
.tarjeta-perfil {
  padding: 1.25rem;
  border-radius: var(--radius-lg);
  border: 1px solid var(--color-border-subtle);
  background: var(--color-surface);
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.tarjeta-perfil__contenido {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.tarjeta-perfil__acciones {
  display: flex;
  gap: 0.5rem;
}

.avatar {
  border-radius: var(--radius-pill);
  background: var(--c-gray-300);
  display: inline-flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.avatar img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.avatar__placeholder {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  color: var(--color-text-muted);
}

/* Tamaños del círculo */
.avatar--sm {
  width: 32px;
  height: 32px;
}
.avatar--md {
  width: 48px;
  height: 48px;
}
.avatar--lg {
  width: 72px;
  height: 72px;
}
.avatar__placeholder :deep(svg) {
  width: 80%;
  height: 80%;
}

@media (max-width: 768px) {
  .tarjeta-perfil {
    padding: 1.25rem;
  }

  .tarjeta-perfil__contenido {
    flex-direction: column;
    align-items: center;
    text-align: center;
    gap: 1rem;
  }

  .tarjeta-perfil__avatar {
    margin-right: 0;
  }

  .tarjeta-perfil__info {
    align-items: center;
  }

  .tarjeta-perfil__acciones {
    width: 100%;
    justify-content: center;
    gap: 0.75rem;
    flex-wrap: wrap;
  }

  .tarjeta-perfil__acciones button {
    width: 100%;
  }
}
</style>
