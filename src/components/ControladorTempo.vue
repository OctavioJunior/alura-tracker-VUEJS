<template>
  <div class="is-flex is-align-items-center is-justify-content-space-between">
    <CronometroTask :tempoEmSegundos="tempoEmSegundos" />
    <BotaoControlador
      @clicado="iniciarContagem"
      icone="fas fa-play"
      textoDaAcao="start"
      :desabilitado="cronometroRodando"
    />
    <BotaoControlador
      @clicado="finalizarContagem"
      icone="fas fa-stop"
      textoDaAcao="stop"
      :desabilitado="!cronometroRodando"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CronometroTask from './CronometroTask.vue';
import BotaoControlador from './BotaoControlador.vue';
export default defineComponent({
  name: 'ControladorTempo',
  emits: ['aposPararCronometro'],
  components: {
    CronometroTask,
    BotaoControlador,
  },
  data() {
    return {
      tempoEmSegundos: 0,
      cronometro: 0,
      cronometroRodando: false,
    };
  },
  methods: {
    iniciarContagem() {
      this.cronometroRodando = true;
      this.cronometro = setInterval(() => {
        this.tempoEmSegundos += 1;
      }, 1000);
    },
    finalizarContagem() {
      this.cronometroRodando = false;
      clearInterval(this.cronometro);
      this.$emit('aposPararCronometro', this.tempoEmSegundos);
      this.tempoEmSegundos = 0;
    },
  },
});
</script>
