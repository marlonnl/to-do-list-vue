<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive ({
    // all, pending, finished
    filtro: 'all',
    tempTask: '',
    tarefas: [
        {
            titulo: 'Comprar melão',
            finalizada: false,
        },
        {
            titulo: 'Lavar cuecas',
            finalizada: false,
        },
        {
            titulo: 'Plantar horta',
            finalizada: true,
        },
    ]
})

const getOnGoingTasks = () => {
    // retorna apenas as tarefas com false
    return estado.tarefas.filter(tarefa => !tarefa.finalizada);
}

const getFinishedTasks = () => {
    // retorna apenas as tarefas com false
    return estado.tarefas.filter(tarefa => tarefa.finalizada);
}

const getFilteredTasks = () => {
    const { filtro } = estado;

    switch (filtro) {
        case 'pending':
            return getOnGoingTasks();

        case 'finished':
            return getFinishedTasks();

        default:
            return estado.tarefas;
    }
}

const addTask = () => {
    estado.tarefas.push({
        titulo: estado.tempTask,
        finalizada: false,
    })

    estado.tempTask = '';
}

</script>

<template>

    <div class="container">

        <Cabecalho :pendentes="getOnGoingTasks().length" />
        <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :temp-task="estado.tempTask" :edit-temp-task="evento => estado.tempTask = evento.target.value" :add-tarefa="addTask" />
        <ListaDeTarefas :tarefas="getFilteredTasks()" />

    </div>

</template>
