<template>
  <header>
    <h1>
      <img src="../assets/logo.png" />
    </h1>
    <button class="button" @click="alterarModo">{{ textoBotao }}</button>
  </header>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'BarraLateral',
  data() {
    return {
      modoEscuroAtivo: false,
    };
  },
  computed: {
    textoBotao() {
      if (this.modoEscuroAtivo) {
        return 'Ativar modo claro';
      }
      return 'Ativar modo escuro';
    },
  },
  emits: ['alterandoTema'],
  methods: {
    alterarModo() {
      this.modoEscuroAtivo = !this.modoEscuroAtivo;
      this.$emit('alterandoTema', this.modoEscuroAtivo);
    },
  },
});
</script>

<style scoped>
header {
  background: #0d3b66;
  width: 100%;
  height: 100vh;
  padding: 1rem;
  text-align: center;
}

@media only screen and (max-width: 768px) {
  header {
    padding: 2.5rem;
    height: auto;
  }
}
</style>
