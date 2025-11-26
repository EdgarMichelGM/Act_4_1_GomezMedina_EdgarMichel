<script setup lang="ts">
import { ref } from 'vue'
import BarraAplicacion from '@/components/organismos/BarraAplicacion.vue'

type OpcionHeader = 'chat' | 'lista' | 'inicio' | 'buscar' | 'perfil'

const vistaActiva = ref<OpcionHeader>('perfil')

/* Cambia la vista activa basada en la opción seleccionada en la barra de aplicación */
const cambiarVista = (vista: OpcionHeader) => {
  vistaActiva.value = vista
}
</script>

<template>
  <div class="main-layout">
    <!-- Escuchamos el evento de la barra -->
    <BarraAplicacion @cambiar-vista="cambiarVista" />

    <main class="main-content">
      <!-- Vista activa cuando la opción es perfil -->
      <section v-if="vistaActiva === 'perfil'">
        <slot />
      </section>

      <!-- Vista no definida en mi sistema -->
      <section v-else class="contenido-vacio">
        <!--  Mensaje temporal -->
        <p class="texto-placeholder">Vista no definida...</p>
      </section>
    </main>
  </div>
</template>

<style scoped>
.main-layout {
  min-height: 100vh;
  background: var(--color-bg);
  display: flex;
  flex-direction: column;
}

.main-content {
  flex: 1;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.contenido-vacio {
  flex: 1;
}
</style>
