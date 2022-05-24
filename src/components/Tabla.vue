<template>
    <div class="container" >
        <table class="table">
            <thead>
                <tr>
                    <th>Nombre</th>
                    <th>Edad</th>
                    <th>Sexo</th>
                    <th>Correo</th>
                    <th>Contraseña</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(persona, p) in persona" :key="p">
                    <td>{{persona.nombre}}</td>
                    <td>{{persona.edad}}</td>
                    <td>{{persona.sexo}}</td>
                    <td>{{persona.correo}}</td>
                    <td>{{persona.contrasena}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    props: {
        persona: {
            type: Array,
            required: true,
        }
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
