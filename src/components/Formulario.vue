<script setup>
    const props = defineProps(['addTarefa', 'tempTask', 'trocarFiltro', 'editTempTask'])
</script>

<template>
    <form @submit.prevent="props.addTarefa">
            <div class="row">

            <div class="col">
                <input :value="props.tempTask" @change="props.editTempTask" required class="form-control" type="text" placeholder="Descrição da tarefa">
            </div>

            <div class="col-md-1">
                <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>

            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="all">Todas as tarefas</option>
                    <option value="pending">Pendentes</option>
                    <option value="finished">Finalizadas</option>
                </select>
            </div>
        </div>

    </form>
</template>