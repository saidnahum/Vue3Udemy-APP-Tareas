<template>
  <div class="alert alert-warning mt-3 d-flex justify-content-between align-items-center">
    <p class="m-0" :class="{'tachado': contenidoTarea.estado === true}">{{contenidoTarea.texto}}</p>
    <div>
      <i 
        class="fas fa-undo-alt mx-2 text-success" 
        role="button"
        @click="modificar(contenidoTarea.id)"
        v-if="contenidoTarea.estado"
      >

      </i>
      <i 
        class="fas fa-check-circle mx-2 text-success" 
        role="button"
        @click="modificar(contenidoTarea.id)"
        v-else
      >

      </i>
      <i 
        class="fas fa-minus-circle text-danger" 
        role="button"
        @click="eliminar(contenidoTarea.id)"
      >
      </i>
    </div>
  </div>
</template>

<script>
import { inject } from '@vue/runtime-core'
export default {
  props: {
    contenidoTarea: {
      type: Object,
      required: true
    }
  },
  setup(){
    const tareas = inject('tareasKey')

    const eliminar = id => {
      tareas.value = tareas.value.filter(item => item.id !== id)
    }

    const modificar = id => {
      tareas.value = tareas.value.map(item => {
        if(item.id === id){
          item.estado = !item.estado
        }
        return item
      })
    }

    return {eliminar, modificar}
  }
}
</script>

<style scoped>
  .tachado {
    text-decoration: line-through;
  }
</style>