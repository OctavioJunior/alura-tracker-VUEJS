<template>
  <QuadroTarefas>
    <div class="columns">
      <div class="column is-7">
        {{ tarefa.descricao || 'Tarefa Desconhecida' }}
      </div>
      <div class="column">
        <CronometroTask :tempoEmSegundos="tarefa.duracaoEmSegundos" />
      </div>
    </div>
  </QuadroTarefas>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import CronometroTask from './CronometroTask.vue';
import QuadroTarefas from './QuadroTarefas.vue';
import ITarefaExecutada from '@/interface/ITarefaExecutada';
export default defineComponent({
  name: 'TarefaExecutada',
  props: {
    tarefa: {
      type: Object as PropType<ITarefaExecutada>,
      required: true,
    },
  },
  components: { CronometroTask, QuadroTarefas },
});
</script>
