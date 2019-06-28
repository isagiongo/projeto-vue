<template>
  <div class="corpo">
    <h1 class="titulo">{{ titulo }}</h1>

    <input type="search" class="filtro" @input="filtro = $event.target.value" placeholder="Pesquise pelo título da foto">
    {{ filtro }}
    <ul class="lista-fotos">
      <li class="lista-fotos-itens" v-for="foto of fotosComFiltro">

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
      fotos: [],
      filtro: ''
    }
  },
  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }
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

  .filtro {
    display: block;
    width: 80%;
    align-self: auto;
  }
</style>
