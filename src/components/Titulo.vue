<template>
  <div>
    <h2 class="tit">{{ titulo }}</h2>
  </div>
</template>

<script>
export default {
      name: 'Titulo',
  data() {
      return {
        titulo: 'Desafio - Formularios',
      }
  },
}
</script>

<style scoped>
.tit{
    font: bold;
    color: rgb(15, 126, 0);
    }
</style>
