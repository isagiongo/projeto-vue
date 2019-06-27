<template>
  <div class="corpo">
    <h1 class="titulo">{{ titulo }}</h1>
    <ul class="lista-fotos">
      <li class="lista-fotos-itens" v-for="foto of fotos">
        <img :src="foto.url" :alt="foto.descricao">
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data () {
    return {
      titulo: 'Alurapic',
      fotos: []
    }
  },
  created () {
    this.$http.get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(fotos => this.fotos = fotos, erro => console.log(erro));
  }
}
</script>

<style>
  .corpo {
    font-family: Arial, Helvetica, sans-serif;
    width: 96%;
    margin: 0 auto;
  }

  .titulo {
    text-align: center;
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-itens {
    display: inline-block;
  }
</style>
