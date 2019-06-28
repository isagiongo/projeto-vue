<template>
  <div class="corpo">
    <h1 class="titulo">{{ titulo }}</h1>

    <ul class="lista-fotos">
      <li class="lista-fotos-itens" v-for="foto of fotos">

        <meu-painel :titulo="foto.titulo">
            <img class="imagem-responsiva" :src="foto.url" :alt="foto.descricao">
        </meu-painel>

      </li>
    </ul>
  </div>
</template>

<script>
import Painel from './components/shared/painel/Painel';

export default {
  components: {
    'meu-painel' : Painel
  },
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
  
  .imagem-responsiva {
    width: 100%;
  }

  .lista-fotos .lista-fotos-itens {
    display: inline-block;
  }
</style>
