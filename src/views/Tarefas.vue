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
  import { useStore } from "@/store";
  import { computed, defineComponent } from 'vue';
  import FormularioPlay from '@/components/FormularioPlay.vue';
  import TarefaItem from '@/components/TarefaItem.vue';
  import BoxTask from '@/components/BoxTask.vue';
  import { OBTER_TAREFAS } from "@/store/tipo-acoes";
  
  export default defineComponent({
    name: 'TarefasView',
    components: {
      FormularioPlay,
      TarefaItem,
      BoxTask
    },
    computed: {
      listaEstaVazia() : boolean {
        return this.tarefas.length === 0
      }
    },
    methods: {
      // salvarTarefa(tarefa: ITarefa) {
      //   this.tarefas.push(tarefa)
      // },
    },
    setup() {
        const store = useStore()
        store.dispatch(OBTER_TAREFAS)
        return {
            tarefas: computed(() => store.state.tarefas),
            store
        }
    },
  });
  </script>

<style>
.lista {
  padding: 1.25rem
}
</style>
  