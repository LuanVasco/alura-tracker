<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <CronometroTask :tempoEmSegundos="tempoEmSegundos"/>
        <BotaoTask @clicado="iniciar" icone="fas fa-play" texto="play" :desabilitado="cronometroAtivo" />
        <BotaoTask @clicado="finalizar" icone="fas fa-stop" texto="stop" :desabilitado="!cronometroAtivo" />
       
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import CronometroTask from "@/components/CronometroTask.vue"
import BotaoTask from "@/components/BotaoTask.vue"
export default defineComponent({
    name: "TemporizadorTask",
    emits: ['aoTemporizadorFinalizado'],
    components: {
        CronometroTask,
        BotaoTask
    },
    data() {
        return {
            tempoEmSegundos: 0,
            cronometroId: 0,
            cronometroAtivo: false,
        }
    },
    methods: {
        iniciar() {
            this.cronometroAtivo = true
            this.cronometroId = setInterval(() => {
                this.tempoEmSegundos += 1
            }, 1000)
        },
        finalizar() {
            this.cronometroAtivo = false
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            clearInterval(this.cronometroId)
            this.tempoEmSegundos = 0
        }
    }
})
</script>
