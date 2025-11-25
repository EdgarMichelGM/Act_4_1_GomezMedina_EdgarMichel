<template>
  <button
    class="btn"
    :class="[variantClass, sizeClass, { 'btn--block': props.block }]"
    :disabled="props.disabled"
  >
    <slot />
  </button>
</template>

<script setup lang="ts">
import { computed } from 'vue'

type Variant = 'primary' | 'accent' | 'neutral'
type Size = 'sm' | 'md' | 'lg'

const props = defineProps<{
  variant?: Variant
  size?: Size
  block?: boolean
  disabled?: boolean
}>()

const variantClass = computed(() => {
  switch (props.variant) {
    case 'accent':
      return 'btn--accent'
    case 'neutral':
      return 'btn--neutral'
    case 'primary':
    default:
      return 'btn--primary'
  }
})

const sizeClass = computed(() => {
  switch (props.size) {
    case 'sm':
      return 'btn--sm'
    case 'lg':
      return 'btn--lg'
    case 'md':
    default:
      return 'btn--md'
  }
})
</script>

<style scoped>
.btn {
  border: none;
  border-radius: var(--radius-pill);
  font-size: var(--fs-sm);
  font-weight: var(--fw-medium);
  padding: 0.5rem 1.25rem;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  cursor: pointer;
  transition:
    background-color 0.15s ease,
    color 0.15s ease,
    box-shadow 0.15s ease,
    text-decoration-color 0.15s ease;
}

/* Tamaños */
.btn--sm {
  padding: 0.25rem 0.75rem;
  font-size: var(--fs-xs);
}

.btn--md {
  padding: 0.5rem 1.25rem;
}

.btn--lg {
  padding: 0.75rem 1.5rem;
  font-size: var(--fs-md);
}

.btn--block {
  width: 100%;
}

.btn--primary {
  background-color: var(--color-primary);
  color: var(--c-white);
}

.btn--primary:hover:not(:disabled) {
  background-color: var(--color-primary-hover);
}

.btn--accent {
  background-color: var(--color-accent);
  color: var(--c-white);
}

.btn--accent:hover:not(:disabled) {
  background-color: var(--color-accent-hover);
}

/* Neutral (negro) */
.btn--neutral {
  background-color: var(--c-gray-900);
  color: var(--c-white);
}

/* Hover */
.btn--neutral:hover:not(:disabled) {
  background-color: var(--c-gray-800);
  text-decoration: underline;
  text-decoration-thickness: 2px;
  text-underline-offset: 2px;
  text-decoration-color: var(--color-primary); /* subrayado azul */
}

/* Disabled s */
.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
</style>
