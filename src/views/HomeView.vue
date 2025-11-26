<script setup lang="ts">
import MainLayout from '../layouts/MainLayout.vue'
import TarjetaPerfilResumen from '@/components/organismos/TarjetaPerfilResumen.vue'
import PestanasSeccion from '@/components/moleculas/PestanasSeccion.vue'
import FichaTutorias from '@/components/organismos/FichaTutorias.vue'
import FichaMaterial from '@/components/organismos/FichaMaterial.vue'
import { ref } from 'vue'

/**
 * Ruta roja::
 * El usuario desde la AppBar de navegación, selecciona el icono de perfil.
 * Se redirige a esta vista en donde esta rura representa el flujo principal del usuario
 * Mentor para acceder, revisar y gestionar sus tutorías dentro del sistema, asi como editar
 * su perfil o cerrar sesión.
 */

type Pestaña = 'material' | 'retroalimentacion' | 'avisos'

const pestañaActual = ref<Pestaña>('material')

const usuario = { nombre: 'Cesar Lara', rol: 'Mentor' }

interface Materia {
  id: string
  nombre: string
  fecha: string
  horario: string
  grupo: string
}

const materias = ref<Materia[]>([
  { id: '1', nombre: 'Nombre Materia', fecha: 'I-000', horario: '08:00-09:00', grupo: 'I-000' },
  { id: '2', nombre: 'Nombre Materia', fecha: 'I-0XX', horario: '10:00-11:00', grupo: 'I-0XX' },
  { id: '3', nombre: 'Nombre Materia', fecha: 'I-0XX', horario: '10:00-11:00', grupo: 'I-0XX' },
  { id: '4', nombre: 'Nombre Materia', fecha: 'I-0XX', horario: '10:00-11:00', grupo: 'I-0XX' },
])

// para abrir la ficha de material
const materiaSeleccionada = ref<Materia | null>(null)

const consultarMateria = (materia: Materia) => {
  materiaSeleccionada.value = materia
}

// datos de ejemplo dentro de la ficha
const recursos = ref([
  { id: 'r1', nombre: 'Nombre Material', mentor: 'Nombre Mentor' },
  { id: 'r2', nombre: 'Nombre Material', mentor: 'Nombre Mentor' },
  { id: 'r3', nombre: 'Nombre Material', mentor: 'Nombre Mentor' },
  { id: 'r4', nombre: 'Nombre Material', mentor: 'Nombre Mentor' },
])

const cerrarFichaMaterial = () => {
  materiaSeleccionada.value = null
}
</script>

<template>
  <MainLayout>
    <TarjetaPerfilResumen :nombre-usuario="usuario.nombre" :rol-usuario="usuario.rol" />

    <div class="separacion-tabs">
      <PestanasSeccion :activa-inicial="pestañaActual" @cambiar="pestañaActual = $event" />
    </div>

    <div class="separacion-tabs">
      <FichaTutorias
        v-if="pestañaActual === 'material' && !materiaSeleccionada"
        :materias="materias"
        @consultar-materia="consultarMateria"
      />

      <FichaMaterial
        v-if="materiaSeleccionada"
        :nombre-materia="materiaSeleccionada.nombre"
        :recursos="recursos"
        @volver="cerrarFichaMaterial"
      />
    </div>
  </MainLayout>
</template>

<style>
.separacion-tabs {
  margin-top: 1.5rem;
}
</style>
