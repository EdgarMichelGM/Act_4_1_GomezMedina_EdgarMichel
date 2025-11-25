<script setup lang="ts">
import BaseIcon from '@/components/atomos/BaseIcon.vue'

const props = defineProps<{
  src?: string
  alt?: string
  size?: 'sm' | 'md' | 'lg'
}>()

const sizeClass = props.size || 'md'
</script>

<template>
  <div class="avatar" :class="`avatar--${sizeClass}`">
    <img v-if="src" :src="src" :alt="alt ?? 'avatar de usuario'" />
    <span v-else class="avatar__placeholder">
      <!-- aquí usamos el icono definido en el catálogo -->
      <BaseIcon nombre="usuario" tamaño="lg" />
    </span>
  </div>
</template>

<style scoped>
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

/* Sizes */
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
</style>
