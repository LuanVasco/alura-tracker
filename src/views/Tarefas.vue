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
        <div class="modal is-active">
          <div class="modal-background"></div>
          <div class="modal-card">
            <header class="modal-card-head">
              <p class="modal-card-title">Modal title</p>
              <button class="delete" aria-label="close"></button>
            </header>
            <section class="modal-card-body">
              <!-- Content ... -->
            </section>
            <footer class="modal-card-foot">
              <button class="button is-success">Save changes</button>
              <button class="button">Cancel</button>
            </footer>
          </div>
        </div>
    </div>
  </template>
  
  <script lang="ts">
  import { useStore } from "@/store";
  import { computed, defineComponent } from 'vue';
  import FormularioPlay from '@/components/FormularioPlay.vue';
  import TarefaItem from '@/components/TarefaItem.vue';
  import BoxTask from '@/components/BoxTask.vue';
  import { CADASTRAR_TAREFA, OBTER_PROJETOS, OBTER_TAREFAS } from "@/store/tipo-acoes";
  import ITarefa from "@/interfaces/ITarefa";
  
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
      salvarTarefa(tarefa: ITarefa) {
        this.store.dispatch(CADASTRAR_TAREFA, tarefa)
      },
    },
    setup() {
        const store = useStore()
        store.dispatch(OBTER_TAREFAS)
        store.dispatch(OBTER_PROJETOS)
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
  