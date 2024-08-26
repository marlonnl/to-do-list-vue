<script setup>
    const props = defineProps(['tarefas']);
</script>

<template>
    <ul class="list-group mt-4">
        <li v-for="tarefa in props.tarefas" class="list-group-item">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
            <label :class="{ finished: tarefa.finalizada }" :for="tarefa.titulo" class="ms-2">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
    .finished {
        text-decoration: line-through;
    }
</style>