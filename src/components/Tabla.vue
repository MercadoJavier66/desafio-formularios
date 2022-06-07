<template>
    <div class="container" >
        <table class="table">
            <thead>
                <tr>
                    <th>Nombre</th>
                    <th>Avatar</th>
                    <th>Correo</th>
                    <th>Contraseña</th>
                    <th>Tipo de Usuario</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(persona, p) in $store.state.personas" :key="p">
                    <td>{{persona.nombre}}</td>
                    <td><img :src="persona.avatar" width="60"></td>
                    <td>{{persona.email}}</td>
                    <td>{{persona.contrasena}}</td>
                    <td>{{persona.tipoUsuario}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>

import Vue from 'vue'   // in Vue 2
import axios from 'axios'
import VueAxios from 'vue-axios'


Vue.use(VueAxios, axios)

export default {
    data (){
        return{

        }
    },
    methods: {
        async getPersonas(){
            const personas = await Vue.axios({
                method: 'get',
                url: 'https://628ee4bddc47852365360ef5.mockapi.io/api/v1/usuario',
            });
            this.$store.state.personas = personas.data
        },
    },
    mounted (){
        this.getPersonas()
    }
}
</script>

<style scoped>
 .table {
    background-color: #fffdc0;
    border: 2px solid #000000;
    font-weight: bold;
    padding-right: 30px;
    padding-bottom: 20px;
    padding-left: 30px;
    padding-top: 20px;
 }


</style>
