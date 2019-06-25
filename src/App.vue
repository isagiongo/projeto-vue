<template>
  <div>
    <h1>{{ titulo }}</h1>
    <img :src="foto.url" :alt="foto.descricao">
  </div>
</template>

<script>
export default {
  data () {
    return {
      titulo: 'Alurapic',
      foto: {
        descricao: 'gato preto',
        url: 'https://www.infoescola.com/wp-content/uploads/2010/12/Gato-Bombaim_774381946.jpg'
      }
    }
  }
}
</script>

<style>
</style>
