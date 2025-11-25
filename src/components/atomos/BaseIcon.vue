<script setup lang="ts">
import { computed } from 'vue'

type NombreIcono =
  | 'grupo'
  | 'usuario'
  | 'editar'
  | 'buscar'
  | 'chat'
  | 'lista'
  | 'inicio'
  | 'perfil'
  | 'carpeta'
  | 'estrella'
  | 'avisos'

const props = defineProps<{
  nombre: NombreIcono
  tamaño?: 'sm' | 'md' | 'lg'
}>()

const claseTamaño = computed(() => {
  switch (props.tamaño) {
    case 'sm':
      return 'icono--sm'
    case 'lg':
      return 'icono--lg'
    case 'md':
    default:
      return 'icono--md'
  }
})
</script>

<template>
  <span class="icono" :class="claseTamaño">
    <!-- Usuario (para avatar) -->
    <svg v-if="nombre === 'usuario'" viewBox="0 0 24 24" aria-hidden="true">
      <circle cx="12" cy="8" r="4" fill="currentColor" />
      <path d="M5 19c0-2.5 3-4.5 7-4.5s7 2 7 4.5v1H5v-1z" fill="currentColor" />
    </svg>

    <!-- Editar -->
    <svg v-else-if="nombre === 'editar'" viewBox="0 0 24 24" aria-hidden="true">
      <rect
        x="3.5"
        y="3.5"
        width="17"
        height="17"
        rx="3"
        ry="3"
        fill="none"
        stroke="currentColor"
        stroke-width="1.8"
      />
      <path
        d="M10 15.5l4.2-4.2 1.7 1.7L11.7 17H10v-1.5z
           M15 9.3l1.1-1.1a1 1 0 0 1 1.4 0l0.9 0.9a1 1 0 0 1 0 1.4L17.3 11"
        fill="currentColor"
      />
    </svg>

    <!-- Buscar (lupa) -->
    <svg v-else-if="nombre === 'buscar'" viewBox="0 0 24 24" aria-hidden="true">
      <circle cx="11" cy="11" r="5.5" fill="none" stroke="currentColor" stroke-width="2" />
      <line
        x1="15"
        y1="15"
        x2="19"
        y2="19"
        stroke="currentColor"
        stroke-width="2"
        stroke-linecap="round"
      />
    </svg>

    <!-- Chat -->
    <svg v-else-if="nombre === 'chat'" viewBox="0 0 24 24" aria-hidden="true">
      <path
        d="M4 5h16v9a2 2 0 0 1-2 2h-6l-3.5 3-0.5-3H6a2 2 0 0 1-2-2V5z"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linejoin="round"
      />
    </svg>

    <!-- Lista -->
    <svg v-else-if="nombre === 'lista'" viewBox="0 0 24 24" aria-hidden="true">
      <line x1="5" y1="7" x2="19" y2="7" stroke="currentColor" stroke-width="2" />
      <line x1="5" y1="12" x2="19" y2="12" stroke="currentColor" stroke-width="2" />
      <line x1="5" y1="17" x2="19" y2="17" stroke="currentColor" stroke-width="2" />
    </svg>

    <!-- Inicio (casita) -->
    <svg v-else-if="nombre === 'inicio'" viewBox="0 0 24 24" aria-hidden="true">
      <path
        d="M4 11l8-7 8 7v8a1 1 0 0 1-1 1h-4v-5h-6v5H5a1 1 0 0 1-1-1z"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linejoin="round"
      />
    </svg>

    <!-- Perfil (círculo con usuario, para AppBar) -->
    <svg v-else-if="nombre === 'perfil'" viewBox="0 0 24 24" aria-hidden="true">
      <circle cx="12" cy="12" r="10" fill="currentColor" opacity="0.2" />
      <circle cx="12" cy="9" r="3" fill="currentColor" />
      <path
        d="M7 17c0-2.2 2.2-4 5-4s5 1.8 5 4"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linecap="round"
      />
    </svg>

    <!-- Carpeta (para "Material") -->
    <svg v-else-if="nombre === 'carpeta'" viewBox="0 0 24 24" aria-hidden="true">
      <path
        d="M3 6a2 2 0 0 1 2-2h4l2 2h8a2 2 0 0 1 2 2v8a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V6z"
        fill="currentColor"
      />
    </svg>

    <!-- Estrella (para "Retroalimentación") -->
    <svg v-else-if="nombre === 'estrella'" viewBox="0 0 24 24" aria-hidden="true">
      <path
        d="M12 3l2.5 5.1 5.6.8-4.1 4 1 5.6L12 16.8 7 18.5l1-5.6-4.1-4 5.6-.8L12 3z"
        fill="currentColor"
      />
    </svg>

    <!-- Avisos (burbuja, similar a chat) -->
    <svg v-else-if="nombre === 'avisos'" viewBox="0 0 24 24" aria-hidden="true">
      <path
        d="M4 5h16v9a2 2 0 0 1-2 2h-6l-3.5 3-0.5-3H6a2 2 0 0 1-2-2V5z"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linejoin="round"
      />
    </svg>

    <!-- Grupo -->
    <svg v-else-if="nombre === 'grupo'" viewBox="0 0 24 24" aria-hidden="true">
      <!-- persona 1 -->
      <circle cx="9" cy="9" r="2.5" fill="currentColor" />
      <path
        d="M5.5 15c0-1.7 1.8-3 3.5-3s3.5 1.3 3.5 3"
        fill="none"
        stroke="currentColor"
        stroke-width="1.8"
        stroke-linecap="round"
      />

      <!-- persona 2  -->
      <circle cx="15" cy="9.5" r="2.3" fill="currentColor" opacity="0.7" />
      <path
        d="M12.5 15.3c0-1.5 1.5-2.7 3-2.7s3 1.2 3 2.7"
        fill="none"
        stroke="currentColor"
        stroke-width="1.6"
        stroke-linecap="round"
        opacity="0.7"
      />
    </svg>
  </span>
</template>

<style scoped>
.icono {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  color: inherit;
}

.icono--sm {
  width: 14px;
  height: 14px;
}
.icono--md {
  width: 24px;
  height: 24px;
}
.icono--lg {
  width: 32px;
  height: 32px;
}

svg {
  width: 100%;
  height: 100%;
}
</style>
