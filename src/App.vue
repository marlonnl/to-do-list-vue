<script setup>
import { reactive } from 'vue';

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
        <header class="p-5 mb-4 mt-4 bg-light rounded-3">
            <h1>Tarefas</h1>
            <p>
                {{ getOnGoingTasks().length }} tarefas pendentes
            </p>
        </header>

        <form @submit.prevent="addTask">
            <div class="row">

                <div class="col">
                    <input :value="estado.tempTask" @change="evento => estado.tempTask = evento.target.value" required class="form-control" type="text" placeholder="Descrição da tarefa">
                </div>

                <div class="col-md-1">
                    <button class="btn btn-primary" type="submit">Cadastrar</button>
                </div>

                <div class="col-md-2">
                    <select @change="evento => estado.filtro = evento.target.value" class="form-control">
                        <option value="all">Todas as tarefas</option>
                        <option value="pending">Pendentes</option>
                        <option value="finished">Finalizadas</option>
                    </select>
                </div>
            </div>
        </form>

        <ul class="list-group mt-4">
            <li v-for="tarefa in getFilteredTasks()" class="list-group-item">
                <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
                <label :class="{ finished: tarefa.finalizada }" :for="tarefa.titulo" class="ms-2">
                    {{ tarefa.titulo }}
                </label>
            </li>
        </ul>

    </div>

</template>

<style scoped>
    .finished {
        text-decoration: line-through;
    }
</style>
