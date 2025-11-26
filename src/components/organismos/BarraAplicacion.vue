<script setup lang="ts">
import { ref } from 'vue'
import BaseIcon from '@/components/atomos/BaseIcon.vue'
import BarraBusqueda from '@/components/moleculas/BarraBusqueda.vue'

/**
 * Opciones disponibles en la barra de aplicación.
 */
type OpcionHeader = 'chat' | 'lista' | 'inicio' | 'buscar' | 'perfil'

const opcionActiva = ref<OpcionHeader>('perfil')

const emit = defineEmits<{
  (e: 'cambiar-vista', vista: OpcionHeader): void
}>()

/**
 * Selecciona una opción en la barra de aplicación y emite un evento de cambio de vista.
 * @param opcion - La opción seleccionada.
 */
const seleccionarOpcion = (opcion: OpcionHeader) => {
  opcionActiva.value = opcion
  emit('cambiar-vista', opcion)
}

/**
 * Término de búsqueda ingresado por el usuario.
 */
const terminoBusqueda = ref('')

/**
 * Realiza una búsqueda con el término proporcionado.
 * @param valor - El término de búsqueda.
 */
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

@media (max-width: 768px) {
  .barra-app {
    padding-block: 0.75rem;
    padding-inline: 1rem;
    min-height: auto;
  }

  .barra-app__contenido {
    flex-wrap: wrap;
    gap: 0.75rem;
  }

  .barra-app__lado-izquierdo {
    min-width: auto;
    flex: 1 0 100%;
  }

  .barra-app__buscador {
    order: 3;
    flex: 1 0 100%;
    justify-content: stretch;
  }

  .barra-app__acciones {
    order: 2;
    margin-left: auto;
    gap: 0.5rem;
  }

  .barra-app__buscador :deep(.buscador) {
    min-width: 100%;
    max-width: 100%;
  }
}

@media (max-width: 768px) {
  .barra-app {
    padding-block: 0.75rem;
    padding-inline: 1rem;
    min-height: auto;
  }

  .barra-app__contenido {
    flex-wrap: wrap;
    gap: 0.75rem;
  }

  .barra-app__lado-izquierdo {
    order: 1;
    flex: 1 0 100%;
    min-width: auto;
  }

  .barra-app__buscador {
    order: 2;
    flex: 1 0 100%;
    justify-content: stretch;
  }

  .barra-app__buscador :deep(.buscador) {
    min-width: 100%;
    max-width: 100%;
  }

  .barra-app__acciones {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;

    background-color: var(--color-primary);
    padding: 0.5rem 1.5rem;

    display: flex;
    justify-content: space-around;
    align-items: center;
    gap: 0.5rem;

    border-radius: 0;
    box-shadow: 0 -2px 6px rgba(0, 0, 0, 0.25);
    z-index: 1000;
  }
}
</style>
