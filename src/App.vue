<template>
  <main
    class="columns is-gapless is-multiline"
    :class="{ 'modo-escuro': modoEscuroAtivo }"
  >
    <div class="column is-one-quarter">
      <BarraLateral @alterandoTema="trocarTema" />
    </div>
    <div class="column is-three-quarters conteudo">
      <FormularioTask @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <QuadroTarefas v-if="listaTarefasVazia"
          >Sem tarefas realizadas!</QuadroTarefas
        >
        <TarefaExecutada
          v-for="(tarefa, index) in tarefas"
          :key="index"
          :tarefa="tarefa"
        />
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import FormularioTask from './components/FormularioTask.vue';
import TarefaExecutada from './components/TarefaExecutada.vue';
import QuadroTarefas from './components/QuadroTarefas.vue';
import ITarefaExecutada from '../src/interface/ITarefaExecutada';

export default defineComponent({
  name: 'App',
  data() {
    return {
      tarefas: [] as ITarefaExecutada[],
      modoEscuroAtivo: false,
    };
  },
  computed: {
    listaTarefasVazia(): boolean {
      return this.tarefas.length === 0;
    },
  },
  methods: {
    salvarTarefa(tarefa: ITarefaExecutada) {
      this.tarefas.push(tarefa);
    },
    trocarTema(modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo;
    },
  },
  components: { BarraLateral, FormularioTask, TarefaExecutada, QuadroTarefas },
});
</script>

<style scoped>
.lista {
  padding: 1.25rem;
}

main {
  --bg-primary: #fff;
  --text-primary: #000;
}
main.modo-escuro {
  --bg-primary: #2b2d42;
  --text-primary: #ddd;
}
.conteudo {
  background-color: var(--bg-primary);
}
</style>
