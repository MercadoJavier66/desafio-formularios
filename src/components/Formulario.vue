<template>
  <div class="container">
      <div class="row">
            <form class="base" >
                <div class="col-3">
                    <label for="nombre" >Nombre y Apellido: </label>
                </div>
                <div class="col-9">
                    <input type="text" id="nombre" maxlength="15" placeholder="Ingrese su Nombre y Apellido" class="" @keyup="validarNombre" v-model="persona.nombre"/>
                </div>
                <div class="row" v-if='nombreValido != ""'>
                    <p class="datoinvalido">{{ nombreValido }}</p>
                </div>
                 <br>
                <div class="col-3">
                    <label for="correo" >Correo Electronico: </label>
                </div>
                <div class="col-9">
                    <input type="text" id="correo" maxlength="20" placeholder="Ingrese su correo electronico" class="" @keyup="validarCorreo" v-model="persona.email"/>
                </div>
                <div class="row" v-if='correoValido != ""'>
                    <p class="datoinvalido">{{ correoValido }}</p>
                </div>
                 <br>
                <div class="col-3">
                    <label for="contrasena" >Contraseña: </label>
                </div>
                <div class="col-9">
                    <input type="password" id="contrasena" maxlength="12" placeholder="Ingrese su contraseña" class="" @keyup="validarContra" v-model="persona.contrasena"/>
                </div>
                <div class="row" v-if='contrasenaValida != ""'>
                    <p class="datoinvalido">{{ contrasenaValida }}</p>
                </div>
                <br>
                <div class="row">
                    <input type="button" class="btn-enviar" value="Enviar" @click="agregarPersona"/>
                </div>
            </form>
      </div>
  </div>
</template>

<script>

import Vue from 'vue'   // in Vue 2
import axios from 'axios'
import VueAxios from 'vue-axios'


Vue.use(VueAxios, axios)

export default {
    name: 'Formulario',
    data(){
        return{
            persona: {

            },
            nombreValido: "",
            correoValido: "",
            contrasenaValida: "",
        }
    },
    methods: {
        validarNombre(){
            const valnombre = /[a-zA-Z]{3,}\s[a-zA-Z]{3,}/g;
            if (valnombre.test(this.persona.nombre)){
            this.nombreValido = "";
                return true;
            } else {
                this.nombreValido = "El Nombre y Apellido debe contener al menos 3 caracteres.";
                return false;
            }
        },
        validarCorreo() {
            const valcorreo = /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/;
           if (valcorreo.test(this.persona.email)){
                this.correoValido = "";
                return true;
            } else {
                this.correoValido = "Mail incorrecto";
                return false;
            }

        },
        validarContra(){
            let reg_ex_password = /^(?=.*?[A-Z])(?=.*?[a-z])(?=.*?[0-9])(?=.*?[#?!@$%^&*-]).{8,}$/;
            if (reg_ex_password.test(this.persona.contrasena)){
                this.contrasenaValida = "";
                return true;
            } else {
                this.contrasenaValida = "La contraseña debe contener al menos 8 caracteres, una mayúscula, un caracter especial y un número."
                return false;
            }

        },
        async agregarPersona() {
             this.persona.tipoUsuario = "cliente"
            await Vue.axios({
                  method: 'post',
                url: 'https://628ee4bddc47852365360ef5.mockapi.io/api/v1/usuario',
                data: this.persona
            });
            this.persona = {}
        },

    }
}
</script>

<style scoped>
    input{
        width: 100%;
    }
    .col-3{
        text-align: initial;
    }
    .col-9{
        text-align: center;
    }
    .base{
        padding-right: 30px;
        padding-bottom: 20px;
        padding-left: 30px;
        padding-top: 20px;
        border: 5px solid #000000;
        background-color: rgb(223, 255, 223);
    }
    .datoinvalido{
        color: rgb(184, 0, 0);
        font-style: oblique;

    }
    .btn-enviar{
        background-color: #1bc501;

    }
</style>
