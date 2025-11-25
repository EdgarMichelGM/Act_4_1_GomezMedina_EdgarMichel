<script setup lang="ts">
import BaseAvatar from '@/components/atomos/BaseAvatar.vue'
import BaseText from '@/components/atomos/BaseText.vue'

// eslint-disable-next-line @typescript-eslint/no-unused-vars
const props = defineProps<{
  nombre: string
  rol?: string
  avatar?: string
}>()
</script>

<template>
  <div class="fila-usuario">
    <BaseAvatar :src="avatar" size="lg" />

    <div class="fila-usuario__info">
      <BaseText size="md" weight="semibold">
        {{ nombre }}
      </BaseText>

      <BaseText v-if="rol" size="sm" muted>
        {{ rol }}
      </BaseText>
    </div>
  </div>
</template>

<style scoped>
.fila-usuario {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  flex: 1;
}

.fila-usuario__info {
  display: flex;
  flex-direction: column;
  gap: 0.15rem;
}
</style>
