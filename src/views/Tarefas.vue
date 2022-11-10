<template>
    <FormularioPlay @aoSalvarTarefa="salvarTarefa"/>
    <div class="lista">
        <TarefaItem 
        v-for="(tarefa, index) in tarefas"
        :key="index"
        :tarefa="tarefa"
        />
        <BoxTask v-if="listaEstaVazia">
            Você não está muito produtivo hoje :(
        </BoxTask>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent } from 'vue';
  import FormularioPlay from '@/components/FormularioPlay.vue';
  import TarefaItem from '@/components/TarefaItem.vue';
  import BoxTask from '@/components/BoxTask.vue';
  import ITarefa from '@/interfaces/ITarefa';
  
  export default defineComponent({
    name: 'App',
    components: {
      FormularioPlay,
      TarefaItem,
      BoxTask
    },
    data() {
      return {
        tarefas: [] as ITarefa[],
      }
    },
    computed: {
      listaEstaVazia() : boolean {
        return this.tarefas.length === 0
      }
    },
    methods: {
      salvarTarefa(tarefa: ITarefa) {
        this.tarefas.push(tarefa)
      },
    }
  });
  </script>

<style>
.lista {
  padding: 1.25rem
}
</style>
  