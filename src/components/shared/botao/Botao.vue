<template>
  <button @click="disparaAcao()" :class="estiloDoBotao" :type="tipo">{{ rotulo }}</button>
</template>

<script>
export default {
  
  props: {
      tipo: {
          required: true,
          type: String
      },
      rotulo: {
          required: true,
          type: String
      },
      confirmacao: Boolean,
      estilo: String
  },
  
  props: ["tipo", "rotulo", "confirmacao", "estilo"],

  methods: {
    disparaAcao() {
      if (this.confirmacao) {
        if (confirm("Confirma operação?")) {
          this.$emit("botaoAtivado");
        }
        return;
      }
      this.$emit("botaoAtivado");
    }
  },

  computed: {
    estiloDoBotao() {
      if (this.estilo == "padrao" || !this.estilo) return "botao botao-padrao";
      if (this.estilo == "alerta") return "botao botao-alerta";
    }
  }
};
</script>

<style scoped>
.botao {
  display: inline-block;
  padding: 10px;
  border-radius: 3px;
  margin: 10px;
  font-size: 1.2em;
}

.botao-alerta {
  background: firebrick;
  color: white;
}

.botao-padrao {
  background: darkcyan;
  color: white;
}
</style>
