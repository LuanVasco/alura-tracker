<template>
    <BoxTask>
        <div class="columns clicavel" @click="tarefaClicada">
            <div class="column is-4">
                {{ tarefa.descricao || 'Tarefa sem descrição' }}
            </div>
            <div class="column is-3">
                {{ tarefa.projeto?.nome || 'N/D' }}
            </div>
            <div class="column">
                <CronometroTask :tempoEmSegundos="tarefa.duracaoEmSegundos"/>
            </div>
        </div>
    </BoxTask>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import CronometroTask from '@/components/CronometroTask.vue'
import BoxTask from '@/components/BoxTask.vue'
import ITarefa from '@/interfaces/ITarefa'

export default defineComponent({
   name: "TarefaItem",
   components: {
    CronometroTask,
    BoxTask
   },
   emits: ['aoTarefaClicada'],
   props: {
    tarefa: {
        type: Object as PropType<ITarefa>,
        required: true
    }
   },
   methods: {
    tarefaClicada() : void {
        this.$emit('aoTarefaClicada', this.tarefa)
    }
   }
})
</script>

<style scoped>
.clicavel {
    cursor: pointer;
}
</style>