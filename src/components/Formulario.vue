<template>
  <div class="container">
      <div class="row">
            <form class="base" >
                <div class="col-3">
                    <label for="nombre" >Nombre y Apellido: </label>
                </div>
                <div class="col-9">
                    <input type="text" id="nombre" placeholder="Ingrese su Nombre y Apellido" class="" @keyup="validarNombre" v-model="persona.nombre"/>
                </div>
                <div class="row" v-if='nombreValido != ""'>
                    <p class="datoinvalido">{{ nombreValido }}</p>
                </div>
                 <br>
                <div class="col-3">
                    <label for="edad">Edad: </label>
                </div>
                <div class="col-9">
                    <input type="number" id="edad" placeholder="Ingrese su Edad" class="" @keyup="validarEdad" v-model="persona.edad"/>
                </div>
                <div class="row" v-if='edadValida != ""'>
                    <p class="datoinvalido">{{ edadValida }}</p>
                </div>
                <br>
                <div class="row">
                        <select data-style="btn-danger" class="form-select form-select-lg mb-3"
                            aria-label="Default select example" v-model="persona.sexo">
                            <option value="" selected></option>
                            <option v-for="sexo in listaSexo" :value="sexo.sexo" :key="sexo.id" >{{ sexo.sexo }}</option>
                        </select>
                </div>
                 <br>
                <div class="col-3">
                    <label for="correo" >Correo Electronico: </label>
                </div>
                <div class="col-9">
                    <input type="text" id="correo" placeholder="Ingrese su correo electronico" class="" @keyup="validarCorreo" v-model="persona.correo"/>
                </div>
                <div class="row" v-if='correoValido != ""'>
                    <p class="datoinvalido">{{ correoValido }}</p>
                </div>
                 <br>
                <div class="col-3">
                    <label for="contrasena" >Contraseña: </label>
                </div>
                <div class="col-9">
                    <input type="password" id="contrasena" placeholder="Ingrese su contraseña" class="" @keyup="validarContra" v-model="persona.contrasena"/>
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
export default {
    data(){
        return{
            persona: {
                nombre: "",
                edad: "",
                sexo: "",
                correo: "",
                contrasena: "",
            },
            listaSexo: [
                {
                    id: 'A',
                    sexo: 'Femenino'
                },
                {
                    id: 'B',
                    sexo: 'Masculino'
                },
                {
                    id: 'C',
                    sexo: 'No Binario'
                },
                {
                    id: 'D',
                    sexo: 'Otros'
                }
            ],
            nombreValido: "",
            edadValida: "",
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
           if (valcorreo.test(this.persona.correo)){
                this.correoValido = "";
                return true;
            } else {
                this.correoValido = "Mail incorrecto";
                return false;
            }

        },
        validarEdad(){
            if (this.persona.edad >= 18 ){
                this.edadValida = "";
                return true;
            } else {
                this.edadValida = "ingrese una edad valida, Mayor a 18.";
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
        agregarPersona() {
            this.$emit('nueva-persona', this.persona);
            this.persona.nombre = "";
            this.persona.edad = "";
            this.persona.sexo = "";
            this.persona.correo = "";
            this.persona.contrasena = "";
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
