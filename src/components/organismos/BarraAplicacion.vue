<script setup lang="ts">
import { ref } from 'vue'
import BaseIcon from '@/components/atomos/BaseIcon.vue'
import BarraBusqueda from '@/components/moleculas/BarraBusqueda.vue'

type OpcionHeader = 'chat' | 'lista' | 'inicio' | 'buscar' | 'perfil'

const opcionActiva = ref<OpcionHeader>('perfil')

const emit = defineEmits<{
  (e: 'cambiar-vista', vista: OpcionHeader): void
}>()

const seleccionarOpcion = (opcion: OpcionHeader) => {
  opcionActiva.value = opcion
  emit('cambiar-vista', opcion)
}

const terminoBusqueda = ref('')

const hacerBusqueda = (valor: string) => {
  console.log('Buscar:', valor)
}
</script>

<template>
  <header class="barra-app">
    <div class="barra-app__contenido">
      <!-- Izquierda: placeholder para logo / icono -->
      <div class="barra-app__lado-izquierdo">
        <span class="marca-placeholder">[ Icon Placeholder ]</span>
      </div>

      <div class="barra-app__buscador">
        <BarraBusqueda v-model="terminoBusqueda" @buscar="hacerBusqueda" />
      </div>

      <nav class="barra-app__acciones">
        <button
          class="boton-icono"
          :class="{ 'boton-icono--activo': opcionActiva === 'chat' }"
          type="button"
          @click="seleccionarOpcion('chat')"
        >
          <BaseIcon nombre="chat" tamaño="md" />
        </button>

        <button
          class="boton-icono"
          :class="{ 'boton-icono--activo': opcionActiva === 'lista' }"
          type="button"
          @click="seleccionarOpcion('lista')"
        >
          <BaseIcon nombre="lista" tamaño="md" />
        </button>

        <button
          class="boton-icono"
          :class="{ 'boton-icono--activo': opcionActiva === 'inicio' }"
          type="button"
          @click="seleccionarOpcion('inicio')"
        >
          <BaseIcon nombre="inicio" tamaño="md" />
        </button>

        <button
          class="boton-icono"
          :class="{ 'boton-icono--activo': opcionActiva === 'buscar' }"
          type="button"
          @click="seleccionarOpcion('buscar')"
        >
          <BaseIcon nombre="buscar" tamaño="md" />
        </button>

        <button
          class="boton-icono"
          :class="{ 'boton-icono--activo': opcionActiva === 'perfil' }"
          type="button"
          @click="seleccionarOpcion('perfil')"
        >
          <BaseIcon nombre="perfil" tamaño="md" />
        </button>
      </nav>
    </div>
  </header>
</template>

<style scoped>
.barra-app {
  background-color: var(--color-primary);
  color: var(--c-white);
  padding-block: 2rem;
  padding-inline: 2rem;
  position: sticky;
  top: 0;
  z-index: 999;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.08);
  min-height: 80px;
}

.barra-app__contenido {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.barra-app__lado-izquierdo {
  min-width: 140px;
}

.marca-placeholder {
  font-size: var(--fs-sm);
}

.barra-app__buscador {
  flex: 1;
  display: flex;
  justify-content: center;
}

/* Botonera derecha */
.barra-app__acciones {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.boton-icono {
  border: none;
  background: transparent;
  cursor: pointer;
  padding: 0.6rem;
  border-radius: 999px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  transition:
    background-color 0.15s ease,
    transform 0.1s ease,
    box-shadow 0.15s ease,
    color 0.15s ease;
  color: var(--c-white);
}

.boton-icono:hover {
  background-color: rgba(255, 255, 255, 0.18);
  transform: translateY(-1px);
}

.boton-icono--activo {
  background-color: var(--c-white);
  color: var(--color-primary);
  box-shadow: 0 0 0 2px rgba(255, 255, 255, 0.6);
  transform: translateY(-1px);
}
</style>
