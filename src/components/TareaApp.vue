<template>
  <h1 class="text-center mb-3">APP Tareas</h1>
  <tarea-form/>
  <TareaItem
    v-for="tarea in tareas" :key="tarea.id"
    :contenidoTarea="tarea" 
  />

  <div class="alert alert-dark mt-3" v-if="tareas.length === 0">
    Sin tareas pendientes!! 😎👍
  </div>
  <!-- <p>{{tareas}}</p> -->
</template>

<script>
import { ref } from '@vue/reactivity'
import TareaItem from './TareaItem'
import TareaForm from './TareaForm.vue'
import { provide, watchEffect } from '@vue/runtime-core'
export default {
  components: {TareaItem, TareaForm},
  setup(){
    const tareas = ref([])

    provide('tareasKey', tareas)

    if(localStorage.getItem('tareas')){
      tareas.value = JSON.parse(localStorage.getItem('tareas'))
    }

    watchEffect(() => {
      localStorage.setItem('tareas', JSON.stringify(tareas.value))
    })

    return {tareas}
  }
}
</script>

<style>

</style>