<script setup lang="ts">
import MainLayout from '../layouts/MainLayout.vue'
import TarjetaPerfilResumen from '@/components/organismos/TarjetaPerfilResumen.vue'
import PestanasSeccion from '@/components/moleculas/PestanasSeccion.vue'
import FichaTutorias from '@/components/organismos/FichaTutorias.vue'
import { ref } from 'vue'

/**
 * Ruta roja::
 * El usuario desde la AppBar de navegación, selecciona el icono de perfil.
 * Se redirige a esta vista en donde esta rura representa el flujo principal del usuario
 * Mentor para acceder, revisar y gestionar sus tutorías dentro del sistema, asi como editar
 * su perfil o cerrar sesión.
 */

const usuario = {
  nombre: 'Cesar Lara',
  rol: 'Mentor',
}

type Pestaña = 'material' | 'retroalimentacion' | 'avisos'

const pestañaActual = ref<Pestaña>('material')

const alCambiarPestaña = (valor: Pestaña) => {
  pestañaActual.value = valor
}

interface Materia {
  id: string
  nombre: string
  fecha: string
  horario: string
  grupo: string
}

const materias = ref<Materia[]>([
  {
    id: '1',
    nombre: 'Nombre Materia',
    fecha: 'I-000',
    horario: '08:00 - 09:00',
    grupo: 'I-000',
  },
  {
    id: '2',
    nombre: 'Nombre Materia',
    fecha: 'I-0XX',
    horario: '10:00 - 11:00',
    grupo: 'I-0XX',
  },
  {
    id: '3',
    nombre: 'Nombre Materia',
    fecha: 'I-0XX',
    horario: '10:00 - 11:00',
    grupo: 'I-0XX',
  },
  {
    id: '4',
    nombre: 'Nombre Materia',
    fecha: 'I-0XX',
    horario: '10:00 - 11:00',
    grupo: 'I-0XX',
  },
])

const consultarMateria = (materia: Materia) => {
  console.log('Consultar materia:', materia)
}
</script>

<template>
  <MainLayout>
    <TarjetaPerfilResumen :nombre-usuario="usuario.nombre" :rol-usuario="usuario.rol" />

    <div class="separacion-tabs">
      <PestanasSeccion :activa-inicial="pestañaActual" @cambiar="alCambiarPestaña" />
    </div>

    <div class="separacion-tabs">
      <!-- Ficha de tutorías solo cuando la pestaña "Material" está activa -->
      <FichaTutorias
        v-if="pestañaActual === 'material'"
        :materias="materias"
        @consultar-materia="consultarMateria"
      />
    </div>
  </MainLayout>
</template>

<style>
.separacion-tabs {
  margin-top: 1.5rem;
}
</style>
