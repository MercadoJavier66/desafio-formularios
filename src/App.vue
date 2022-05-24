<template>
  <div id="app">
    <Titulo/>
    <br>
    <Formulario  @nueva-persona="agregarPersonaTabla"/>
    <br>
    <br>
    <Tabla :persona="personas"/>
  </div>
</template>

<script>
import Tabla from './components/Tabla.vue'
import Formulario from './components/Formulario.vue'
import Titulo from './components/Titulo.vue'


export default {
  name: 'App',
  components: {
    Titulo,
    Formulario,
    Tabla
  },
      data() {
        return {
            personas: []
        }
    },
    methods: {
        agregarPersonaTabla(persona) {
            console.log(persona);
            const nuevaPersona = {...persona};
            this.personas.push(nuevaPersona);
        }
    }
}
</script>

<style>
#app {
  text-align: center;
  margin-top: 60px;
}
</style>
