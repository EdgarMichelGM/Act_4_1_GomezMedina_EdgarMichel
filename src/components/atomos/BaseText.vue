<script setup lang="ts">
const props = defineProps<{
  as?: 'p' | 'span' | 'h1' | 'h2' | 'h3'
  size?: 'xs' | 'sm' | 'md' | 'lg'
  weight?: 'regular' | 'medium' | 'semibold' | 'bold'
  muted?: boolean
}>()

const tag = props.as || 'p'
</script>

<template>
  <component
    :is="tag"
    class="text"
    :class="[
      `text--${props.size || 'md'}`,
      `text--${props.weight || 'regular'}`,
      { 'text--muted': props.muted },
    ]"
  >
    <slot />
  </component>
</template>

<style scoped>
.text {
  margin: 0;
}

.text--xs {
  font-size: var(--fs-xs);
}
.text--sm {
  font-size: var(--fs-sm);
}
.text--md {
  font-size: var(--fs-md);
}
.text--lg {
  font-size: var(--fs-lg);
}

.text--regular {
  font-weight: var(--fw-regular);
}
.text--medium {
  font-weight: var(--fw-medium);
}
.text--semibold {
  font-weight: var(--fw-semibold);
}
.text--bold {
  font-weight: var(--fw-bold);
}

.text--muted {
  color: var(--color-text-muted);
}
</style>
