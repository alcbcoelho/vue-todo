<script setup>
const props = defineProps(["newTask", "registerTask", "changeFilter", "editNewTask"])
</script>

<template>
    <!-- @{event-name}.prevent: invokes e.preventDefault() -->
    <form @submit.prevent="props.registerTask">
      <div class="row">
        <div class="col">
          <input required @change="props.editNewTask" class="form-control" type="text" placeholder="Digite aqui a descrição da tarefa" :value="props.newTask">
        </div>
        <div class="col-md-1">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="props.changeFilter"  class="form-control">
            <option value="all">Todas as tarefas</option>
            <option value="pending">Tarefas pendentes</option>
            <option value="done">Tarefas finalizadas</option>
          </select>
        </div>
      </div>
    </form>
</template>